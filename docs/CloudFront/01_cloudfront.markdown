---
layout: default
title: Commands
parent: CloudFront
nav_order: 1
---

Below you will find useful Linux commands.
-- 

`stat -c "%a %n" filename` Shows the numeric code for the file permissions 

`stat -c "%a %n" *` A variant of above command for all files in folder

`cut -d: -f1 /etc/passwd getent passwd` - Prints users from the OS 

`systemctl | grep running` - List of running services under systemctl

`systemctl list-unit-files | grep enabled` - Similar command than above

AWK Searching command in s3 log bucket
--
Listing

```
    $ aws s3 ls s3://your-logs-bucket/2021-07-16-09
 
    2021-07-16 19:11:25        936 2021-07-16-09-11-24-5B6304EC364015C4
    2021-07-16 19:11:53        468 2021-07-16-09-11-52-DDBBDEF61B5F7439
    2021-07-16 19:11:54        468 2021-07-16-09-11-53-B5238C1820331487

    $ aws s3 ls s3://your-logs-bucket/2021-07-16-09 | awk '{print $1, $4}'

    2021-07-16 2021-07-16-09-11-24-5B6304EC364015C4
    2021-07-16 2021-07-16-09-11-52-DDBBDEF61B5F7439
    2021-07-16 2021-07-16-09-11-53-B5238C1820331487

```

Copy s3 logs list to local computer
```
    $ for log in `aws s3 ls s3://your-logs-bucket/2021-07-16-09-40 | awk '{print $4}'`; do aws s3 cp s3://your-logs-bucket/$log ./$log; done

    download: s3://your-logs-bucket/2021-07-16-09-11-24-5B6304EC364015C4 to ./2021-07-16-09-11-24-5B6304EC364015C4
    download: s3://your-logs-bucket/2021-07-16-09-11-52-DDBBDEF61B5F7439 to ./2021-07-16-09-11-52-DDBBDEF61B5F7439
    download: s3://your-logs-bucket/2021-07-16-09-11-53-B5238C1820331487 to ./2021-07-16-09-11-53-B5238C1820331487

```


```
# code block
print '3 backticks or'
print 'indent 4 spaces'
``` 



[Link button](http://example.com/){: .btn }

[Link button](http://example.com/){: .btn .btn-purple }
[Link button](http://example.com/){: .btn .btn-blue }
[Link button](http://example.com/){: .btn .btn-green }

[Link button](http://example.com/){: .btn .btn-outline }