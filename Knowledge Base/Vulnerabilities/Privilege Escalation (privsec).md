# Privilege Escalation (privsec)
## Directory

- [Linux](#Linux)
- [Windows](#Windows)
	- [Accounts](#Accounts)
	- [Escalation-Vectors](#Escalation-Vectors)
## Description
"Privesc" refers to the act of elevating the privileges of a normal, unprivileged user to that of a privileged user, often administrative or superuser, to exploit a target machine. 

Whether for extracting information unavailable to the low privilege user or performing actions available only to a privileged user, this is a necessary skill to learn for attackers and defenders alike. 

For this reason, all accounts that can be should be low privileged, as there is no reason to make an attacker's life any easier than it should be. An example is ensuring that the standard Apache webserver user, `www-data`, has the most limited access possible, up to and including a limited shell. 

## Linux
[Top](#Directory)


## Windows
[Top](#Directory)

### Accounts
The typical accounts/groups on a Windows machine can be summarized as:
- **Domain/Enterprise Administrator** &mdash; Usually the highest account level found in an enterprise using Active Directory. Usually able to manage all accounts in an organization, control their access levels, and manage the largest amount of resources and assets within the [domain](../concepts/Domain%20(Active%20Directory.md). The domain refers to the central registry that manages all of the users, computers, and other "objects" in the domain 
- **Services** &mdash; Typically assigned to software so that it may perform the assigned tasks such as backup, antivirus scanning, etc. 
- **Domain Users**  &mdash; Accounts typically assigned to employees. They should abide by "least privilege," meaning they only have the access required to do their job. 
- **Local Accounts**  &mdash; Only available on a local system and not considered on the domain. 

The best practice is to manage these accounts in groups to better control access and privilege levels. Users can be added and removed easily as their needs change. 

### Escalation-Vectors
- **Stored Credentials** &mdash; When important credentials are stored locally and accessible by an attacker, such as in configuration files, they can lead to compromise
- **Windows Kernel Exploit** &mdash; Any unpatched vulnerability on the local system that can be abused by an attacker. 
- **Insecure File and Folder Permissions** &mdash; On occasion, for either good reasons or due to neglect, a normal user may be able to read/write sensitive files
- **Insecure Services Permissions** &mdash; Similar to insecure file/folder permissions, low privilege users may have access to services with their own permissions sets. Anything from starting/stopping services to querying system/domain information can be the result. Good for both full exploitation or chaining an exploit through incremental access.
- **DLL Hijacking** &mdash; [DLLs](../Concepts/Windows/Dynamic%20Link%20Library%20(DLL).md) or *Dynamic Link Libraries* are often used to hijack legitimate processes. In the event a DLL was deleted or otherwise not present, attackers can replace it with one of their own if they can put it where the application expects the missing one to be. The result can include privilege escalation, information disclosure, etc. 
- **Unquoted Service Path** &mdash; Paths that contain spaces and are not enclosed in quotes allow hackers to submit their own executable and hijack the path the service attempts to run. 
- **Always Install Elevated** &mdash; `MSI` packages use the Microsoft installer often for ease of use. These can be set with a policy to *AlwaysInstallElevated* that ensures the install process runs with administrator-level privileges without the need for the user to have these privileges. A malicious executable packaged as an `MSI` can therefore be installed with admin privileges. 
- **Other Software** &mdash; Third-party software introduces a wide variety of escalation vectors that can be exploited. 

### Identifying
###### Pentestmonkey has a great tool for Windows privesc available on [GitHub](https://github.com/pentestmonkey/windows-privesc-check)

Identifying privsec attack vectors can be done manually or with automated tools. 

#### Local Commands
- `net users` &mdash; Lists users on the target system
- `systeminfo | findstr /B /C: "OS Name"/C: "OS Version"` &mdash; Lists OS information for further privsec information gathering. 
- `wmic service list` &mdash; Identifies services installed on the target system
## Information Gathering
#windows #linux #privsec