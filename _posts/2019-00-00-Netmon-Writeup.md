---
layout: post
title: Netmon Write-up
---

So in honour of the first official write-up on this blog I find it fitting that I do it on my first ever box on HackTheBox.eu.

(Side note: If you havent already, I highly suggest signing up to HackTheBox.eu, It's a fantastic service for newbie pentesters)

Alright, lets get to it.

First thing first, lets run an nmap scan to find out what we're working with.

Nmap scan report for 10.10.10.15.

Host is up (0.049s latency).

Not shown: 995 closed ports

PORT    STATE SERVICE      VERSION

21/tcp  open  ftp          Microsoft ftpd

80/tcp  open  http         Indy httpd 18.1.37.13946 (Paessler PRTG bandwidth monitor)

135/tcp open  msrpc        Microsoft Windows RPC

139/tcp open  netbios-ssn  Microsoft Windows netbios-ssn

445/tcp open  microsoft-ds Microsoft Windows Server 2008 R2 - 2012 microsoft-ds

Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Okay, now we have something, so this is a Windows machine running a webserver on port 80 and an ftp service on port 21. We're not too concerned with the other stuff

So lets have a look at that webserver then...

![Netmon Homepage](https://raw.githubusercontent.com/WitSecGroup/WitSecGroup.github.io/master/images/Netmon_Homepage.png)

Well there's a log-in section right there so lets try and get some creds later. For now, let's go back and look at that ftp service.
Since we don't have any credentials right now, lets try an anonymous log in...

Connected to 10.10.10.152.
220 Microsoft FTP Service
Name (10.10.10.152:root): anonymous
331 Anonymous access allowed, send identity (e-mail name) as password.
Password:
230 User logged in.
Remote system type is Windows_NT.
ftp> 

Success! Alright, lets have a look at all the files with an "ls -a" command to show all files including hidden files.

11-20-16  10:46PM       <DIR>          $RECYCLE.BIN
02-03-19  12:18AM                 1024 .rnd
11-20-16  09:59PM               389408 bootmgr
07-16-16  09:10AM                    1 BOOTNXT
02-03-19  08:05AM       <DIR>          Documents and Settings
06-13-19  03:50PM                   74 hash.txt
02-25-19  10:15PM       <DIR>          inetpub
06-13-19  03:45PM            738197504 pagefile.sys
07-16-16  09:18AM       <DIR>          PerfLogs
02-25-19  10:56PM       <DIR>          Program Files
02-03-19  12:28AM       <DIR>          Program Files (x86)
02-25-19  10:56PM       <DIR>          ProgramData
02-03-19  08:05AM       <DIR>          Recovery
02-03-19  08:04AM       <DIR>          System Volume Information
02-03-19  08:08AM       <DIR>          Users
02-25-19  11:49PM       <DIR>          Windows

Changing our directory to Users we can see a Public user and an Administrator, we dont yet have access to the Admin account so lets check out Public

02-03-19  08:05AM       <DIR>          Documents
07-16-16  09:18AM       <DIR>          Downloads
02-03-19  12:35AM                   33 lel.txt
07-16-16  09:18AM       <DIR>          Music
07-16-16  09:18AM       <DIR>          Pictures
02-03-19  12:35AM                   33 user.txt
07-16-16  09:18AM       <DIR>          Videos


And there it is! Our first flag, user.txt.

Searching around a little more will lead us to some back up files comtaining a username and password for admin access

