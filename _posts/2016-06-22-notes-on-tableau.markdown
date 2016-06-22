---
layout: post
title: "Notes on Tableau"
date: 2016-06-22
tags: technical
---
<br/>

Notes on using Tableau (v9.3).

<br/>

**Using Cloudera Hive and Cloudera Impala as Data Source**

I'm trying to connect my Tableau to Cloudera Hive (CDH 5.5) and Impala as data source for testing the compatibility with Tableau. The cluster is configured with Kerberos authentication, so I need to download an ODBC driver for Cloudera Hive to connect.

The version of Hive ODBC that I used is 2.19, on Windows 64-bit. As you get the 'tgt' from Kerberos server, you can access Hive pretty seamlessly as any other data source. Some of the things that I noticed:

* If you cancel the job in Tableau to retrieve or data related processing (using live connection), the job will still be running on you Hadoop cluster.
* It's painful to wait for the Map Reduce job to finish. 

For Impala, using ODBC version of 2.13, 2.14, and 2.15, I got an error when dragging a table to Tableau data source window: "Unsupported Impala type: 15". Searching for the problem did not yield any results. So, I jumped to version 2.29, based on an information from Tableau website about restriction to not using version 2.28. So, version 2.29 should be working, right? Yes, fortunately, it is.

And, reading from the release notes of Impala ODBC, if you are on a windows machine joined to the same domain with your Hadoop Kerberos cluster, you won't need to use MIT Kerberos, starting from version 2.14.

<br/>

