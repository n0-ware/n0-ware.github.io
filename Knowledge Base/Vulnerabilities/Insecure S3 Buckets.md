# Insecure S3 Bucket Access
## Description
Insecure [AWS S3 Bucket](https://aws.amazon.com/s3/) Access is a common problem facing IT Departments that do not properly secure their resources, either through negligence or lack of knowledge. An S3 bucket that is made world-readable (or even writeable) can pose extraordinary risks to the organization that owns the bucket.

Assets can be hosted freely easily and very cheaply on S3, making it an attractive option for companies to use for their resources. Occasionally, IT teams will circumvent the often bureaucratic nature of corporate governance by using S3 to host assets such as PDFs and images without prior approval, such as portals for information access. 

## Identifying-Buckets
Items hosted on buckets are easy to identify through the links used to represent them on the website. The links look like this:

`http://BUCKETNAME.s3.amazonaws.com/FILENAME.ext` 
or
`http://s3.amazonaws.com/BUCKETNAME/FILENAME.ext`

## Reconnaissance
Some basic commands for recon on a bucket are below. To do this, you need to have a `profile` created with `aws configure`, meaning you need to have compromised both the `access key` and `secret access key`. 
- Match the Account ID belonging to an access key &mdash;  `aws sts get-access-key-info --access-key-id AKIAEXAMPLE --profile PROFILENAME` 
- Enumerate the Username belonging to an access key &mdash; `aws sts get-caller-identity --profile PROFILENAME`
- List all the EC2 instances running in an account &mdash; `aws ec2 describe-instances --output text --profile PROFILENAME`
- List all the EC2 instances running in an account in a different region &mdash; `aws ec2 describe-instances --output text --region us-east-1 --profile PROFILENAME`

## Bucket-Commands
If you want to list the contents of a bucket to test if it is open, you can attempt to `curl` the bucket or use `aws` CLI commands. 

Practice with a bucket the IRS makes available with all the tax filings of Tax-Exempt corporations that file 990s that is world-readable.

> The trailing argument `--no-sign-request` allows you to request the data without being an AWS customer or logging in. Authenticated users do not require this.

**List with:**
```
curl http://irs-form-990.s3.amazonaws.com/
aws s3 ls s3://irs-form-990/ --no-sign-request
```

**Download with:**
```
curl http://irs-form-990.s3.amazonaws.com/201101319349101615_public.xml
aws s3 cp s3://irs-form-990/201101319349101615_public.xml . --no-sign-request
```
> Note the `.` in the AWS command that designates that path to copy the file to. This designates the current path, but it can be another path you specify. 
## Using Credentials
If you located credentials, you can add them to your `aws` CLI configuration file:
```
aws configure --profile PROFILENAME
```
The entry is saved to `.aws/config` and `.aws/credentials`
Credentials are used with any `aws` command such as:
```
aws s3 ls --profile PROFILENAME
```
