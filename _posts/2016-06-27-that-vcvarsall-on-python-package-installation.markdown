---
layout: post
title: "That vcvarsall.bat on Python Package Installation"
date: 2016-06-27
tags: technical
---
<br/>

One of the frustating errors in installing some of python packages is the famous "Unable to find vcvarsall.bat". Fortunately, there is a wonderful explanation about the underlying problem by Steve Dower [here](https://blogs.msdn.microsoft.com/pythonengineering/2016/04/11/unable-to-find-vcvarsall-bat/).

It would be easy to do if you don't have a GPO (Windows AD group policy) that forbids you from installing from `TEMP` directory. By the best of all lucks, I have it.

After downloading the `VCForPython27.msi` file (as referenced for Python 2.7 in the link above), I found myself unable to do an installation, though I have a local administrator privilege. After diving into the Windows events log, I found the culprit: the group policy.

Few days later, I wondered if I could just use a command line installation for the `.msi` file, i.e., `msiexec`. Would it be any different? Gratefully, yes. The command line `msiexec /i VCForPython.msi` worked perfectly. But, when I tried to do a `pip` installation, the "Unable to find vcvarsall.bat" was still there. Searching for the `vcvarsall.bat` in normal `C:` path gave no results.

Going through the documentation for [msiexec](https://technet.microsoft.com/en-us/library/cc759262%28v=ws.10%29.aspx), I found that I could output the installation log to a file, in this case I log them all `/L*`. The result is very informative. The installation, by all means, went to a local temporary directory, which is odd? Perhaps, because I used a local administrator privilege while logging in using different credential.

> *That damn log is important*

So, I tried using some other options that I found by searching on Google: the `TARGETDIR`, the `INSTALLDIR`. Both didn't work. Then, being a Windows user for quite a long time, I remembered a question on a typical installation prompt asking whether I want to install for 'all users'. Apparently, there is another hidden option: `ALLUSERS=1`. It will tell `msiexec` to install for all users. The result was magnificent. The installation path was set on that `Program Files` directory. Hence, the "Unable to find vcvarsall.bat" is no more.

<br/>

