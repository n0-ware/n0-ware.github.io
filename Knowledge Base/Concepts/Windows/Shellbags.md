# ShellBags
## Description

Read more here &mdash; [Windows ShellBags - Part 1](https://shehackske.medium.com/windows-shellbags-part-1-9aae3cfaf17)

ShellBags can be explored using a tool by **Eric Zimmerman** available here. [Shellbags Explorer](https://ericzimmerman.github.io/#!index.md)


[^1]: https://shehackske.medium.com/windows-shellbags-part-1-9aae3cfaf17
[^2]: https://www.shehackske.com/


### What are ShellBags?[^2]
Credit To Shehacks Kenya[^1]

Microsoft Windows registry keeps track of folder settings to enhance the user experience using ShellBags. Windows ShellBags primary purpose is to improve user experience and “remember” preferences while browsing folders. Information stored in ShellBags can be critical during a forensic investigation.

Windows ShellBags were introduced into Microsoft’s operating system Windows XP, and are still present on all Windows 10 system releases. When you open, close or change viewing options of any folder on your computer, either from Windows Explorer or from the Desktop (even by right-clicking or renaming the folder), a ShellBag record is created or updated.

**Ever noticed when a user in a windows operating system modifies a folder size by e.g., resizing the window itself.** Then going back to that folder at a later date, the customization remains? That is shellbags in action!

There are many sources of digital evidence and they are divided into three major forensic categories of devices where evidence can be found: Internet-based, stand-alone computers/devices, and mobile devices. In this article, we will focus on stand-alone computers. **Digital artifacts** in digital **forensics** are pieces of data that can be used as good information when **digital** crimes occur so that they can be used as evidence for re-analysis by **forensic** teams.

Windows Shellbags artifact can be used to answer the difficult questions of data enumeration in intrusion cases, identify the contents of long-gone removable devices, and show the contents of previously mounted encrypted volumes.

### Why are ShellBags Important in Digital Forensics Investigations?[^2]
Credit To Shehacks Kenya[^1]

For any digital forensic investigator, it is crucial to note the following:

-   If any directory is mentioned in Windows ShellBags, it must have been present on the system at some point in time (even if it is not present anymore). This is valid for local filesystems including compressed archives, as well as for network locations e.g., remote mapped shares and removable devices e.g., USB flash drive.
-   As these actions and viewing preferences are tied to the user’s registry hives, we can connect specific user accounts and specific folders. Moreover, we can get information about when the folder has been last accessed from MAC timestamps contained in ShellBags.

### Where Do We Get ShellBags From?[^2]
Credit To Shehacks Kenya[^1]

It is buried deep in the system; it is a user-specific file.

Follow the path:

`C:\Users\…..\AppData\Local\Microsoft\Windows` and locate the `UsrClass.dat` file. 

**ShellBags are hidden by default, so be sure to adjust your view if you cannot find them.**

> For Windows 7 and later, shellbags are also found in the UsrClass.dat hive in the registry:
-   `HKCRLocal SettingsSoftwareMicrosoftWindowsShellBags`
-  `HKCRLocal SettingsSoftwareMicrosoftWindowsShellBagMRU`