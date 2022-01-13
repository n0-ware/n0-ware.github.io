# Continuous Integration/Continuous Delivery
## Description
A crucial aspect of software development. 

**CI** &mdash; Continuous Integration is the process by which software source code is kept somewhere centralized to prevent duplicate versions of the same code while tracking revisions, changes, and versions. 
**CD** &mdash; Continuous Delivery, often the logical next step of the *CI* model where code is immediately and automatically deployed to the test, pre-production,  or production environments. Sometimes also used as the acronym for *Continuous Deployment*.

These two can be considered a set of practices that result in a continuous loop that includes the steps of software development. 

## Risks

While *CI/CD* removes many of the manual risks to the code-base itself when deploying changes and making upgrades, it does introduce a new set of risks related to the security of the update process itself. 
- Where are the keys and credentials stored? 
- Does the code-base itself leak? 
- Can an attacker gain the full source code of the application? 

A penetration tester will attempt to compromise this process and disclose information or corrupt the process. The major risks associated with *CI/CD* are
1. **Access security** &mdash; The more points of integration, the more potential points of compromise. Every integration requires managing the permissions, whether partial or full access. 
2. **Permissions** &mdash; Interconnected components require varying levels of permissions so they can interact with each other. Like integrations, these permissions must be managed. 
3. **Keys and Secrets** &mdash; Commonly used to facilitate integration, keys, secrets, passwords, etc., need to be closely protected and secured and **never** included in the code-base itself in a way that they can be leaked. 
4. **User security** &mdash; User accounts are a common attack vector, and anyone with access to the source code must have their access protected and monitored. Consider a malicious actor that installs malicious code into the final rendition of a payment processor via a compromised user...
5. **Default configuration** &mdash; Default passwords and other configurations are common on many platforms. If defaults are not changed and then used in the *CI/CD* process, complete compromise is possible. 

