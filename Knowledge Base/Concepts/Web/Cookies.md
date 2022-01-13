# Cookies
Cookies are essentially tiny pieces of data (metadata) or information your computer stores locally that can be sent to a server when making a request. 

Can be assigned at any time and contain any value, allowing a web server to store any information it wants. 

Cookies are found within the *Developer Tools* section of your browser using <kbd>F12</kbd> or <kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>i</kbd>. 
- Firefox: Locate in the `Storage` tab
- Chrome: Locate in the `Application` tab. Select `Cookies` from the dropdown menu on the left side.

## Types
- session - Identify you and your access level for stateful communication with a webserver. Often called a  ([Sessions](Sessions.md)) and used for [Authentication](../General/Authentication.md)
- persistent
- secure
- HTTP-only
- Same-site
- Third-party
- Supercookie
- Zombie cookie
- Cookie wall

## Structure
Cookies *always* have a `Name` and `Value`. This is the "main pair", defining the name and value of the pair. Any other values after the first are `attribute-value` pairs. 

1. Name
2. Value
3. Zero or more attributes (name/value pairs)
	- Store information such as expiration, flags, domain, etc

Attackers are mstly concerned with the `Name` and `Value` of a cookie. The owebserver handles the remaining components. 

| Component | Purpose | Example |
| :-: | :-: | :-: | 
| Name | Unique cookie identifier (arbitrarily set by web-server). Always paired with the value component. | SessionID | 
| Value | Unique cookie value (arbitrarily set by web-server). Always paired with the name component | sty1z3kz11mpqxjv648mqwlx4ginpt6c |
| Domain | Originating domain of the cookie. Sets the scope of the cookie. |.tryhackme.com |
| Path | Local path to cookie. Sets the scope of the cookie. | / |
| Expires/Max-age | Date/time at which cookies expires | 2022-11-11T15:39:04.166Z |
| Size | Disk size of the cookie in bytes. This is typically {Name+Value} | 91 |
| HttpOnly | Cookie cannot be accessed through client-side scripts | (indicated by a checkmark) |
| Secure | Cookie is only sent over HTTPS | (indicated by a checkmark) |
| SameSite | Specifies when a cookie is sent through cross-site requests | none |
| SameParty | Extends the functionality of _SameSite_ attribute to First-Party sets. | (indicated by a checkmark) |
| Priority | Defines the importance of a cookie. Determines whether it should be removed or held on to | High |

Attribution: [TryHackMe](https://tryhackme.com)

![Cookies in a Browser](../Photos%20(Concepts)/Cookie-In-Browser.png)

## Values
Cookie values are encoded, not random strings. The values can be decoded into non-arbitrary values such as `JSON` or Javascript objects. 

Attackers can decode cookies to identify the underlying objects. Once identified, it can be modified, re-encoded in the same way, and submitted. 

An example decoded cookie:
```
{firstName:'n0ware', lastName:"s0mewhere", age:1337, eyecolor:"blue"}
```

## Uses

1. Personalization
2. Tracking
3. Session Management

#cookies #session #state #authentication 