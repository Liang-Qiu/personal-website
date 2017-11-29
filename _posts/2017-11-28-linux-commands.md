---
layout: post
title: "Linux Commands"
---

{{ page.title }}
================

**Tee** command is used to store and view (both at the same time) the output of any other command.  
The following command (with the help of tee command) writes the output both to the screen (stdout) and to the file.
```
$ ls | tee file
```