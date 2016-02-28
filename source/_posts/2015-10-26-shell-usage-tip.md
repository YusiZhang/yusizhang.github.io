---
layout: post
title: "Shell Usage Tip"
date: 2015-10-26 14:59:04 -0700
comments: true
categories: 
---

## Source env setting

When I tried to write a shell script to set some environment variables that will stay in that shell session, I found the changes I made was lost after that shell process terminated. 

For example, my proxyon.sh is like this:

```
#!/bin/sh
export http_proxy="http://myproxy.com:80"
export https_proxy=$http_proxy
export HTTP_PROXY=$http_proxy 
echo $http_proxy
```

Then in the shell terminal, instead of running ```sh proxyon.sh```, I can use ```source proxyon.sh``` to make sure all the env changes stays during the current shell session.

## Check running process

```
ps -ef
```

For example, if I want to know if weblogic server is running or not, do this.

```
ps -ef | grep java | grep wls
```

## List hidden files

```
ls -a
```

or if you install ```tree```

```
tree -a
```

## Find a file

Find by file name under the current folder.
```
find . -name "keyword"
```

## MD5 check sum
```
[ec2-user@ip-172-31-23-84 ~]$ mkdir md5test
[ec2-user@ip-172-31-23-84 ~]$ cd md5test/
[ec2-user@ip-172-31-23-84 md5test]$ ls
[ec2-user@ip-172-31-23-84 md5test]$ touch file1.txt file2.txt
[ec2-user@ip-172-31-23-84 md5test]$ ls
file1.txt  file2.txt
[ec2-user@ip-172-31-23-84 md5test]$ md5sum *.txt > md5sumtest.md5
[ec2-user@ip-172-31-23-84 md5test]$ cat md5sumtest.md5 
d41d8cd98f00b204e9800998ecf8427e  file1.txt
d41d8cd98f00b204e9800998ecf8427e  file2.txt
[ec2-user@ip-172-31-23-84 md5test]$ echo "xxxx" > file1.txt 
[ec2-user@ip-172-31-23-84 md5test]$ md5sum -c md5sumtest.md5 
file1.txt: FAILED
file2.txt: OK
md5sum: WARNING: 1 computed checksum did NOT match
[ec2-user@ip-172-31-23-84 md5test]$ cat file1.txt 
xxxx
[ec2-user@ip-172-31-23-84 md5test]$ cat /dev/null > file1.txt 
[ec2-user@ip-172-31-23-84 md5test]$ md5sum -c md5sumtest.md5 
file1.txt: OK
file2.txt: OK
```

## 



