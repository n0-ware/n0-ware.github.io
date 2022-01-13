# Open Source Intelligence (OSINT)

## Description
OSINT, or open-source intelligence, refers to the information (intelligence) available to the public in some way or another. OSINT is often used in conjunction with the actual process of gathering information on a target, whether as an attacker, defender, or third-party such as a government agency to develop a profile on the target(s). OSINT is both an art and a learned skill, and while there are tools and resources available, much of OSINT involves being creative, digging deep, and having the patience to complete the task with diligence and a keen eye for detail. 

The core of OSINT revolves around information available on the internet in two distinct places
- The ***Clearnet***, or the internet, on social media sites, company websites, GitHub, personal pages, etc. 
- The ***darknet***, home of the "internet underground" and only accessible through the *TOR* network or other similar software. This is where the more valuable and less available information will be found and is most used by criminals, journalists, government, whistleblowers, and other types that need to keep themselves and their information hidden. 

## OSINT Tactics
Each individual or team that conducts OSINT will develop its own methodology. 
### Models
There are many models available for OSINT and they serve as excellent repositories for learning the craft and developing your own methodology. 

#### OSINT Framework

The [OSINT Framework](https://osintframework.com/)

#### RIS OSINT 
###### Credit to [Arno Reuser](https://www.linkedin.com/in/reuser/?originalSubdomain=nl)
The RIS OSINT Data-information model" follows this approach to information gathering

![RIS OSINT Flow](Photos%20(Concepts)/RIS_OSINT_FLOW.png)

Essentially, **Intelligence** is obtained from **Information** that is obtained from **Data**. Intelligence will inevitably lead to a **Decision** that requires you to determine what to do next and **Change** accordingly. 

The RIS OSINT Roller coaster details what a potential flow may look like when acting on an objective. 

![RIS OSINT Roller Coaster](Photos%20(Concepts)/RIS_OSINT_ROLLERCOASTER.png)


### Sources
#### Accounts
In the internet age, individuals and their data are often tied to various accounts. These accounts tend to sprawl, resulting in large and poorly curated (and guarded) centers of intelligence. Locating, parsing, and identifying the useful information within a target's account is a sometimes painstaking process, but can be very useful. Facebook, Twitter, Reddit, Google, etc., are all viable sources of intelligence. Once identified, the username can be leveraged further to identify accounts of other lesser-known services such as unique forums and comment boards. 

When analyzing an account, we are often attempting to accomplish the following objectives. 

| Objective | Purpose | 
| :- | :- | 
| Real or Persona | An account can belong to either a real person by name or a persona. In either case, we want to identify the person's real name, link it to a persona, and leverage that into further information on the target | 
| Email | While harder to find openly, the email is often the key to further information gathering | 
| Linked accounts | Once the first account in the trail is found, connecting the dots to other accounts is easier and a valuable step | 
| History |  Building a "case-file" on the target is only as important as the objective, but can lead to valuable information for the objective and hint at other avenues for information via mentions, photos, etc. | 
| Information in Posts | Leveraging history, you can gain insight into the target's personal characteristics, location, other accounts, real name, etc.  | 

#### Google
Believe it or not, Google is powerful. Even more powerful than just Googling, is using Google's built-in features to hone your search. "Google-Dorking" as it is known is a valuable skill to learn, even if you never memorize all of the commands. Some of the more valuable search techniques to learn are:

| Term | Purpose | Example | 
| :- | :- | :- | 
| `+` or `-` | Ensuring the result contains/does not contain the specific term | +"username" or -"green bay" | 
| site: | Guarantees the results from from a specific website only. Can be used with wildcards. | site:\*.microsoft.com or site:facebook.com | 
| filetype | Searches for a specific filetype only | filetype:"txt" or filetype:"csv" | 
| link | Searches for external links to other pages | link:"cooking" | 
| inurl | Seraches for a URL that matches one or more keywords | inurl:"hacking" | 
| before/after | References a date range to search within | (before:2010-01-02) and/or (after:2021-01-01) | 

Don't forget that Google can translate as well! [Google Translate](https://translate.google.com/)

#### Blocktrail
###### Stub
Blockchain allows for us to easily identify linking characteristics, but is harder to link those traits to an individual. Various tools exist for helping with OSINT on the blockchain, such as:
- [Blocktrail](https://btc.com/)
- [Bitcoin Who's Who](https://www.bitcoinwhoswho.com/)
- [Graphsense](https://graphsense.info/)
- [Block Explorer](https://blockexplorer.com/)

#### GitHub
On GitHub, once a piece of code is added, it is retained forever in the "commits" section of the repositories history. Even if that code is later deleted and re-committed, the original passwords and other sensitive information that may have been contained in the commit is retained in the history, even if it is no longer visible in the source code. 

#osint