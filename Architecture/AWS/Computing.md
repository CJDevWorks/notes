
Computing
=========================


EC2 (Elastic compute cloud)
============================

- virtual machines -(xen hiper-visor) called as instances
- They come as tier based on
        - machine, resource (cpu, memory, disk, io)
- You can launch from 1 to thousands* and they are disposable.

**Amazon machine Image** - 
Required for launching clones (instances). All EC2 instances start with AMI.
- How it does
- Bit for bit copy in root volume ie they will copy the os , application details and everything in S3.
In administrative zone. "Why administrative zone" - look storage(we should not provide access to underlying resource)

launch a new application using same image. 

Different Families for EC2 and their significance :
 - t series
 - m series
 - c series
 - r series
 - d series
 - GPU's

**Instance MetaData Service**
 - For monitoring service .. lanching it again
 - get all the data provide that into some other script.
 
**Bootstrapping with Userdata**

- self healing infrastructure
- script instance to configure itself

**Billing option**
- Billing model: On-Demand Vs Reserved instance  Vs Spot instances In terms of 
    - Commitment 
    - Hourly Prices (regardless of use so reserved instance will be charged)
    - Availability.

On-Demand -(??)

Reserved : for long running highly available application (DB)

Spot instances : temp jobs/batch processing/ -- interruptions are OK. 
record stopping point and when it restart it running from stopping point. 
  
**DEMO**
- launch a EC2
- Instance meta data service
- stopping and terminating instances

AWS Lambda
============