## Sed Usage
Good explanation &mdash; https://linuxhint.com/sed_remove_whitespace/

##### Basic Syntax
- `sed`
- `/s` &mdash; substitution expression
- `REGEXP` &mdash; regular expression to match
- `replacement` &mdash; replacement string
- `flags` &mdash; any flags to modify the command

##### Regular expressions

Some of the regular expressions we will use here are:

-   **^** matches start of the line
-   **$** matches **the end of line**
-   **+** matches one or more occurrences of the preceding character
-   **\*** matches zero or more occurrences of the preceding character.

##### Example

**_Trim the white space from a cookie:_**
```
7b 63 6f 6d 70 61 6e 79 3a 20 22 54 68 65 20 42 65 73 74 20 46 65 73 74 69 76 61 6c 20 43 6f 6d 70 61 6e 79 22 2c 20 69 73 72 65 67 69 73 74 65 72 65 64 3a 22 54 72 75 65 22 2c 20 75 73 65 72 6e 61 6d 65 3a 22 61 64 6d 69 6e 22 7d
```

**_Command chain_**
```
n0ware@hartbox- echo "7b 63 6f 6d 70 61 6e 79 3a 20 22 54 68 65 20 42 65 73 74 20 46 65 73 74 69 76 61 6c 20 43 6f 6d 70 61 6e 79 22 2c 20 69 73 72 65 67 69 73 74 65 72 65 64 3a 22 54 72 75 65 22 2c 20 75 73 65 72 6e 61 6d 65 3a 22 61 64 6d 69 6e 22 7d" > cookie.txt


n0ware@hartbox- cat cookie.txt | sed -r 's/\s+//g' > cookie_modified.txt

n0ware@hartbox- cat cookie_modified.txt
7b636f6d70616e793a2022546865204265737420466573746976616c20436f6d70616e79222c206973726567697374657265643a2254727565222c20757365726e616d653a2261646d696e227d
```

**_In this command:_**
- `-r` &mdash; says to use *regex*
- `'s/` &mdash; is a substitution. Everything between this and the next `/` is part of the string we are looking to substitute. In this case, we are using a *regex* as the "string" to substitute. 
- `\s+` &mdash; catches all *whitespace* characters. This is our regex
- `/g` &mdash; says to do this globally 

>Because there is nothing between the second and third `/`, it replaced our string identified through *regex* with nothing. 

_**If we wanted to replace with something...**_

```
n0ware@hartbox- echo "7b 63 6f 6d 70 61 6e 79 3a 20 22 54 68 65 20 42 65 73 74 20 46 65 73 74 69 76 61 6c 20 43 6f 6d 70 61 6e 79 22 2c 20 69 73 72 65 67 69 73 74 65 72 65 64 3a 22 54 72 75 65 22 2c 20 75 73 65 72 6e 61 6d 65 3a 22 61 64 6d 69 6e 22 7d" > cookie.txt


n0ware@hartbox- cat cookie.txt | sed -r 's/\s+/ banana /g' > banana_cookies.txt

n0ware@hartbox- cat banana_cookies.txt
7b banana 63 banana 6f banana 6d banana 70 banana 61 banana 6e banana 79 banana 3a banana 20 banana 22 banana 54 banana 68 banana 65 banana 20 banana 42 banana 65 banana 73 banana 74 banana 20 banana 46 banana 65 banana 73 banana 74 banana 69 banana 76 banana 61 banana 6c banana 20 banana 43 banana 6f banana 6d banana 70 banana 61 banana 6e banana 79 banana 22 banana 2c banana 20 banana 69 banana 73 banana 72 banana 65 banana 67 banana 69 banana 73 banana 74 banana 65 banana 72 banana 65 banana 64 banana 3a banana 22 banana 54 banana 72 banana 75 banana 65 banana 22 banana 2c banana 20 banana 75 banana 73 banana 65 banana 72 banana 6e banana 61 banana 6d banana 65 banana 3a banana 22 banana 61 banana 64 banana 6d banana 69 banana 6e banana 22 banana 7d
```

In this situation, everything between the second and third `/` is what we used as a replacement. 
#cli #regex #replace