---
layout: post
title: "Notes on Tableau"
date: 2016-06-22
tags: technical
---
<br/>

Notes on using Tableau Desktop (v9.3) - no server.

<br/>

**Live and Extract Mode**

When connecting to a data source, you can choose between Live or Extract mode. The Live mode will make Tableau to query the database for any changes related to the data you want to view. Use this if your database is super fast. 

While the Extract mode will tell Tableau to download the data as tableau extract file (.tde) to you machine, and load it into you local memory. Use this if your database performance is slowly killing your patience. Please note that your local machine needs to have enough memory and processing power. 

The extract mode will require you to distribute your tableau workbook (.twb) with the data extract (.tde). You can use tableau packaged workbook (.twbx) to make them into one file. If you use a large dataset, the resulting .twbx file will not be so appealing to be transferred as a report. (~100 MB for a couple of charts? Damn...)

<br/>

**Using Cloudera Hive and Cloudera Impala as Data Source**

I'm trying to connect my Tableau to Cloudera Hive (CDH 5.5) and Impala as data source for testing the compatibility with Tableau. The cluster is configured with Kerberos authentication, so I need to download an ODBC driver for Cloudera Hive to connect.

The version of Hive ODBC that I used is 2.19, on Windows 64-bit. As you get the 'tgt' from Kerberos server, you can access Hive pretty seamlessly as any other data source. Some of the things that I noticed:

* If you cancel the job in Tableau to retrieve or data related processing (using live connection), the job will still be running on you Hadoop cluster.
* It's painful to wait for the Map Reduce job to finish. 
* Use 'Extract' mode if you are to do analysis by dragging and dropping measures and dimensions multiple times, unless your Hive run on Spark

For Impala, using ODBC version of 2.13, 2.14, and 2.15, I got an error when dragging a table to Tableau data source window: "Unsupported Impala type: 15". Searching for the problem did not yield any results. So, I jumped to version 2.29, based on an information from Tableau website about restriction to not using version 2.28. So, version 2.29 should be working, right? Yes, fortunately, it is.

And, reading from the release notes of Impala ODBC, if you are on a windows machine joined to the same domain with your Hadoop Kerberos cluster, you won't need to use MIT Kerberos, starting from version 2.14.

<br/>

**Error "Online map could not be loaded"**

Check your Tableau Desktop logs at '~\Documents\My Tableau Repository\Logs'. In my case, the error is caused by 'Internet communication error: SSL connect error'. The problem, I suppose, is because the local machine cannot verify the SSL/TLS Certificate provided by tableau maps provider.

My solution was to open one of the link that Tableau tried to access in Internet Explorer, so that the SSL/TLS Certificate can be recognized, e.g., open 'https://maps.tableausofware.com'. 


