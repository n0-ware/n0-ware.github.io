# cut	
## Syntax:
```
<STDIN_Optional> | cut OPTION... [FILE]
```

## Arguments:
- `-d "delimiter"` &mdash; Sets a "delimiter."
- `-f (field number)` &mdash; Specifies the field to cut 
- `-b` &mdash;Extract specific bytes. Ranges specified with a `-`. A number followed by a or preceded by a `-` specifies "from # to end or from beginning to dash."" Tabs/spaces are treated as 1 byte
	- `cut -b 1,2,3 file.txt` 
	- `cut -b 1-3,5-7 file.txt`
	- `cut -b 3- file.txt` 
	- `cut -b -3 file.txt`

## Examples
Cutting MD5 hashes cleanly:
```
md5sum file.txt | cut -d " " -f 1
```
