# TryHackMe - Advent of Cyber 2021 - Day 17
## Elf Leaks (Cloud)
> Edward Hartmann
> January 5, 2022

***<u>Refs/Links:</u>***
- [Advent of Cyber 2021 TOC](Advent%20of%20Cyber%20Table%20of%20Contents.md)  
-  Tags[^1]
-  Flag[^2]

[^1]: #s3 #insecuredesign #permissions #aws
[^2]: *Question 1:* `images.bestfestivalcompany.com`  
					*Question 2:* `It's easy to get your elves data when you leave it so easy to find!`  
					*Question 3:* `wp-backup.zip`  
					*Question 4:* `AKIAQI52OJVCPZXFYAOI`  
					*Question 5:* `019181489476`  
					*Question 6:* `ElfMcHR@bfc.com`  
					*Question 7:* `HR-Portal`  
					*Question 8:* `Winter2021!`  

## TOC
- [Question 1](#Question-1)
- [Question 2](#Question-2)
- [Question 3](#Question-3)
- [Question 4](#Question-4)
- [Question 5](#Question-5)
- [Question 6](#Question-6)
- [Question 7](#Question-7)
- [Question 8](#Question-8)

## Walkthrough
In this box, we are tasked with investigating how The Grinch gained access to employee personal information. We know that HR recently made available an HR portal via an [Insecure AWS S3 Bucket](../../../../Knowledge%20Base/Vulnerabilities/Insecure%20S3%20Buckets.md) and we suspect that it is the source of the leak the Grinch used for some extreme [content discovery](../../../../Knowledge%20Base/Concepts/Web/Content%20Discovery.md). 

### Question-1
[Top](#TOC)
The first question asks us to identify the website the HR team used to send out their announcement. To find the source of any image, simply right-click and choose "Copy image address." Paste the copied text anywhere to view the URL of the image. I have pasted it into the browser URL bar. 

![Finding Image Source](AoC-2021_Photos/Day_17/01_AoC_Day_17_01-05-22-Image-Source.png)

In our case, we only want the middle portion, the subdomain, domain name, and top-level domain of the URL. `example.example.xyz`. 

### Question-2
[Top](#TOC)

Now we are asked to retrieve a flag from the bucket. This assumes that the bucket is accessible from anyone, with or without the proper permissions. Let's examine the URL of an S3 Bucket resource briefly. 

![S3 URL Explained](../../../../Knowledge%20Base/Vulnerabilities/Photos%20(Vulnerabilities)/S3_URL_EXPLAINED.png)

To attempt to access an object in the same bucket as the Christmas Tree image, let's run an `aws` CLI command, replacing `flyer.pnh` with `flag.txt`. This can also be done with `curl`

```
aws s3 cp s3://images.bestfestivalcompany.com/flag.txt . --no-sign-request   
```
Or
```
curl https://s3.amazonaws.com/images.bestfestivalcompany.com/flag.txt
```

![First Flag](AoC-2021_Photos/Day_17/02_AoC_Day_17_01-06-22-Flag1.png)
### Question-3
[Top](#TOC)

To find other interesting files, we need to "list" the files in the bucket with either `aws s3 ls` or by using `curl` against the entire bucket. Let's do so now. 

```
aws s3 ls s3://images.bestfestivalcompany.com/ --no-signin-request
```
Or
```
curl https://s3.amazonaws.com/images.bestfestivalcompany.com/
```

![AWS vs Curl for List](AoC-2021_Photos/Day_17/03_AoC_Day_17_01-06-22-aws-ls-vs-curl.png)

As you can see, using the AWS CLI creates a much cleaner output than simply using `curl`. Take a look at the files we listed and identify the one that seems interesting to us. 

> Alternatively, simply navigate to the URL `https://s3.amazonaws.com/images.bestfestivalcompany.com/` in your browser and view the XML rendered on-screen.

### Question-4
[Top](#TOC)

Once you've identified the proper file, download it and unzip the file to view the contents. This can also be done with `aws s3 cp` or `wget`. We don't use `curl` on this occasion because we want to download the file, not simply return text confirming it exists. 

```
aws s3 cp s3://images.bestfestivalcompany.com/<FILE_TO_DOWNLOAD> . --no-sign-request
```
Or
```
aws s3 cp s3://images.bestfestivalcompany.com/<FILE_TO_DOWNLOAD> . --no-sign-request

```

> If you are ever on a system without `wget` but with `curl`, you can pipe the output of `curl` into another file using the *redirect* function `>`. e.g., `curl <COMMAND> > somefile.txt`

Inside this file are a huge number of folders and files. We know we are looking for an AWS Access Key. These keys are for both [Access Control](../../../../Knowledge%20Base/Concepts/Web/Access%20Control.md) and [Authentication](../../../../Knowledge%20Base/Concepts/General/Authentication.md) with AWS resources, including S3. 

Since we don't know off hand what file may contain a string we are looking for, we can start by using `cat` on all of the available files and piping the output into `grep` with the filter `AKIA` to return potential keys. 

Using `cat` in this manner will attempt to run the command on every flat file, skipping other directories, in the file we run the command from. Run the command below. 

```
cat * | grep "AKIA"
```

![Access Key Found](AoC-2021_Photos/Day_17/05_AoC_Day_17_01-06-22-Access-Key.png)

And there it is. We now have the Access Key to upload for this S3 Bucket. 

### Question-5
[Top](#TOC)

To identify the account  ID an AWS Access Key belongs to, we need to perform some basic [AWS Reconnaissance](../../../../Knowledge%20Base/Vulnerabilities/Insecure%20S3%20Buckets.md#Reconnaissance). The problem we have, however, is we need both the `access key` and `secret key` to create a profile on within the `aws` tool. To do this, we need to find the second key. 

Knowing we located the first key within this directory, it is a good assumption the second key will be there as well. Run the same `cat | grep` command as before, but replace `AKIA` with `SECRET`. 

```
cat * | grep SECRET
```

![Locating Secret Key](AoC-2021_Photos/Day_17/06_AoC_Day_17_01-06-22-Secret-Key.png)

Great, we have both pieces we need now for this task. 

> For reference, both of these files are from the `wp-config.php` file, but this requires some knowledge of WordPress ahead of time. You can locate them both with `cat wp-config.php | egrep 'SECRET|AKIA'`

![Using egrep](AoC-2021_Photos/Day_17/08_AoC_Day_17_01-06-22-Using-egrep.png)

With the two pieces we need for a profile, let's create one. Run the command below, pasting in the appropriate keys when asked and leaving the other options default. 

```
aws configure --profile HR
```

![Configure Profile](AoC-2021_Photos/Day_17/09_AoC_Day_17_01-06-22-configure-profile.png)

> For reference, `aws` stores this information in `~/.aws` in two separate configuration files
With that done, we can run our reconnaissance commands on the account. The command we want is below. Replace `AKIAEXAMPLE` with the actual access key. **The guide does not inform you that you also need to include the profile you just created in this command.**

```
aws sts get-access-key-info --access-key-id AKIAEXAMPLE --profile <PROFILE_NAME>
```

![Account ID](AoC-2021_Photos/Day_17/10_AoC_Day_17_01-06-22-Account-ID.png)

There is the Account ID for the Access Key in question. 

### Question-6
[Top](#TOC)

To identify the Username belonging to this profile we created, we need a different [reconnaissance](../../../../Knowledge%20Base/Vulnerabilities/Insecure%20S3%20Buckets.md#Reconnaissance) command. This one is more detailed and returns the information from the prior command and more, including the `Arn`, or "Amazon Resource Name" of the user. This will contain the username we want. Run the command below. 

```
aws stst get-caller-identity --profile <PROFILE_NAME>
```

![Finding the Username](AoC-2021_Photos/Day_17/11_AoC_Day_17_01-06-22-ARN-Username.png)

Let's move on. 
### Question-7
[Top](#TOC)

Let's see what other resources are available for us to access in this account. First, let's list the EC2 instances that may or may not be running. Another [reconnaissance](../../../../Knowledge%20Base/Vulnerabilities/Insecure%20S3%20Buckets.md#Reconnaissance) will do this for us. Run the command below. We pipe this into `grep` because the output can be quite long and we are just interested in tags at the moment. 

```
aws ec2 describe-instances --output text --profile HR | grep -i tags
```

![Listing Tags on EC2](AoC-2021_Photos/Day_17/12_AoC_Day_17_01-06-22-EC2-Name.png)

At the bottom, we find the name of the instance we are looking for. 
### Question-8
[Top](#TOC)

The final question tasks with finding some information contained in the [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/) service. Nearly without exception, each AWS service has corresponding `aws` commands, this is no exception. 

You can do some web research to learn how to use the command, or run `aws secretsmanager help` to get started. The command we are looking for first is `list-secrets`. Many `aws` commands have "sub-commands" that can be run with them, as we saw with `ec2 describe-instances`. Run the command below. 

```
aws secretsmanager list-secrets --profile <PROFILE_NAME>
```

![Listing Secrets](AoC-2021_Photos/Day_17/13_AoC_Day_17_01-06-22-Listing-Secrets.png)

This `JSON` can be confusing, but the information we need for this secret is the `Arn` or `Name`. You can run the help command again to discover how to get the value of the secrets, or run the command below for a shortcut using [`get-secret-value`](https://docs.aws.amazon.com/cli/latest/reference/secretsmanager/get-secret-value.html) and providing a [`secret-id`](https://docs.aws.amazon.com/cli/latest/reference/secretsmanager/get-secret-value.html#options). 

```
aws secretsmanager get-secret-value --secret-id HR-Password --profile <PROFILE_NAME>
```

Looks like Santa is playing games with us, we found a secret string, but we are in the wrong region. But we have a hint, we want a region closer to Santa. After doing some research, the closest region to the North Pole is the Europe (Stockholm) Region, named `eu-north-1`. We can add this to the command with the `--region` argument

```
aws secretsmanager get-secret-value --secret-id HR-Password --region eu-north-1 --profile <PROFILE_NAME>
```

![Final Flag](AoC-2021_Photos/Day_17/15._AoC_Day_17_01-06-22-Final-Flag.png)

There we have it. The final Flag!

***Congratulations on completing this box!***  

See you at the next one &mdash; [Advent of Cyber 3 Day 18](Day%2018%20-%20Advent%20of%20Cyber%202021.md)
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
