# Cross-Site Scripting (XSS)
- Tags[^1]

[^1]: #owasp #xss #injection #webapp 

## TOC-GH
- [Document Object Model DOM](#DOM)
	- [Example DOM XSS](#Example-DOM)
- [Reflected](#Reflected)
	- [Example Reflected XSS](#Example-Reflected)
- [Stored](#Stored)
	- [Example Stored XSS](#Example-Stored)
- [Blind](#Blind)
	- [Example Blind XSS](#Example-Blind)


## Description
[Cross-Site Scripting](Cross-Site%20Scripting%20(XSS).md), or *XSS*, is classified as an injection attack according to the [*OWASP Top 10 2021*](https://owasp.org/www-project-top-ten/). XSS involves *injecting* malicious JavaScript into a web application with the hope that it is executed by other users. 

Achieving XSS on a target can lead to multiple outcomes, including:
- Stealing cookies for [session hijacking](Session%20Hijacking.md)
- Running a keylogger
- Redirecting to an entirely different website
- Resetting their password
- Placing an order
- And more

## Types
There are four different types of XSS

### DOM
[Document Object Model](../Concepts/Web/Document%20Object%20Model%20(DOM).md), or DOM, is a programming interface for `HTML` and `XML` documents. DOM represents the page in a way that other programs can alter the document structure, style, and content. Since a web page is just a document, it can be rendered in multiple ways, most commonly either in a browser or as the `HTML` source code. 

DOM-based XSS is where malicious JavaScript is executed directly in a user's browser without the need for a new page to load or data to be submitted to backend code. This is 100% contained in the browser, and execution occurs when the JavaScript code in the website acts on input or user interaction

[Example DOM XSS](#Example%20DOM%20XSS)

### Reflected
Reflected XSS occurs when some [user supplied input](../Concepts/Web/User-Supplied%20Input.md)  or other data is sent in an [`HTTP` request](../Concepts/Web/HTTP%20Request.md) to an application and the application includes that data in a response in a way that is unsafe. 

[Example Reflected XSS](#Example%20Reflected%20XSS)

### Stored
Also known as *persistent XSS* occurs when an application receives data from an [untrusted](../Concepts/General/Trust.md) source and *stores* that data in later [HTTP responses](../Concepts/Web/HTTP%20Response.md) in an unsafe manner. The data can be stored in the database that feeds the application, for example. 

This is very common with comment boards, where users are able to submit input and that input is sent via an [HTTP POST request](../Concepts/Web/POST%20Request.md). Any user viewing the comment will execute the malicious JavaScript.

### Blind
Similar to stored in that it is stored in the web application, perhaps in a database, that is viewed later by another user, such as a help desk technician. The difference here between typical stored XSS is that the attacker cannot confirm that the attack was successful because they do not have access to the location the script was stored. 

## Finding

## Examples
### Example-DOM
A website's JavaScript gets contents from the `window.location.hash` and writes that information to the current page. The contents of this hash are not checked for malicious content, enabling the attacker to inject whatever JavaScript they would like onto the web page. 

These are often passed in the URL portion of a link to an unsuspecting user. 

### Example-Reflected 
Suppose a website includes a text input form that is immediately echoed on the page and the search is reflected in the browser. Take this for example

`https://vulnsite.com/search?term=banana`

If the application does not process, validate, or sanitize the data, it will simply return `HTML` code. 

`<p>You searched for "banana"</p>`

An attacker can abuse this behavior, crafting an attack such as

`https://vulnsite.com/search?=<script>/My-Bad-Payload/</script>`

The page will then render my script after the `?`

`<p>You searched for <script>/My-Bad-Payload/</script></p>`

If someone were to click this link, the attacker's payload would be executed in the victim browser within the context of that session

### Example-Stored
Imagine a scenario where a blog allows users to submit comments. The [POST Request](../Concepts/Web/POST%20Request.md) request might look something like this:

```
POST /post/comment HTTP/1.1  
Host: vulnsite.com  
Content-Length: 100  
  
postId=3&comment=I+love+making+comments.&name=n0_ware+knowns=n0_ware%40someemail.io
```

The web page renders the code as 

`<p>I love making comments</p>`

If the website does not process the data in any way, attackers could submit data  such as `comment=%3Cscript%3E%2FBad%2BInjection%2Bhere%2B*%2F%3C%2Fscript%3E` that would render as `<p><script>/Bad injection here/</script>`.

An example of changing user passwords on a comment board could look like this, where `/settings` is the URL where users reset their password, and this page is also vulnerable to XSS in the URL. 

`<script>fetch('/settings?new_password=gotcha');</script>`

When a user views this comment, their browser will execute the request. If the website happened to be `www.vulnsite.com`, the browser will execute the request `https://vulnsite.com/settings?new_password=gotcha`. At any time, the attacker can brute force potential user names with the password `gotcha` and compromise their account. 

### Example-Blind
An attacker submits a stored XSS payload in a contact request or helpdesk ticket that is later ran by a user working for the company. In this context, the attacker may be able to acquire privileged credentials only accessible to internal members of the organization managing the application. Consider the attack pattern as similar to an [example Stored XSS](#Example%20Stored%20XSS)