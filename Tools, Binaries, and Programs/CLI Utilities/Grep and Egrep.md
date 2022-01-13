# Grep and Extended Grep
Grep and its cousin Extended Grep are used to match text strings to input, either from within a file or via a command piped into them. 
## Egrep
### Usage
`egrep` is used when you intend to use an "extended [regular expression](../../Knowledge%20Base/Concepts/Regular%20Expressions%20(regex).md)" beyond just a simple `string|otherstring` command via the `-E` flag with classic `grep`. It can be combined with other flags as well, and the [Regular Expressions (regex)](../../Knowledge%20Base/Concepts/Regular%20Expressions%20(regex).md) is always wrapped in single quotes, such as `'^(linux|unix)'`.

### Arguements
- `-i` &mdash' Case insensitive pattern match
- `-W` &mdash; Matches whole words
- ` ` &mdash; 
- ` ` &mdash; 
- ` ` &mdash; 
- ` ` &mdash; 
- ` ` &mdash; 
- ` ` &mdash; 
- ` ` &mdash; 


### Regex

- `.` &mdash; Matches any single character. If you want to match a dot, then you need to escape it with `\`. `'Searchin.'` returns `Searching`. `Searching.\.` will return `Searching.`
- `^` &mdash; Matches text only at the beginning of a line **if it is placed at the beginning of a regex**. For example, `^n0_ware`. Can be combined with `$`
	- If `^` is used within `[]`, it will negate the contents. For example, `fox1` will not be returned via `fox[^0-9]`.
- `$` &mdash; Matches text only at the end of a line. The syntax is `n0_ware$`. Can be combined with `^`
	- The above two commands can be used together to find an empty line via `^$`.
- `[]` &mdash; Anything contained with a bracket means it can be either character. The string `[nN]0_ware` will return both `n0_ware` and `N0_ware`. This can be used many times, such as `[nN][oO0]_[wW][aA][rR][eE]`
	- Brackets can also be used with ranges, such as `[0-9]` or `[a-zA-Z]`. Very common with IP regex and hash locating. 
	- Used singularly, will contain return all strings that contain a match to the options, such as `[aeiou]` returns all lines that have a vowel. 
	- You can also specify a characters class enclosed in `[::]` such as `[[:alnum:]]`.
	-  `[[:alnum:]]` – Alphanumeric characters.
	-   `[[:alpha:]]` – Alphabetic characters
	-   `[[:blank:]]` – Blank characters: space and tab.
	-   `[[:digit:]]` – Digits: ‘0 1 2 3 4 5 6 7 8 9’.
	-   `[[:lower:]]` – Lower-case letters: ‘a b c d e f g h i j k l m n o p q r s t u v w x y z’.
	-   `[[:space:]]` – Space characters: tab, newline, vertical tab, form feed, carriage return, and space.
	-   `[[:upper:]]` – Upper-case letters: ‘A B C D E F G H I J K L M N O P Q R S T U V W X Y Z’.
- `{#,#}` &mdash; The curly braces after a character tell grep how many times to match that character, from a minimum up to a maximum. Omitting a `#` removes the option, allowing you to specify no minimum and no maximum. For example, to match `192` you would use `[0-9]{1,3}`. 
	-  `{3}` will match items up to three times
	-  `{3,}` will match with at least 3
	-  `{1,2}` will match 1 or 2 times
- `|` &mdash; This is "or". Great for matching one of two strings, like `linux|windows`. 
- `?` &mdash; The preceding character will be matched once, at most
- `*` &mdash; Preceding character will be matched zero or more times
- `+` &mdash; Preceding character will be matched one or more times
- ` ` &mdash; 
- ` ` &mdash; 
- ` ` &mdash; 
- ` ` &mdash; 
- ` ` &mdash; 
- ` ` &mdash; 


### Examples
***IP Matching***
```
egrep '[[:digit:]]{1,3}\.[[:digit:]]{1,3}\.[[:digit:]]{1,3}\.[[:digit:]]{1,3}' file
```