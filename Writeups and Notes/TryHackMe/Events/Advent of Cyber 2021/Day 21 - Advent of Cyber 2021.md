# TryHackMe - Advent of Cyber 2021 - Day 21
## Needs in Computer Stacks (Blue Teaming)
> Edward Hartmann
> January 8, 2021

***<u>Refs/Links:</u>***
- [Advent of Cyber 2021 TOC](Advent%20of%20Cyber%20Table%20of%20Contents.md)  
-  Tags[^1]
-  Flag[^2]

[^1]: #blue #yara #ir #detection
[^2]: *Question 1:* ` `  
					*Question 2:* ` `  
					*Question 3:* ` `  
					*Question 4:* ` `  

## TOC
- [Question 1](#Question-1)
- [Question 2](#Question-2)
- [Question 3](#Question-3)
- [Question 4](#Question-4)

## Walkthrough
In this scenario, we are tasked with using [YARA rules](../../../../Knowledge%20Base/Concepts/Defense/YARA%20Rules.md) to automate some detection tools against ongoing attacks against. We are provided some sample files and instructions on how to create YARA rules.

> This lab takes place on the attack box, but the `YARA` command is easily installed with `sudo apt install yara` and you may copy the contents of the `testfile.txt` onto your system if you choose to do so. 

This box is more of "how to use YARA" than anything and has rather simple tasks. Considering writing some rules yourself against test files like I have done in my description of [YARA rules](../../../../Knowledge%20Base/Concepts/Defense/YARA%20Rules.md) and you will learn a lot more!

My simple test rule is:
```
rule hitrule   {
        meta:
                author="n0_ware"
                description="Sample rule for testing"
                created="1/8/2022 00:00"
        strings:
                $a="Hello"
                $b="worlds"
        condition:
                $a and $b
}
```

And my tile is `testfile.txt`:
```
Hello world
```

**Basic**
![Test File Hit](../../../../Knowledge%20Base/Concepts/Photos%20(Concepts)/YARA-Rules-Testing.png)

**Metadata Returned**
![Metadata Returned](../../../../Knowledge%20Base/Concepts/Photos%20(Concepts)/YARA-Rules-Testing-Meatdata.png)

**Strings Matched**
![Matched Strings](../../../../Knowledge%20Base/Concepts/Photos%20(Concepts)/YARA-Rules-Testing-Matched-Strings.png)

### Question-1
[Top](#TOC)

Read the guide provided to your, mine, or THMs, and consider the correct boolean operator, if it cannot be either `and` or `not`, which can it be?

### Question-2
[Top](#TOC)

The metadata is a valuable portion of the YARA rule. Read the guide, and find out which [YARA flag](../../../../Knowledge%20Base/Concepts/Defense/YARA%20Rules.md#Arguments) you need for this 

### Question-3
[Top](#TOC)

More arguments! Do some searching to find out which flag you need to "**negate**", aka, return only rules that did not match. 

### Question-4
[Top](#TOC)

Finally, we are told to make some modifications to our `eicaryara`	 rule used during the walkthrough. This change will make it so that the rule no longer hits (try it with the flag that is the answer to the previous question). Note the output (without the flag from the previous question) and provide your answer.

***Congratulations on completing this box!***  

See you at the next one &mdash; [Advent of Cyber 3 Day X](AoC-2021_DayXX.md)
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
