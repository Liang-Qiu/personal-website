---
title: "Linux Commands"
date: 2017-11-28
---

================

**Tee** command is used to store and view (both at the same time) the output of any other command.  
The following command (with the help of tee command) writes the output both to the screen (stdout) and to the file.
```
$ ls | tee file
```

**Du** command is used to view the disk usage.  
The following command lists the usage of current folder and sorts the result.
```
$ ds -h --max-depth=1 | sort -h
```