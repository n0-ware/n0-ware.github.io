# Nmap


## Flags

### Information Discovery
- `-v, vv, vvv, vvvv, vvvvv` &mdash; Increased verbosity with each `v`
- `-PR` &mdash; ARP discovery 
- `-sn` &mdash; Performs host discovery but does not sfcan
- `-Pn` &mdash; Disables ping to check if the port is up. Slower but performs checks on all ports. 
- `-n` &mdash; Do not resolve DNS entries 
- `-A` &mdash; "Aggressive Detection Mode" runs several flags at once. `-O`, `-sV`
- `-sV` &mdash; Performs version scanning on the host 
- `-O` &mdash; Identifies the Operating System 
- `-sC` &mdash; Default safe script scan. [List](https://nmap.org/nsedoc/categories/default.html) 
	- All Nmap Scripts &mdash; [Reference](https://nmap.org/nsedoc/)


### Port Discovery
- `-p # or #-# or #,#,#,#` &mdash; Specify port(s) to scan
- `-p-` &mdash; Scan all ports (time consuming)
- `-F` &mdash; Fast port scan 
- `-` &mdash; 
- `-` &mdash; 
- `-` &mdash; 
- `-` &mdash; 
- `-` &mdash; 

### Connection Variants
- `-sS` &mdash; TCP Syn scan allows you to determine the state of the port without connecting fully to the target system. This comes in handy when you are scanning a target for open ports without revealing yourself to your test subject. Performs *syn-syn/ack* portions then does not respond with *ack*
- `-sT` &mdash; TCP Connect scan lets you detect open TCP ports. This scan method allows for a more granular approach to detecting open ports. Performs the complete *3-way handshake*
- `-sU` &mdash; UDP scan sends a UDP packet to determine what state the UDP port is in. Like a TCP scan, reveals open ports that are able to accept UDP requests.
- `-sA` &mdash; TCP `ack` scan determines if a port is stateful and/or filtered. Relates to firewalls and can give a skilled attacker deeper insight into the security appliances that are protecting a target network.


### Output
- `-oA <filename>` &mdash; Output to all formats
	- `-oN <filename>` &mdash; Normal output
	- `-oX <filename>` &mdash; XML output 
	- `-oG <filename>` &mdash; Greppable nmap
	- All these arguments support `strftime`-like conversions in the filename. 
	- `%H`, `%M`, `%S`, `%m`, `%d`, `%y`, and `%Y` are all exactly the same as in `strftime` 
	- `%T` is the same as `%H%M%S`
	- `%R` is the same as `%H%M`
	- `%D` is the same as `%m%d%y`
	- A `%` followed by any other character just yields that character (`%%` gives you a percent symbol).
	- *Example*: `-oX 'scan-%T-%D.xml'` will use an XML file with a name in the form of `scan-144840-121307.xml`.


#nmap #enumeration #networking 