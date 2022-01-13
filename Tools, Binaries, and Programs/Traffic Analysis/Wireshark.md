# Wireshark
## Description
[Manual](https://www.wireshark.org/docs/wsug_html_chunked/)

A full writeup of Wireshark is unfeasible and I will leave that to the experts. Instead, this document will serve as a writeup of useful tools and tricks I have learned using Wireshark

## Command Reference
- `==` &mdash; Equals
- `&&` &mdash; And
- `||` &mdash; Or
 - `!` or `not` &mdash Used to negate the following filter. 
	 - e.g. `!(tcp.port==3389)` or `not tcp.port==3389`
 - `matches "[regex]"` - Search within a filter using a `regex`
 - 
### Common Filters
#### HTTP
- `http.request.method == GET` &mdash; Filter only [GET Request](../../Knowledge%20Base/Concepts/Web/GET%20Request.md) requests. Same for [POST Request](../../Knowledge%20Base/Concepts/Web/POST%20Request.md) but substitute `GET` for `POST`. 
- `http.request` &mdash; Filter only `HTTP` requests
- `contains` &mdash; Used to identify if a specific filter *contains* a string, such as `http contains "www.google.com"` or `http.user_agent contains Mozilla`.
- `http.response.code` &mdash; Filtering for response codes


#### DNS
- `dns.txt` &mdash; Return only text records
- `dns.qry.type == ##` &mdash; Search for a specific type  of query **by number**. 
	- [Ref - IANA](https://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml)
- `dns.id` &mdash; Filter by a transaction ID


#### FTP
- `ftp` for user commands and `ftp-data` for data streams
## References
- Wireshark uses the [Berkley Packet Filter (BPF) Syntax](https://en.wikipedia.org/wiki/Berkeley_Packet_Filter)