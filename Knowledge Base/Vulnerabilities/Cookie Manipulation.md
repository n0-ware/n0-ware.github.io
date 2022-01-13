# Cookie Manipulation

[^1]: #cookies #encoding 

[Cookie](../Concepts/Web/Cookies.md) manipulation involves modifying it to cause unintended behavior the web developer did not intend. Cookie manipulation is possible because they are stored locally, giving you complete control. 
> This does not mean you can simply write "give me admin" in the cookie. You must understand how the webserver will interpret the cookie. 

## Method
Because cookies are encoded, they must be decoded, modified, and re-encoded in the same way to achieve successful manipulation.

An example decoded cookie:
```
{firstName:'n0ware', lastName:"s0mewhere", age:1337, eyecolor:"blue"}
```

A brief summary of cookie manipulation:
1. Obtain a cookie value
2. Decode the cookie value
3. Identify the object notation/structure
4. Change the parameters of the object to something advantageous to you, such as a higher privilege level or another user
5. Re-encode the cookie and insert it into the `value` space
6. Cause an action on the cookie, such as by refreshing the page or logging in. 

> You can also modify cookies in browser requests using tools like [BurpSuite](../../Tools,%20Binaries,%20and%20Programs/Information%20Gathering/Web%20Applications/BurpSuite.md)

