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

