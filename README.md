# Cloud_Computing_With_AWS


### Some of the basics steps to AWS

1. We must always use the the region Ireland which when using linux will be known as `eu-west-1`
2. Always keep our password private and safe and not share with anyone.

### Launching an EC2 instance and making a key pair:

### Creating a key pair:
1. Log in to AWS
2. Search ec2 and click on it
3. Click keypair
4. Generate and download the key
5. Move the key file to .ssh folder

1. We first select EC2 and create an instance.
2. we choose the name belal-tech201-app
3. Choose Ubuntu version 18.04
4. make sure we choose the correct key pair for us devops-tech201
5. Default VPC
6. Subnet Devops student 1a
7. auto assign IP: Enable.
8. Select security group option:
9. choose name belal-tech201-app
10. Secruity group rule select SSH and MY IP.
11. Secruity group rule 2 select HTTP and anywhere.
12. Security group rule 3 Custom TCP and anywhere.
13. Configure storage 8 GB is enough for us as we have little data.

### After configuring instance
`cd .ssh` this will allows us to get into our `.ssh` folder where our key pair is located 
we then use command `chmod 400 devops-tech201.pem` to make sure we have the correct permission for accessing the key 
and then `ssh -i "devops-tech201.pem" ubuntu@ec2-34-253-77-203.eu-west-1.compute.amazonaws.com` this means here is our key for the ubuntu linux machine located in eu-west on AWS.
after this we run `sudo apt-get install update` to make sure everything is updated 
and then we install nginx using`sudo apt-get install nginx`
and we should get this:
![Alt text](nginx.png)

Just to  to Note: If you get a Connection timed out error - it is a port 22 issue. That means, that your computer might have a Dynamic IP address.

![Alt text](port%2022%20error.png)

Go to your Instance`s Security.
then your Security Group.
then click edit your security group configurations: On port 22: Switch to My IP 

Should now work and you should be able to ssh in the instance through your bash terminal.

### Migrating our app folder to our EC2 Instance and running our app via the cloud:

We will do this using `scp` method which stands for secure copy it uses SSH protocol to transfer data between hosts this is the command I used

`scp -i devops-tech201.pem -r C:/Users/belal/OneDrive/Documents/Devops/tech201_virtualisation/tech201_virtualisation/environment ubuntu@ec2-34-253-77-203.eu-west-1.compute.amazonaws.com:/home/ubuntu`

It will take some time to copy everything, but after it is done use the command:

`ssh -i "devops-tech201.pem" ubuntu@ec2-34-253-77-203.eu-west-1.compute.amazonaws.com`
this will allow us to SSH into our EC2 instance.
























![Alt text](Diagram.jpg)


## Cloud Computing and it's Importance:

## What is the Cloud

Simply put, cloud computing is the delivery of computing services—including servers, storage, databases, networking, software, analytics, and intelligence—over the Internet (“the cloud”) to offer faster innovation, flexible resources, and economies of scale. You typically pay only for cloud services you use, helping you lower your operating costs, run your infrastructure more efficiently, and scale as your business needs change.

### Benefits of cloud computing
Scalability
Cost saving
Flexibility
Disaster recovery
Security

BUSINESS SIDE:
Improved productivity
Competitive advantage


### Types of Cloud Computing

The three main types of cloud service are:

Infrastructure as a Service (IaaS): Provides virtualized computing resources, such as servers, storage, and networking, that can be rented and accessed over the internet. With IaaS, users are responsible for managing and securing their own applications and data.

Platform as a Service (PaaS): Provides a platform for building and deploying software applications without the need to manage the underlying infrastructure. PaaS typically includes application development tools, databases, and middleware.

Software as a Service (SaaS): Provides access to software applications over the internet, with the infrastructure and maintenance handled by the service provider. SaaS applications are typically accessed through a web browser.

The main differences between these three types of cloud service are the level of control and responsibility that the user has over the underlying infrastructure. With IaaS, the user has the most control over the infrastructure, but also has the most responsibility for managing it. With PaaS, the user has less control over the infrastructure, but can focus more on building and deploying applications. With SaaS, the user has the least control over the infrastructure, but can simply use the software application without worrying about infrastructure or maintenance.Additionally, there are different deployment models for cloud services, including public, private, and hybrid cloud. Public cloud services are available to the general public and are owned and operated by a third-party cloud provider. Private cloud services are used by a single organization and are typically managed in-house or by a third-party service provider. Hybrid cloud services are a combination of public and private cloud, providing the benefits of both.

### Different types of cloud:

![Alt text](Hybrid,%20Public%20and%20Private.png)

### Operation expenditure vs Capital expenditure (OpEx vs CapEx).
Capital expenditure: Will need to by servers, cable, networking equipment whereas Operation expenditure allows us to forgo this and pay for what we use. Which provides companies with very high levels of flexibility. 

### Companies using it:
Many of these companies use it in a similar way, but Netflix for example uses CDN CloudFront to tell your geographic location and share content accordingly. Checks IP address. Sage maker for machine learning

### Summary:
To summarise, although there will always be a market for traditional computing, cloud computing has definitely changed the industry and the way companies approach their computing infrastructure. 
