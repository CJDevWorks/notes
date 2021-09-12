**Upon completion of this lab you will be able to**

- Configure and launch an instance in EC2
- Understand the Instance States and other critical instance information
- Generate and use a Secure Shell (SSH) public/private key pair
- Connect to a running Linux instance using an SSH client
- Extract metadata about your running instance
- Terminate an instance


====================================================

- Additional navigation options are across the top-left of the Dashboard
- Basic account information, current region, and Support options are across the top-right
- Navigation to additional EC2 resources and features are located in the left pane
- Resources section - provides a high-level summary of current EC2 resource usage
- Launch Instance section - Offers a single click to start the process of launching a new EC2 instance (you'll do that next)
- Service Health section - Simple and quick way to obtain the high-level service health in your region (or click Service Health Dashboard for a more comprehensive AWS health check)
- Additional Information - Context sensitive help on Getting Started (with EC2) or a complete listing of all AWS documentation



You can configure many different options on this page of the wizard, but it's best to keep your first launch simple. Skim the different fields, but leave the default values. If you are particularly interested in any particular field, hover over the i information icon next to it for a basic description.  The information icon is a useful feature for easing your learning curve while using the AWS Console. In many cases, the help text also includes a link to related documentation. To summarize a few key points:

- You will launch a single instance
- The Cloud Academy Lab environment has created a default VPC (Virtual Private Cloud) for you to launch your instance into
- The EC2 service will launch the instance into one of several subnets in the US West (Oregon) region

=======================================================

List all instance metadata by issuing the following command:

    curl -w "\n" http://169.254.169.254/latest/meta-data/

To extract specific metadata append key words to the end of the http path URL provided in the curl request. For example, you can easily check the list of security groups attached to the instance, its ID, the hostname, or the AMI ID. The "-w" command line option tells curl to write the output to standard output (STDOUT).

Enter the following commands to extract specific metadata associated with your running instance: 

    curl -w "\n" http://169.254.169.254/latest/meta-data/security-groups
    curl -w "\n" http://169.254.169.254/latest/meta-data/ami-id
    curl -w "\n" http://169.254.169.254/latest/meta-data/hostname
    curl -w "\n" http://169.254.169.254/latest/meta-data/instance-id
    curl -w "\n" http://169.254.169.254/latest/meta-data/instance-type

Enter the following command to get the public SSH key of the attached key pair using the public-keys metadata:

    curl -w "\n" http://169.254.169.254/latest/meta-data/public-keys/0/openssh-key


**Terminating an EC2 Instance**


AWS bills EC2 usage per second in most cases. Although the Cloud Academy lab engine will clean up this lab environment for you, it's good to learn how to stop or terminate an instance from the AWS console. When you are sure that you no longer need an instance, you can terminate it. The specific instance and the data on the root volume (system disk) is not recoverable (by default) however. So be sure you don't need it before terminating an instance. If you stop an instance, you can start it again later (and access data on all the disks). In this lab step you will terminate a running EC2 instance.

 