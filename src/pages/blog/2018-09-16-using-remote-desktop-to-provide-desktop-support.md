---
templateKey: blog-post
title: Using Remote Desktop to provide desktop support
date: 2018-09-16T17:55:02.279Z
description: >-
  The easy way to remote desktop to a users computer without having to
  disconnect them using PSExec and the RDP Wrapper Library
tags:
  - rdp windows
---
**Requirements:**

* PSTools (in particular we need _PSExec_) - this can be downloaded from [here](https://docs.microsoft.com/en-us/sysinternals/downloads/psexec).
* RDP Wrapper Library - the latest release is available [here](https://github.com/stascorp/rdpwrap/releases) (version 1.6.2 is the latest at the time of writing).
* A Windows Firewall rule that allows your computer to remotely access the target computers over Powershell (ports 139 and 445 TCP).

**Getting started:**

1. Ensure that
