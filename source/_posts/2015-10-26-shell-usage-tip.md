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





