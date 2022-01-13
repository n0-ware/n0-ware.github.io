# Hashing
"Hashing" refers to the one-way cryptographic function by which a string of data is converted to a (seemingly) random string of characters of a fixed length based on the algorithm used. This is always accomplished through a cryptographic algorithm, and the resulting hash length and complexity are determined by the choice of algorithms, such as **MD5** or the **SHA** family. 

Regardless of the length of the input, a *hash* is always the same length when using a particular algorithm. The Bible and your grocery list, when hashed via **MD5**, will return the same 128-bit, 32-byte character string. The strength of hashing is in its ease of use one-way, and near impossibility the other way. For example, if you change one letter in The Bible and hash it again, the result will be different than the first. 

A lot can be said about hashing, various algorithms, their strengths, known collisions (where two values output the same hash value), and so on. 

## Example
As mentioned, any two values, when hashed with the same algorithm, output the same, fixed length. The example below is using `md5sum`, a CLI tool built into most operating systems. 

![Hashing Two Passwords](Photos%20(Concepts)/HASHING-MD5-Example.png)

## Uses
### Passwords
Passwords are typically stored *hashed* on secure, modern systems. This means that when a user inputs a password, **the actual password is never compared to an exact match of the stored password**. Instead, the password is *hashed* on input and compared to the stored *hash* on the server. This makes for excellent security, particularly when *salt* values are added to the hash, making brute-force hash attempts nearly impossible. 

### Authentication
#### Windows
Windows stores various credentials in the [SAM](General/Authentication.md#SAM) databases and uses [LSASS](General/Authentication.md#LSASS) for authentication in a variety of ways.

## Abusing
### Cracking
###### See the note on [password cracking](../../Vulnerabilities/Password%20Cracking.md) for detailed information
Cracking passwords hashes several things
- Brute forcing a list of known password hashes against a compromised hash to find a match
- Recovering a cleartext password in a situation where the hash can be matched
-
### Dumping-Hashes
The concept of "dumping hashes" refers to stealing credentials from memory, usually from a service such as [LSASS](General/Authentication.md#LSASS)