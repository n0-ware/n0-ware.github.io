# Content Discovery
## Description
*Content* refers to the assets and inner workings of an application **not** designed to be accessed by external/unauthorized users.
- Files
	-  Configuration files
	-   Passwords and secrets
	-   Backups
	-   Content management systems
	-   Administrator dashboards or portals
- Folders
- Pathways

*Content Discovery* is the process of gaining access to this content through [Enumeration](../General/Enumeration.md), testing, and probing. Webservers are designed to simply serve files and folders as long as you link to or know the name of the file or folder you are looking for. There are no native protections, it is simply a directory. 

Searching for content via [Directory Busting](Directory%20Busting.md) manual [Enumeration](../General/Enumeration.md)works well for both files and folders, and searching for specific file extensions and speed of and prioritize your discovery. Common file and folder names such as `admin`, `config.txt`, `assets`, `passwords.txt`, and others are great places to start. Many of these names are available in custom wordlists. 

Beyond discovering content available outside of protections, default passwords are potentially available if the developer did not disable them. Wordlists such as [Seclists](../../../Tools,%20Binaries,%20and%20Programs/Wordlists/Seclists.md) are great for identifying these potential gaps in security. 

## Example
1. You run a blog and want to host reviews on recipes. However, you want to hide unfinished recipes not up for review yet. You hide the *admin panel* so that you are the only one that can access the core configurations of your web server, but the pages are still accessible via [Enumeration](../General/Enumeration.md) and [Directory Busting](Directory%20Busting.md).
2. A page designed to be secure calls insecure `javascript` functions that divulge information, and this function is visible by inspecting [GET Request](GET%20Request.md) and [POST Request](POST%20Request.md) requests. 
3. Discovering an [Insecure AWS S3 Bucket](../../Vulnerabilities/Insecure%20S3%20Buckets.md)

