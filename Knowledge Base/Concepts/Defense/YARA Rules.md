# YARA Rules
## Description
YARA rules are like small pieces of a programming language, but instead of "doing something" like producing a program, they define rules against which various systems check for malware. These rules are included in an organization's IPS, IDS, or other detection systems actively defending against and altering to potential malware. 

These rules **define unique patterns and strings** within malware of any type that will match the suspected file against a threat group and/or malware family the original sample is attributed to. 

By developing YARA rules, **threat researchers can begin building a profile of malware**, and through several samples of the same family, even identify multiple pieces of malware from the same campaign or threat actor. 

Read more [here](https://blog.malwarebytes.com/security-world/technology/2017/09/explained-yara-rules/)


## Syntax
A basic YARA rule may look like this
```
rule my_rule
{
	meta:
		author = "n0_ware"
		description = "sample rule"
		created = "1/8/2022 00:00"
	strings
		$textstring = "/bin/sh"
		$hedstring = {2f62696e2f7368}
	conditions
		$textstring or $hexstring
}
```

A rule to detect *[EICAR](https://www.eicar.org/?page_id=3950)*  test files may look like
```
rule eicaryara {    
	meta:      
		author="n0_ware"      
		description="eicar detection string"
		created="1/8/2022 00:00"
	strings:      
		$a="X5O"      
		$b="EICAR"      
		$c="ANTIVIRUS"      
		$d="TEST"    
	condition:      
		$a and $b and $c and $d  
}
```
- **Rule** &mdash; Designates the start of a rule
- **meta** &mdash; Metadata related details not particular to how the rule functions and optional, but very valuable for understanding the hit
- **Strings** &mdash; This section details the strings you want to match within the rule, defining strings like variables
	- `$` &mdash; Defines the start of a string declaration, followed by the name we associated with it. In the example above we have `$textstring` and `$hexstring`. 
	- Text strings are legible portions of the file. Wrapped in `""`. These can also be a regex for more complex pattern matching. 
	- Hex strings are raw sequences of bytes in a file. Wrapped in `{}`.
- **Conditions** &mdash; This section defines which conditions the rule must meet to define a "hit" on a specific file. These are boolean expressions, and use the strings defined in the `strings` section as variables. Possible boolean expressions are &mdash; `and`, `or`, `not`. 
	- You must understand boolean order of operations to properly utilize these rules

## CLI
On the command line, we can run a YARA rule against a file rather simply, using the `yara` command

```
yara [options] rule_file [target]
```

When a rule is a hit, it will return with the name of the rule. Consider this example below of a test rule looking for `Hello world` in a file

![Test File Hit](Photos%20(Concepts)/YARA-Rules-Testing.png)

Adding `-m` returns the Metadata, which is why this is important.

![Metadata Returned](Photos%20(Concepts)/YARA-Rules-Testing-Meatdata.png)

Adding `-s` returns the matched strings

![Matched Strings](Photos%20(Concepts)/YARA-Rules-Testing-Matched-Strings.png)

Adding `-n` returns rules that did not match. Good for testing
### Arguments
- `-m` &mdash; Returns the metadata on the rule with a hit. 
- `-s` &mdash; Returns information on the strings that match
- `-c` &mdash; Print only matches
- `-n` &mdash; Print only non-matches
 
