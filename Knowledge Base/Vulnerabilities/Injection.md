# Inection Attacks

## Description
Injection[^1] attacks are #3 on the [*OWASP Top Ten*](https://owasp.org/www-project-top-ten/) web application vulnerabilities. 

[^1]: [OWASP Injection](https://owasp.org/Top10/A03_2021-Injection/)

In general, applications become vulnerable to injection when
- [User-Supplied Input](../Concepts/Web/User-Supplied%20Input.md) is trusted without validation, filtering, or sanitizing by the application
- An interpreter uses dynamic queries directly on non-parameterized cells without any safeguards, such as context-aware escaping
- Hostile data is used in object-relational mapping search parameters to extract additional, and often sensitive, records
- Hostile data is directly used or concatenated, such as when a SQL command contains the structure and malicious data in dynamic [Queries](../Concepts/General/Queries.md), commands, or stored procedures.

## Finding

## Examples
- [Cross-Site Scripting (XSS)](Cross-Site%20Scripting%20(XSS).md)
- [NoSQL Injection](NoSQL%20Injection.md)


## Prevention
