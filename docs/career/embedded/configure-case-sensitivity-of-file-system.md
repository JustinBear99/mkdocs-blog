---
date:
  created: 2023-11-01
  updated: 2023-11-01

tags:
  - Embedded
  - Yocto
  - BitBake

comments: true
---

# Configure Case Sensitivity of File System

## While building an image of yocto project

My build environment is created from Docker Ubuntu 22.04 on Win11 laptop. While setting up for building yocto project, I've encountered some dependency issues but those can be fixed with `apt install xxx` from the message feedback by `bitbake`. However, since the file system is provided by WSL2, aka windows OS, I still have to adjust the case sensitivity setting from the host.

```shell
build@e57acb0162c2:~/yocto/build$ bitbake imx-image-multimedia
NOTE: Bitbake server didn't start within 5 seconds, waiting for 90
WARNING: You are running bitbake under WSLv2, this works properly but you should optimize your VHDX file eventually to avoid running out of storage space
ERROR:  OE-core's config sanity checker detected a potential misconfiguration.
    Either fix the cause of this error or at your own risk disable the checker (see sanity.conf).
    Following is the list of potential problems / advisories:

    The TMPDIR (/home/build/yocto/build/tmp) can't be on a case-insensitive file system.


Summary: There was 1 WARNING message.
Summary: There was 1 ERROR message, returning a non-zero exit code.
```

## Solution

Follow the [guideline](https://learn.microsoft.com/en-us/windows/wsl/case-sensitivity) from Microsoft. We can use `PowerShell` `cd` to the build folder and command `fsutil.exe file setCaseSensitiveInfo tmp enable` to the the directory `tmp`.

Notice that the command only works for *empty* directory and the child dirs inherited the case sensitivity. So next time, we should change the sensitivity before setting up the build environment. 😂