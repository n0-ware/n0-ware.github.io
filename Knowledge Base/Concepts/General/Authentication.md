# Authentication

<a href="#windows-authentication">Windows Auth Methods</a>
## Description
Essentially the processes of verifying a user's identity to confirm without a doubt (ideally) that the user is who they say they are. Identity for authentication can be proven in several ways, including:
1. Using a known set of credentials sent to a server or a local database, such as a username and password
2. Token authentication (i.e., unique pieces of encrypted text like cookies, pre-generated API tokens, etc.)
3. Biometric authentication (fingerprints, voices, etc. )

Often conflated with authorization, but it is very different. Being *authorized* means that one is allowed, permitted,  or otherwise expected to have access to a certain piece of content or collection of assets/resources. Being *authenticated* means that the identity of a user is confirmed **and the user is authorized to access what they are authenticated for**. Authorization determines what the authenticated user can access. Authentication relates to the **C** in the **CIA** triad. It is used when protections and/or accountability is required for a set of resources. 

## Web

### Cookies
*<u>Cookie used for authentication</u>*

![](Photos%20(Concepts)/Cookie-In-HTTP-Request--THM.png)

The authentication processes can be as follows:
1. A request such as a login is usually made as a [POST Request](Web/POST%20Request.md)
2. Server verifies it received data and sets a unique cookie
	- Type of value determined by either best-practices or the web developer.
3. Once assigned, as long as it lives in your browser, all future [GET Request](Web/GET%20Request.md) requests will use that cookie to identify you and your access using [Deserialization](Web/Deserialization.md).

#authentication #authorization #webapp #tokens #cookies 

### AWS-CLI
AWS uses an *Access Key* and a *Secret Access Key* to authenticate users over the command line. 
For vulnerable S3, see [Insecure S3 Bucket Access](../../Vulnerabilities/Insecure%20S3%20Buckets.md)

## Windows Authentication Methods
<a id="windows-authentication" description="Explanation of Windows authentication methods">

### SAM
Windows stores various credentials in the *Security Accounts Manager* database. They are typically stored as [hashes](Hashing.md) of one of two kinds:

- **LAN Manager (LM)** &mdash; the oldest form of password storage used in Windows and kept around for legacy systems. The algorithm is weak, using a limited character set as input, making it possible to attempt all possible combinations rather easily.
- **NT Lan Manager (NTLM)** &mdash; The modern system of hashing used to store passwords.

### LSASS
The process Local Security Authority Subsystem Service (LSASS) steps in to retrieve the user's credentials from the [SAM](#SAM) database when a user logs in. It compares the provided credentials against the hashed form of the user's password. If they match, the user is logged in. 

LSASS stores the credentials in memory after this is successful. The is designed to be convenient, such as allowing them to use another resource without having to enter the credentials again. LSASS itself uses these credentials in-memory for other reasons, making it vulnerable to credential dumping. 