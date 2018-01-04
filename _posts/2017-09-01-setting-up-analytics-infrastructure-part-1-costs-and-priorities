---
layout: post
title: Setting up Analytics Infrastructure Part 1: Costs and Priorities
date: 2016-07-01T00:00:00.000Z
desc: None
keywords: Data Science,EMR,Spark,Hive
categories:
  - Data Science,Spark,Hive
tags:
  - Data Science
icon: icon-phone-gap
---

Building internal analytics product.


1. Get out the early analytics wins.
 Who are your users? What kind've meaningful categories can we separate them into? Who should we focus on?
 Where do users seem to have trouble? Where are the big dropoff points?

At this point, the company is almost completely in the dark. I think this period it's absolutely pivotal, that some of
these questions get answered, at least with a rough cut.


2. Juggle insights and infrastructure.
The programmer in me leans toward focusing on infrastructure. But the reality is, your company may have quite a few different teams
and projects it is focusing on, and these projects need data. Especially if it's your intention to build a data mature company,
there's a balance between providing teams now with data, and saying no to requests so that you can focus on the longterm and so that
you can ensure careful stewardship of the data. Personally, I tend to overindulge people, and I think other analysts have the same problem.
But oftentimes people who don't work with data daily aren't able to delve into their assumptions about their project and wether or not
the data they are requesting serves their needs. Sometimes they are taking an experimentation/ AB testing mindset into problems where variables are hard to isolate and testing, at this time,
has too high of an opportunity cost.


3. Start to focus more and more on infrastructure




You can build dedicated data analytics infrastructure very, very cheaply. The hard part is selecting your technology stack
and finding someone with broad enough understanding of the business







I wanted to do a 2 to 3 part-series on some lesson learned while building a companys internal analytics product.
There is article after article about the importance of being data-driven, about how data scientists spend 80% of their
time cleaning data or on tracking, and so on and so on... Nobody seems to really provde
a general overview of how analytics gets built at a company on the engineering and distribution side. How do we answer core questions
about the business and deliver relevant and actionable insights to stakeholders in a business with multiple focuses and efforts? How do we
provide this data on a recurring basis without hiring a team of report-generating analysts?


# My Story
I have spent the last 2 years at italki, analyzing data, delivering data to other teams, and finally building the tools that
analyze and deliver data to others automatically.

# Some assumptions and a disclaimer:
We are looking at a 10-100 people sized company, a startup with a web-based product. Your company has successfully launched your product and you have users and you have data. You
have individuals or departments who desperately need data. There are core assumptions about the business that need to be analyzed and tested.

**Disclaimer**
The path forward I'm going to describe is fairly general. Most likely there are quite a few ways to build a data mature product at a young startup.

# 1. Get out the easy analytics wins.
 Who are your users? What kind've meaningful categories can we seperate them into? Who should we focus on?
 Where do users seem to have trouble? Where are the big dropoff points?

These questions can be answered roughly, but even a first cut to some of the big questions will provide enormous insight.
This early period is akin to the analytic dark-ages, and the data analysts job is to elevate the company from these dark ages.
It can be thrilling to provide insight into these questions and to provide so much value at such an early stage.

# 2. Start building out a data warehouse.
Your successes and value the data you've analyzed in step 1 will create enormous demand for your skills, especially as the team grows.


# italki Analytics Tech Stack
Our technology stack is not too different from what was



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

