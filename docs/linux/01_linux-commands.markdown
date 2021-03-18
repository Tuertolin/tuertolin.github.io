---
layout: default
title: Commands
parent: Linux
nav_order: 1
---

Below you will find useful Linux commands.
-- 

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

[Link button](http://example.com/){: .btn }

[Link button](http://example.com/){: .btn .btn-purple }
[Link button](http://example.com/){: .btn .btn-blue }
[Link button](http://example.com/){: .btn .btn-green }

[Link button](http://example.com/){: .btn .btn-outline }