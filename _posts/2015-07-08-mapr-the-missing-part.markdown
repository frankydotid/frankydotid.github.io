---
layout: post
title: "MapR: The Missing Part"
date: 2015-07-08
tags: technical
---

I had been tasked with assessing Hadoop distributions for my company these past few months. We contacted the three main players in this field: Cloudera, Hortonworks, and MapR. For this purpose, I used the contact form on each website. Unfortunately, no words from Hortonworks reached us. So, we were left with two options, Cloudera and MapR.

A little bit of background on how these two distributions differ.

Cloudera was built from pure implementation of Apache Hadoop, based on Java. They integrated the different tools of the Hadoop ecosystem into one package, and distribute them as so. They also put their management software on top of it, to ease the installation and configuration of the many tools, which without it, requires you to install and configure each of the tools one by one.

On the other hand, MapR, chose to re-implement the Hadoop idea in C-slash-C++. They called the resulting implementation as MapR File System (MapR-FS), in contrast with the Hadoop File System (HDFS). The advantage that they claimed to offer is the performance boost over the Apache Hadoop implementation, NFS support, POSIX compatibility, and random read/write on the stored data. This implementation is compatible with HDFS API, hence, it can also take advantage of the tools in Hadoop ecosystem. They also implement their own NoSQL database to compete with HBase, that they called as MapR-DB, which offer better stability and performance.

Throughout the assessment and hands-on testing, we are becoming more and more convinced that MapR provides a better suit for our needs as a large enterprise. This is mainly due to the capabilities it offers that we could not find in Cloudera. This might also be caused by the presentations from MapR that were more convincing, which promoted more about the features than about how the company has the biggest market share.

The table below shows the comparison that we made, which a little bit bias towards what MapR provides. We really like the NFS support. It is very easy to copy and paste files to your Hadoop cluster. The mirroring and snapshot are also great. What is also great is that it used less number of hardware, though a little bit of higher in specification, but still cheaper. This is because these two vendors charged the license by the number of node (machine) you use. Less machine, less license, less cost. No additional stand-by Namenode or Resource Manager, which look like a waste of money.

[Comparison of MapR and Cloudera]({{ site.url }}/image/mapr-vs-cloudera.jpg)


***The Missing Part

As much as I like the capabilities that MapR provides, I still have trouble to fully endorse them. If you ever had an experience using the Cloudera Manager and then you switched to use MapR Control System (MCS), you will probably see what I mean. Cloudera Manager is a very fun administration tool. Everything seems centralized. The configuration for each service (tool), the cluster configuration, the installation of new services, management of nodes (adding/removing) and every one of them, they are all look fun and easy to do. It feels like a just the right tool to manage Hadoop cluster.

MCS? Not so fun. They provide view for each node, and what services running on them, but not a view for each service. If you want to change the configuration of the service (tool), you need to ssh into every single node and change the configuration one by one. Installing new service? No button to do that. Restarting the whole cluster? Select all the nodes and restart. Changing cluster configuration? Go to command line. They provide a way to do centralized configuration through some tricky centralized configuration directory that you can setup, but it doesn't feel like a fun thing to do.

This administration part is what I think MapR needs to improve. They need to move the much of their administration tasks from the command line to the MCS. A centralized view and configuration of services and nodes will be a nice improvement. It is a very good product, and it should promote itself more by helping the administrator to go home early and meet his family.
