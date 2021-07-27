---
layout: default
title: Jekyll autodeploy to AWS
parent: Deployment
nav_order: 1
---

Jekyll autodeploy to AWS - By using GitHub --> CodePipeline --> CodeBuild --> s3 bucket --> CodeCloudfront.
-- 

This is the architecture that I'm using to automate this website. I have my code stored in GitHub repository. Every time that I update my GitHub repository, AWS CodePipeline will execute a conteiner in CodeBuild to deploy this code into an s3 bucket by using Jekyll. From there, the content will be serve via CloudFront.

![Jekyll autodeploy to AWS architecture](/docs/docs_assets/deployment/Jekyll-autodeploy-to-AWS.jpg)


In total, we will use the following AWS services to host and automate the deployment of our website. These are:
- Route53
- CloudFront 
- S3
- CodePipeline
- CodeBuild 

All these services are managed by AWS. This basically means that you don’t have to worry about servers or capacity. This is all handled by AWS. 

s3 Bucket - Static website hosting configuration
--

1.Create an s3 bucket by following this instruccions [Creating a bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/create-bucket-overview.html)
Remember that the bucket name needs to be a DNS-compliant name.
2.Configure your bucket as an Static Website hosting. By going to your bucket, select Properties tab and then select Static Website hosting.
    - Static website hosting: Enabled
    - Hosting type: Host a static website
    - Index document: index.html 

After enabling the s3 static website hosting, please asve the Bucket website endpoint, we will need it later for configuring your CloudFront ditribution. When you configure your bucket as a static website, the website is available at the AWS Region-specific website endpoint of the bucket. For example:
http://yourbucketname.s3-website-ap-southeast-2.amazonaws.com

![S3 Static Website hosting](/docs/docs_assets/deployment/Jekyll-autodeploy-to-AWS_02.jpg)

3.On top of that, we will need to make our bucket public for our consumers to access content at the website endpoint. For this purpose, we will need to edit the S3 Block Public Access settings for the bucket. 
    - Choose the name of the bucket that you have configured as a static website.
    - Choose Permissions.
    - Under Block public access (bucket settings), choose Edit.
    - Clear Block all public access, and choose Save changes. 

![S3 Block Public Access](https://docs.aws.amazon.com/AmazonS3/latest/userguide/images/edit-public-access-clear.png)

4.Last but not least, we need to edit our bucket policy to allow everyone to "GetObject" from our bucket:
    - Under Buckets, choose the name of your bucket.
    - Choose Permissions.
    - Under Bucket Policy, choose Edit.
    - To grant public read access for your website, copy the following bucket policy, and paste it in the Bucket policy editor

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::Bucket-Name/*"
            ]
        }
    ]
}
```

With that, your bucket now has public access. If you copy any index.html file into the root of your bucket, you will be able to browse it when you hit your website bucket endpoing (The one that you copied on step 2).
Just for testing purpose, create an index.html file by using any text editor, and then upload the file into your s3 bucket.

```
<!doctype html>
<html>
  <head>
    <title>This is the title of the webpage!</title>
  </head>
  <body>
    <p>This is an example paragraph. Anything in the <strong>body</strong> tag will appear on the page, just like this <strong>p</strong> tag and its contents.</p>
  </body>
</html>
```

You should be able to browse it as the below image:

![s3 bucket with host static website](/docs/docs_assets/deployment/Jekyll-autodeploy-to-AWS_03.jpg)





`stat -c "%a %n" filename` Shows the numeric code for the file permissions 

`stat -c "%a %n" *` A variant of above command for all files in folder

`cut -d: -f1 /etc/passwd getent passwd` - Prints users from the OS 

`systemctl | grep running` - List of running services under systemctl

`systemctl list-unit-files | grep enabled` - Similar command than above


```
# code block
print '3 backticks or'
print 'indent 4 spaces'
``` 

