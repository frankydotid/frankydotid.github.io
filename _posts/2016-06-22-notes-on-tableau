---
layout: post
title: "Notes on Tableau"
date: 2016-06-22
tags: technical
---
<br/>

Notes on using Tableau (v9.3).

<br/>

**Using Cloudera Hive as Data Source**

I'm using Cloudera Hive (CDH 5.5) as my data source for testing the compatibility with Tableau. The cluster is configured with Kerberos authentication, so I need to download an ODBC driver for Clouder Hive to connect.

The version of ODBC that I used is 2.19, on Windows 64-bit. As you get the 'tgt' from Kerberos server, you can access Hive pretty seamlessly as any other data source.

Some of the things that I noticed:
- If you cancel the job in Tableau to retrieve or data related processing (using live connection), the job will still be running on you Hadoop cluster.
- It's painful to wait for the Map Reduce job to finish. 


<br/>

