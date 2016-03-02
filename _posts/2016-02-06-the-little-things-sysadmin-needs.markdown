---
layout: post
title: "The Little Things The Sysadmin Needs"
date: 2016-02-06
tags: technical
---
<br/>

These are the little things that I learned when configuring my VPC. It will be updated every time I found something small new things.

<br/>

**Permanent iptables**

To setup a permanent `iptables` in CentOS 6.5, put the rules inside `/etc/sysconfig/iptables`. The rules that you set up using `iptables` command in your shell, will disappear when the machine reboots. 

You can also use `iptables-save` command, instead of `iptables`. The command will be stored at `/etc/sysconfig/iptables.save`, and be applied to `/etc/sysconfig/iptables` when the machine reboots.

<br/>

**Temporary iptables rule**

I sometimes need to open certain port temporarily to do some tasks. What I do is to insert the `iptables` rule that accepts the port that I want to access as the first rule. Never forget to delete the rule afterwards.

Inserting new rule at the beginning of the chain:

`iptables -I INPUT 1 <the rule>`

Deleting the rule:

`iptables -D INPUT <the same rule>`

<br/>

**Can I read that?**

User `alice` have a file `a.txt` under `/home/alice/`, with a permission of `744`. The `/home/alice` itself is set to `700`. Can user `bob` read `a.txt`? Of course not, silly me.

<br/>

**Timezone**

I once confused of why my blog post didn't show up on my VPC, while it was showing on the github page. It turned out that I forgot to change the time of my server. The blog post was newer than the date shown on the server. 

Changing the timezone to your local timezone:

`ln -s /usr/share/zoneinfo/<your timezone> /etc/localtime`

<br/>

**Encryption**

There are some ways to encrypt your file. One that I found when I wanted to encrypt my `tar.gz` file is from [here](http://superuser.com/questions/162624/how-to-password-protect-gzip-files-on-the-command-line), using `openssl`. You can go like this if you want to do symmetric basic encryption with AES-256:

`openssl enc -aes-256-cbc -e -in <yourfilename> -out <yourencryptedfilename>`

To decrypt it, you can do this:

`openssl -aes-256-cbc -d -in <yourencryptedfilename> -out <yourdecryptedfilename>`

There are some options for salting and choosing different encryption or hashing algorithm. A `gpg` command can be used if you prefer public/private key encryption type.

<br/>

**Verifying Tar**

In order to verify the data integrity of your backup in `tar.gz` file, [some say](http://stackoverflow.com/questions/2001709/how-to-check-if-a-unix-tar-gz-file-is-a-valid-file-without-uncompressing) that you can just run `tar -tf <yourtarfile>` to list the content. If `tar` is satisfy, then everything is just fine.

<br/>

**SNMP Trouble**

I can get a result of `snmpwalk -v1 -c public localhost system`, but when I'm using my public IP address instead of `localhost`, I get a no response error. When I ask the network team: "No rule for that, nothing will block it".

It turns out that you a self-introspection is necessary for the server itself, as for a human. Check your `hosts.allow` file, and ensure you have `snmpd: <allowed segments/ip/ALL>` in there. See [here](http://www.net-snmp.org/wiki/index.php/FAQ:Agent_30) or [here](https://access.redhat.com/discussions/1394813).

<br/>

