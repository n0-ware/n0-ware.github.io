# Log Poisoning

<u>***Refs***</u>
[Local File Inclusion](Local%20File%20Inclusion%20(LFI).md)

## Description

**Log Poisoning** refers to an attack where an application's log files are manipulated to produce a negative result. Typically, the log is injected with malicious code that can do anything from divulging information to producing  [remote code execution](Remote%20Code%20Execution.md) depending on the type of [user supplied input](../Concepts/Web/User-Supplied%20Input.md) we can inject into the log. 

***This attack has two prerequisites to be effective::**

1. We can inject a malicious payload into a service's log files, such as *Apache*  or *SSH*. 
2. We have access to the log file, either directly or via some other vulnerability such as [local file inclusion (LFI)](Local%20File%20Inclusion%20(LFI).md), so we can view the executed code and/or add to the corrupted log file with more code.  

The prerequisites mean we need good enumeration and proof of concept skills beforehand to identify the vulnerability. It also requires some knowledge of how web applications work, such as when code is executed on the server-side and how that affects what we see on the client-side.

## Testing

Once you have determined you can view an application's log files, testing what you can control in the log file is the first step. If the malicious log is captured, we simply need to be able to access the log file to run the script. How you access the log and run the code varies from method to method

### With Curl
For example, a log that captures the `User-Agent` field may be vulnerable to [Injection](Injection.md) through a modified `User-Agent` field. Attackers can modify a `curl` command to submit a custom `User-Agent` field with the `-A` flag.  This custom field can contain a payload, sent via `HTTP` request with `curl`. An *Apache* server will then attempt to read the log file, potentially executing any code you submitted. 

`curl -A "Testing for RCE" https://vulnsite.io/index.html`

Following the `curl` request, we then verify the custom `User-Agent` field was recorded and confirm the vulnerability. 

> `curl` has a bit of a learning code, but it allows you to entirely customize an `HTTP` request. 

### SSH
If you are attacking `SSH`, this can be done via the username. Both require poor [user input](../Concepts/Web/User-Supplied%20Input.md) sanitation. 

## Exploiting

### PHP
We identify a log that stores four headers &mdash; username, IP address, `User-Agent`, and the page visited

Since we can control the `User-Agent` field when interacting with a web application, we send a custom request to the web application on a page we know is logged. 

`curl -A "Testing for RCE" https://vulnsite.io/index.php`

We then inspect the log file to see if the custom `User-Agent` was recorded in the log. 

Next, we send a "proof of concept" request injected with `PHP` code to see how the server/client renders the code. 
 
 `curl -A "<?php phpinfo()?>" https://www.vulnsite.io/index.php`
 
 Accessing the corrupted file will likely take some of [local file inclusion vulnerability](Local%20File%20Inclusion%20(LFI).md). Depending on how you access the log file, you will either see no `User-Agent` or the code will render the information on the screen. You may have to attempt to access the file in several ways to render the code where on the client-side. 
 
 Regardless, if you don't see your code rendered but also don't see the code itself, this is proof of [RCE](Remote%20Code%20Execution.md) and you may continue to exploit the service.
 
 > Not seeing the code you type in is a good sign because that means the code ran on the server. You may not be able to disclose information without a visual representation of the code on your screen, but you can still run code on the server, possibly writing files to an accessible location or simple generating a backdoor for you to access and gain a foothold on the server. 

### Corrupting Sessions

If an attacker can access the location [session](../Concepts/Web/Sessions.md) information is stored on a server and poor [user input](../Concepts/Web/User-Supplied%20Input.md) sanitation is in place, we can corrupt a session with some sort of malicious code, such as with `PHP` if the server is running a `PHP` backend. 

Session information is often stored in common locations, such as 
- `c:\Windows\Temp`
- `/tmp/`
- `/var/lib/php5`
- `/var/lib/php/session`

Consider a login screen where the username is stored. An attacker can submit a username such as `<?php phpinfo(); ?>` and navigate to where the sessions are stored to identify if the code is executed on the server-side. To find the correct `session_id`, simply use your browser's developer tools and locate the `PHPSESSID` or another relevant session (such as `JESSIONID` with Java) and access that file via the directory the sessions are stored in, such as `/tmp/sess_9lmhiq5msgbg2nbiha3tecjki2`. 

![PHPSESSID](Photos%20(Vulnerabilities)/LFI-PHPSESSIONID.png)

Proceed to poison the session with malicious code, then access that file on the server through a browser to verify you have successful execution. Accessing the file will likely require some kind of [local file inclusion vulnerability](Local%20File%20Inclusion%20(LFI).md)
