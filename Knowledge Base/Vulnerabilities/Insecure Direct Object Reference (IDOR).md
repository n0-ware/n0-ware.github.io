# Insecure Direct Object Reference (IDOR)
###### Tags[^1]
IDOR stands for Insecure Direct Object Reference and is a type of access control vulnerability. An [Access Control](../Concepts/Web/Access%20Control.md) [Vulnerability](../Concepts/General/Vulnerability.md) is when an attacker can gain access to information or actions not intended for them. An IDOR vulnerability can occur when a web server receives [User-Supplied Input](../Concepts/Web/User-Supplied%20Input.md) to retrieve objects (files, data, documents), and too much [Trust](../Concepts/General/Trust.md) as been placed on that input data, and the web application does not [Validation](../Concepts/General/Validation.md) whether the user should, in fact, have access to the requested object.

**TL;DR:** 

Change user-supplied data to get access you should not have

## Vulnerability

A product, user, service, or another unique identifier in a URL is a **must test**. IDOR can reveal sensitive information and potentially give usually restricted access to certain functions. 

### Locating IDOR 

#### **Three places**
##### In a [Queries](../Concepts/General/Queries.md) component
Data is passed in the URL when making a request to a website

![IDOR in a URL](Photos%20(Vulnerabilities)/IDOR-URL--THM.png)

**Protocol**: https:// **Domain**: website.thm **Page**: /profile **Query Component:** id=23

The `/profile` page is being requested, and the parameter id with the value of `23` is being passed in the query component. This page could potentially be showing us personal user information, and by changing the `id` parameter to another value, we could view other user's data.

##### Post Variables
Forms that [POST Request](../Concepts/Web/POST%20Request.md) on a website can reveal vulnerable fields if inspected. Often, in hidden fields. If able, changing the field in the `POST` request can give access elsewhere. 

![IDOR in a hidden field on a POST form](Photos%20(Vulnerabilities)/IDOR-Post_Form--THM.png)

Use a `POST` editor such as [BurpSuite](../../Tools,%20Binaries,%20and%20Programs/Information%20Gathering/Web%20Applications/BurpSuite.md) to modify the request as you send it

##### Cookies
[Cookies](../Concepts/Web/Cookies.md) are often used to save sessions/logins. Usually, it involves a [Sessions](../Concepts/Web/Sessions.md). Sometimes, these session id's can be hard coded using the *User ID* and offer an exploit path. 

![Hard Coded User ID in Cookie](../Concepts/Photos%20(Concepts)/Session-ID-UID_Hard_Coded--THM.png)

[^1]: #idor #accesscontrol #userinput #query #queries #post #session #bounty #cookies 
