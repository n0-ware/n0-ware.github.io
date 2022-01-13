# Path Traversal

## Description
Path traversal involves escaping upward or drilling down from the web root to access files we should not be able to.

Most files of interest are unlikely to be located in the same directory as the web page we are on, such as `index.html`. More likely, we have to try some creative relative file references.

-   Direct file inclusion, such as `/etc/passwd`
-   Indirect references using `../` to move up a directory. Each set of `../` moves up one directory
-   We can bypass basic filtering that will strip sets of `../` by "wrapping" it in another set with `....//`. The inner set is stripped, leaving the outer set intact.
-   URL [encoding](app://obsidian.md/concepts/encoding_decoding.md) such as double encoding.

```
https://vulnsite.io/search.php?file=/etc/passwd
https://vulnsite.io/settings.php?file=../../../../../../etc/passwd
https://vulnsite.io/custom.php?file=../../../../../../etc/passwd%00 
https://vulnsite.io/admin.php?file=....//....//....//....//etc/passwd 
https://vulnsite.io/status.php?file=%252e%252e%252fetc%252fpasswd
```

> The last example here is URL double-encoded. Try it in [CyberChef!](https://gchq.github.io/CyberChef/#recipe=URL_Decode()URL_Decode()&input=JTI1MmUlMjUyZSUyNTJmZXRjJTI1MmY)

#insecuredesign #lfi #pathtraversal
