Security and Identity :
=======================

- IAM : Signin /authentication - grouping , user permissioning

- Inspector - Agent on virtual machine

- Certificate Manager : free SSO cirteficate for your domain.

- Directory Service - ADS

- WAF : Application level protection (firewall for network)

- Artifacts : Security and compliance : (all docs)

IAM : (Identity Access Management)
======

- user 
- group
- Roles
Policy documents applies on above 3 - (in Json)

- Its universal , it doesn't apply to region. 

- root account has complete admin acess and its created when first AWS account is created.

- New Users have NO permission.New users are provided Access Key ID and Secret Access Keys
These are not same as password, so cant be used to login through console. But these can be used via API or command line.

Setup multi-factor authentication on root account.
Create and customize the password retention policy
