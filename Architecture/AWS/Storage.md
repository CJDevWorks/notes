Storage in AWS :
=================

1. Instance Store - EC2 - (few GB to Tera byte)
2. BlockStore - EBS
3. ObjectStore - very cheap/durable/S3/all operation using https/write once read many
4. Cold Store - Archival Storage /transition from S3/slow retirval

5. AWS storage gateway : Service connects on premise appliance with cloud based storage
    - File based
    - Volume based
    - Tape based

Object storage vs block storage:
---------------------------------
- if you want to change a bit/part of data then u can do it in BLKS but in OBJ_S you have to update whole document
- OBJ_S uses https/http for operation whereas BLK_S uses optimized APIs.
- BLK_S is more efficient. 
- RandomIO is for block storage
- OBJ_S cant be mounter(it provides illusion)
- S3 is good for DB backup but not DB operation.

Manage Storage CLass :
        Standard
        Standard_IA
        Glacier

eg: logs in S3. After 7 days they transition to glacier 
and permanently deleting it after 7 years.

S3
====== 

- all operation using https. write once read many
- pay by use .
- No limit on size of bucket (which is unique- globally)
- individual file size 5TB
- put request has 5GB limit. So we have multipart upload
- Encryption
- Fault taulrent and high availibility : - across availibility zone - so we have durability due to los of data centre.
- No file system . only bucket and objetc - url- htttps://<availibility>.amazonaws.com/mybucket/object 
- (Simple Storage Service)Object Sotage - (Metadata in their own database - dropbox)No database , application.olutions offers durable, available storage for flat files

*DEMO*  TODO:
Q. create S3.
    - bucket / object  
 
 Provide :
    - permission (IAM), user, group etc.., account
    - 
 - create a bucket policy for public read (static assets in S3 for web app- reducing load on AWS)
 - Add life cycle rule    
    
Glacier
==============

- Used for data archival. Store backup/Vaults/Archives (like compliance requirement)
- Cheapest
- Write once read rarely. 
     - Backup of S3.
     - Direct upload
- Download via retrieval request (You cant re-store immediately .)
    *   3-5 hour wait
    *  $0.5/1000 pulls
 

Instance storage : EC2 
======================
 - build/free-cost with machine/
 - high degree IO
 - Ephemeral-non persistent
 - No Snapshot  
 - what are different tiers :
    t1/t2/m4, c4 -- have no store volume 
    m3 medioum, m3.large, m3.xlarge, d2.8xlarge, hi1.4xlarge??


EBS :
=======
  - Independent from machine (EC2+EBS)
  - $@GB@month 
  - Up to 16 TB/Durable - but per avalibility zone/
  - Exits in single (same AZ as EC2) AZ
  - Snapshot provided.
  - Encryption.
  - Connected over network (but it's not NAS).
  - Can be encrypted.
  - Can be used in RAID(?) or Logical volume manager(LVM?)

Options:
- compare SDD and HDD IOps/Storage/throughput.
  
  **DEMO**
  - create a EBS volume
  - Mounting a EBS olume linux/windows
  - creating a Snapshot
  
- EFS : Elastic file based service. (To store files). Can install DB
- Storage Gateway : Connect to S3


EBS Snapshot
==============
 - to S2 durability of upto two AZs
 - should be store admin zone (where people have only read only or see it as resource).
 - Easily copied to other region and can be shared(between accounts).
 - First snapshot is full backup then subsequents are delta. (but how they will be stored in a object store??)
 
  
S3 Snapshot
===============


Glacier data retrival
========================

