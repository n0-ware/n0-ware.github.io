# Deserialization
**Serialization** is the process of turning some object into a data format that can be restored later. People often serialize objects to save them to storage, or to send as part of communications.

**Deserialization** is the reverse of that process, taking data structured from some format, and rebuilding it into an object. Today, the most popular data format for serializing data is JSON. Before that, it was XML.

However, many programming languages offer a native capability for serializing objects. These native formats usually offer more features than JSON or XML, including customizability of the serialization process.

Unfortunately, the features of these native deserialization mechanisms can be repurposed for malicious effects when operating on untrusted data. Attacks against de-serializers have been found to allow denial-of-service, access control, and remote code execution (RCE) attacks.

> Attribution: [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/cheatsheets/Deserialization_Cheat_Sheet.html)
>
> *More information can be found at the attribution*

#deserialization #json