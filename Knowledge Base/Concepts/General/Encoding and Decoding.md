# Encoding and Decoding

## Description

Firstly, encoding **is not** encryption. It is the process of changing the format of a message into another format, generally to use a data string from one source as input for another where the original string was not in the proper format for the receiving service. On occasion, it is used for obfuscation of code. Given that it is not encryption, the information is not truly confidential. 

Encoding relies on using well-known systems to convert data into another type of data, usually to send complex data objects, such as `JSON`, through a medium that requires a specific set of *ASCII* characters, a specific data format, etc. Cookies, for example, are often encoded in `base64` to allow `JSON` notation for user credentials to pass to a browser, for example


## Types
### Base64 
These encoding schemes are commonly used when there is a need to encode binary data that needs to be stored and transferred over media that are designed to deal with ASCII.

Each digit represents exactly 6 bits of data, meaning three bytes (24 bits) can be represented by four 60bit base64 digits. 

### Rot13
Commonly referred to as a "rotation" or "Caesar" cipher, these rely on shifting the letters of the alphabet by a specified number of "rotations." Rot13 refers to 13 rotations. For example:

```
ABCDEFGHIJKMNOPQRSTUVWXYZ
```
Equals
```
NOPQRSTUVWXZABCDEFGHIJKLM
```

### URL
### XOR
"Exclusive" or (XOR) cipher uses boolean math to function. The "XOR"  function is a logical operator that returns true (1) when two values are different from another. This requires a stream of binary, where **0 is false** and **1 is true**

| A | B | Output | 
| :-: | :-: | :-: | 
| 0 | 0 | 0 | 
| 0 | 1 | 1 | 
| 1 | 0 | 1 |
| 1 | 1 | 0 | 

`XOR` encoding requires a "key", represented by a decimal number, converted into binary. 
## Tools
### CLI
#### Base64
On the CLI run, pipe information into `base64` to encode and add `-d` to decode. 
### CyberChef
This online (or local) tool is used to "bake" recipes from or to an encoding format. 
[CyberChef](https://gchq.github.io/CyberChef/)



#encoding #decoding