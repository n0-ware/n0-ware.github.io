# HTTP(S)

### Description
Hypertext Transfer Protocol (HTTP) is the protocol that specifies how a web browser and a web server communicate. This is a client-server protocol allowing for communication between a *client* and a *webserver*. 

Similar to a standard `TCP` network request, but, HTTP adds specific headers to identify the protocol and other information. 

With an HTTP request, the *method* and *target*  header will always be included. 
- **Target**: Specify what to retrieve
- **Method**: How to retrieve it


### Request/Response
<u>Example request:</u> 
```
http
GET / HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0 Firefox/87.0
Referer: https://tryhackme.com/
```

A successful request results in a response, including requested content and a status code[^1]. 
<u>Example response:</u> 
```
http
HTTP/1.1 200 OK
Server: nginx/1.15.8
Date: Wednesday, 24 Nov 2021 13:34:03 GMT
Content-Type: text/html
Content-Length: 98

<html>
<head>
    <title>Advent of Cyber</title>
</head>
<body>
    Welcome To Advent of Cyber!
</body>
</html>
```

HTTP(S) is a [stateless](Protocol%20States.md) protocol. [Cookies](Cookies.md) are used to manage states, identify users, and control access. This allows for a stateful connection. 

###### References:
[Authentication](../General/Authentication.md)



[^1]: [HTTP Response Status Codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)

#http #https #webapp #request #response #authentication #cookies 