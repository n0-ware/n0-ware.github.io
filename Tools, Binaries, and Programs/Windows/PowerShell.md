# PowerShell
## Description
"*Windows PowerShell is an interactive object-oriented command environment with scripting language features that utilizes small programs called "cmdlets" to simplify configuration, administration, and management of heterogeneous environments in both standalone and networked typologies by utilizing standards-based remoting protocols.*" - **Ed Wilson**

PowerShell comes baked into the Windows OS and is a very useful tool for Windows System Administrators to automate may of the day-to-day tasks they must accomplish, including manage Active Directory. PowerShell is also a favorite tool that allows adversaries to perform nerarious activities, a concept related to [living off the land](../../Post-Exploitation/Living%20off%20the%20Land%20(LOLBAS).md).

The website definition of PowerShell is &mdash; *"PowerShell is a cross-platform task automation solution made up of a command-line shell, a scripting language, and a configuration management framework. PowerShell runs on Windows, Linux, and macOS."*

John Hammond's TryHackMe Advent of Cyber 3, Day 8 Walkthrough video contains an excellent description of PowerShell, its native features, how to read a log, and more. Available [here](https://www.youtube.com/watch?v=oGX7vLtjbic). 

## Command-lets
Known as "cmdlets." Usually follow the format `Verb` + `-` + `Noun`. You can run "classic" `cmd.exe` commands on PowerShell, but the "power" lies in the `cmdlets`. 

## Logging
All PowerShell commands are logged on each workstation. These are logged into the [Windows Event Log](../../../Knowledge%20Base/Concepts/Windows/Windows%20Event%20Log.md) system.
## Transcription-Logs
PowerShell transcription logs capture the input and output of Windows PowerShell. These can be reviewed later to see what happened and when. They can be enabled by Group Policies or via configurations in the registry. 

Run this in an administrator command prompt 
```
reg add HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\PowerShell\Transcription /v EnableTranscripting /t REG_DWORD /d 0x1 /f

reg add HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\PowerShell\Transcription /v OutputDirectory /t REG_SZ /d C:/ /f

reg add HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\PowerShell\Transcription /v EnableInvocationHeader /t REG_DWORD /d 0x1 /f
```

These are plain text files that require no specific software. The names of the logs are random, but you can tell the date of the log and the order they come in via the `Date Modified` and `Date Created` attributes, as well as by timestamps or organizational standard naming conventions. 