**AWS**
========

AWS Global Infrastucture :
==========================

Region and availability zone

Networking and content delivery
=================================

- VPCC: Content delivery

- DNS

- Route53 : Highly scalable DNS Service

- Cloud front : Network and storage.CDN to distribute content around the world?

- DirectConnect : Dedidated line to AWS (reliable internet connection or security)

- EC2: Virtualization , docker container,

- EC2 Container Services :

- Elastic Beanstalk : (Provision all the infra based on code???).Elastic Beanstalk automatically handles the deployment, from capacity
provisioning, load balancing, auto-scaling to application health monitoring based
on the code you upload to it, where as CloudFormation is an automated
provisioning engine designed to deploy entire cloud environments via a JSON
script.

- Lambda : (+EC2 Virtual machine - Serverless upload your code and server responds based on events) : Amazon Echo/Alexa

- LightSail : Out of box Cloud

Storage:
===========

- S3: (Simple Storage Service)Object Sotage - (Metadata in their own database - dropbox)No database , application.olutions offers durable, available storage for flat files
- Glacier : Used for data archeival. You cant store immediately . Store backup

- EFS : Elastic file based service. (To store files). Can install DB

- Storage Gateway : Connect to S3

- EBS :


DB
===========

- RDS : Relation database Service, Mysql, postgress, Oracle

- DynamoDB : NoSQL - Really scalable and high performance

- RedSift : AMAZAON Warehouse. (To run report queries)

- ElasticCache : Caching your data in cloud.


Migration :
===========

- Snowball: appliance to store data : disks to further move to some other env()
SnowBall edge : Run analytics on Snowball

- DMS : Move from in-premise (other amz db) to other amazon DB.
eg: oracle(SQL,MYSQL, post-gress, SAP) ==> roar. DMS (will handle all migration)

- SMS : Server migration Services
VM in premises to - AMZ cloud (EC2)


Analytics:
==========

- Athena : SQL queries on those files

- EMR : Elastic Map Reduce : Big data- log analysic, web index, fanacial market analysis.
 Framework Hadoop, Apache spark, Apache-hbase, splunk,

- Elastic Search : Search engine for your application (alternative cloud search)
Elastic search is free software. Other alternative is angolia. This is lightenning fast.

- Kenesis: Massive data at very high rate. Sentiment analysis, social media feeds
and run real time analytics on it.

- DataPipeline : Move data from S3 to DynamoDB or vice versa. Setup DataPipeline.

- QuickSight : Visualization analytics.




Security and Identity :
=======================

- IAM : Signin /authentication - grouping , user permissioning

- Inspector - Agent on virtual machine

- Certificate Manager : free SSO cirteficate for your domain.

- Directory Service - ADS

- WAF : Application level protection (firewall for network)

- Artifacts : Security and compliance : (all docs)


Management Tools :
==================

- cloud watch : Disk utilization, CPU etc.

- **Cloud Formation** : Infrastructure into formation. Documents that describe the complet infrastuctrure.
You define complete infrastucture from a command line.
Define all components in the document.

- Cloud trail - Auditing changes to AWS environment.

- **OPSWorks** : Automate deployent using CHEF

- **Config** : Monitor and raise alert on functionality. Eg some config hat break
a email will be raise.


- Service Catalogue : whta services are allowed in organization.

- Trusted Advisor : Scan our env and recommnd, and then automated Cost optimization, performance optization, security fixes. All this is automated way of scanning ur env and giving  tips.


Application Services :
======================


- Step functions :

- SWF : Co-ordinating automated and human task

- API gateway :

- AppStream :

- Elastic Transcoder :

Developer Tools
===============

- CodeBuild

- CodeDeploy

- CodePipeline


Mobile
======

- mobile hub  : console contains - cognito

- cognito : real world application (instagram style)

- Device Farm :  testing on different device.

- Mobile analytics :

- pinpoint :  Google analytics for ur mobile app.


Business Productivity
=====================

- Workdocs

- WorkMail

- IoT : Keeping track of all the devices.


Desktop and work streaming :
============================

- WorkSpecs : Think client (actual OS runs in cloud)

- Appstream2.0


AI
===

- Alexa : Lex. previous

- Poly :  Amazon text to voice. (Echo uses it)

- Machine Learning :

- Rekognition : Image processing, facial recognition.(% recognition)

Messaging :
===========

- SNS : Simple messageing (network)

- SQS  : decouple ur application via Queue.

- SES : Simple email Services



Questions :
===========

What you know

What is an AWS region?

Which statement best describes Availability Zones?

An AWS VPC is a component of which AWS service?

Which AWS service is specifically designed to run a developer's code on an infrastructure that is automatically provisioned to host that code?

Which AWS service allows you to run code without having to worry about provisioning any underlying resources (such as virtual machines, databases, etc.)

Amazon's highly scaleable DNS service is known as ________.

Which AWS compute service is specifically designed to assist you in processing large data sets?

What is the difference between Elastic Beanstalk & CloudFormation?

Which AWS service is used a CDN to distribute content around the world?

Which of the following AWS services would be the best choice for long term data archival?

Which AWS service offers the following database engines: SQL, MySQL, MariaDB, PostgreSQL, Aurora, and Oracle?

Which of the following AWS services is used primarily for data warehousing?

Which AWS service is used for collating large amounts of data streamed from multiple sources?

You need to add users to your AWS account and set password rotation policies for these new users. Which AWS service would best fit your requirements?

You need to supply auditors with logs detailing the individual users that provision specific resources on your AWS platform. Which service would best meet this need?

You need a configuration management service that enables your system administrators to configure and operate your web applications using Chef. Which AWS service would best suit your needs?

Your digital media agency needs to convert their media files in to different formats to suit different devices. Which AWS service should you consider using to meet these needs?

 What you should review

What does an AWS Region consist of?

What is a VPC?

Which of the following AWS solutions offers durable, available storage for flat files?