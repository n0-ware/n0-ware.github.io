# TryHackMe - Advent of Cyber 2021 - Day 3
## Christmas Blackout (Web-Exploitation)
> Edward Hartmann
> December 22, 2021

<u>Refs/Links:</u>
- [Advent of Cyber 2021 TOC](Advent%20of%20Cyber%20Table%20of%20Contents.md)  
-  Tags[^1]
-  Flag[^2]

[^1]: #authentication #brokenaccesscontrol #insecuredesign #contentdiscovery #webapp 
[^2]: *Question 1:* `admin`  
					*Question 2:* `administrator`
					*Question 3:* `THM{ADM1N_AC3SS}`  

## Walkthrough
We are given a website vulnerable to enumeration to attempt directory busting and authentication brute-forcing. 

![Landing Page](AoC-2021_Photos/Day_03/1.0_AoC-Day-3_12-22-21-Landing-Page.png)

The first thing we are going to do is attempt to enumerate hidden directories to [discover hidden content](../../../../Knowledge%20Base/Concepts/Web/Content%20Discovery.md). Using [dirbuster](../../../../Tools,%20Binaries,%20and%20Programs/Information%20Gathering/Web%20Applications/dirbuster.md) and [Seclists](../../../../Tools,%20Binaries,%20and%20Programs/Wordlists/Seclists.md) is our attack path. 

```
dirb http://10.10.150.97 /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-small.txt
```

Quickly, `dirb` identifies the directory `/admin` as the admin dashboard. 

![Directory Busting](AoC-2021_Photos/Day_03/2.0_AoC-Day-3_12-22-21-dirb.png)

![Admin Dashboard](AoC-2021_Photos/Day_03/3.0_AoC-Day-3_12-22-21-Admin-Dashboard.png)

Some basic manual guessing and we can find a valid admin login using the combination `administrator:administrator`. 

![Successful Login](AoC-2021_Photos/Day_03/4.0_AoC-Day-3_12-22-21-admin-login-default-creds.png)

While inspecting the target with [BurpSuite's](../../../../Tools,%20Binaries,%20and%20Programs/Information%20Gathering/Web%20Applications/BurpSuite.md), we can also identify that when loading the `/admin` page, it also calls a `javascript` function `/admin/loginpage.js`. Investigating this script clearly gives out the administrator username and password. 

![Admin Page Calling JavaScript](AoC-2021_Photos/Day_03/5.0_AoC-Day-3_12-22-21-Admin-Calling-Javascript.png)

![JavaScript Giving Away Login Info](AoC-2021_Photos/Day_03/6.0_AoC-Day-3_12-22-21-Admin-JS-Vuln.png)

Once we are successfully authenticated, we have access to the Admin dashboard and the Flag for the box. 

![Welcome, Admin!](AoC-2021_Photos/Day_03/7.0_AoC-Day-3_12-22-21-admin-dashboard-authenticated.png)


***Congratulations on completing this box!***  

See you at the next one &mdash; [Advent of Cyber 3 Day 4](Day%2004%20%20-%20Advent%20of%20Cyber%202021.md)
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
