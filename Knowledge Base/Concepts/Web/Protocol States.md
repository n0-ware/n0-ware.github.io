# Protocols - Stateful vs Stateless
A **stateless protocol** is a [communication protocol](https://en.wikipedia.org/wiki/Communication_protocol "Communication protocol") in which the receiver must not retain [session](https://en.wikipedia.org/wiki/Session_(computer_science) "Session (computer science)") state from previous requests. The sender transfers the relevant session state to the receiver in such a way that every request can be understood in isolation, that is without [reference](https://en.wikipedia.org/wiki/Reference "Reference") to session state from previous requests retained by the receiver.

In contrast, a **stateful protocol** is a communication protocol in which the receiver may retain session state from previous requests.

## Examples
An [HTTP(S)](HTTP(S).md) server interprets requests independent of each other request. 

Contrast this with an [FTP](FTP.md) server. The session is interactive, and within each session, the user is authenticated and given a set of variables (working directory, transfer mode, etc), all stored on the server as part of the session state.

#protocol #state #session