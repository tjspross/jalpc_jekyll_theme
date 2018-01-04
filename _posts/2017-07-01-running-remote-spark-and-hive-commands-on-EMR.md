---
layout: post
title: Running Remote Hive, Sqoop or Spark Commands on EMR
date: 2016-07-01T00:00:00.000Z
desc: Why your startup should not use Google Analytics for Product Analysis
keywords: Data Science,EMR,Spark,Hive
categories:
  - Data Science,Spark,Hive
tags:
  - Data Science
icon: icon-phone-gap
---

AWS provides pretty thorough documentation on all of its products, but in some cases there is still a huge knowledge gap
AWS generally provides pretty thorough documentation for all of it's products. When it came to building our data pipeline, information 
on the web about about how to actually run Hive and Spark jobs through EMR was extremely lacking, and experimenting and debugging new 
ways to submit jobs to clusters was a huge headache.

Since our tasks ran daily or weekly and we weren't using Hadoop as our data warehouse, the idea was that one task would start up our cluster, 
several tasks would complete whatever data-cleaning operation, and the final task would finally shutdown the cluster. This would happen 
daily and take under an hour.

# Requirements
We have the remote cluster and the local server. In the case that we are developing, the local server is our local machine. When these
jobs are ready for production, they can be moved to a remote server that handles scheduling of our ETL tasks. This scheduling server
will be tasked with communicating with the remote cluster it creates.

Note that I have a very, very strong preference for writing data-cleaning tasks in SQL when possible. SQL code is easy to read and understand
and SQL is skill shared by pretty much all data scientists.


With that in mind, I had the following requirements for any method for submitting remote Hive, Spark or Sqoop jobs.
1. I want to see stdout and stderr in my console when developing.
2. SQL queries should run remotely the same as if I ran them directly in Hive or Spark Shell. I want to be able to copy-paste production 
SQL code into a shell when debugging or when adding features - no need to escape or double-escape regular expression strings.
3. If I changed code locally, it needs to be reflected in whatever code/files run remotely. This wasn't really hard to solve, it just 
required creating files with unique timestamps on the remote server. Another solution was uploading local files at runtime to S3 and 
overwriting its predecessor.

In certain cases, my Spark SQL code ran faster than the same operation written using the (py)Spark DataFrame API.

# Use UNIX Commands and SSH

AWS documentation emphasizes submitting steps to EMR through their Add Steps API. Very few workflow engines (Airflow, Luigi) run commands 
this way for a reason. There's no huge advantage to doing it through AWS CLI or boto3 and I personally find the AWS CLI command clunky.
```
aws emr add-steps --cluster-id <Your EMR cluster id> --steps Type=spark,Name=Spark,Args=[--deploy-mode,cluster,--master,yarn,s3://your-bucket/script.py,s3://your-bucket/input.csv,s3://your-bucket/output/],ActionOnFailure=CONTINUE
```

Additionally, This method deposits stdout and stderr of the command to S3 instead of your terminal and it's a bit inconvenient when
developing. I would NOT recommend using Amazon EMRs Add Step functionality.

It is much much simpler to just stick to good old UNIX commands. There's some nuance in how to run these commands depending on the 
application you are running (Hive, Spark or Sqoop) which I will go into below. But this is really just the simplest way.

# Hive
Hive allows you to run quoted query commands. i.e:

```
hadoop@xx-xx-xxxx home> hive -e 'select * from user'
````

This is nice, but allows

