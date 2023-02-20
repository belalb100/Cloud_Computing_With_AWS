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
![Alt text](images/nginx.png)

Just to  to Note: If you get a Connection timed out error - it is a port 22 issue. That means that your computer might have a Dynamic IP address which means it is always changing.



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

Creating a 2 tier system:

App tier deployed-available on public IP

Create 2nd tier with required dependencies - Ubuntu 18.04, mongodob installed, change mongod.conf 0.0.0.0.
Need a security group for our database - allow 27017 from anywhere - allow only from app instance
Go back to the app and create an environment variable with the database endpoint
Relaunch the app
Securing architecture with firewalls
Separate firewall to app, seperate firewall to database
App is exposed to the world, database is exposed only to app, limiting access to database




### Cloning our EC2 instance `APP` to an AMI (Amazon Maching Image):

![Alt text](images/diagram%20best.png)


First: We need to start our instance then we open gitbash as Admin to go into our ssh folder and from their we `ssh` into our ec2 app machine to make sure it is working before we clone it( we can find the `ssh` command with key pair on AWS website in our instance if we click on instance ID then click `connect` we will locate it their). So once we acces our app and we see it is working we go back to our instance on AWS we select it and then we go to `Actions` in the top right and we select `Images` and then we select create an image and we enter in our details which is name tech201 and app and MAKE SURE we enter which ports we will use as those who come after will know or even us we might come back after several months and not remember which ports we were using, the lastly we select create image at the bottom and the image is now created.





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

![Alt text](images/Hybrid,%20Public%20and%20Private.png)

### Operation expenditure vs Capital expenditure (OpEx vs CapEx).
Capital expenditure: Will need to by servers, cable, networking equipment whereas Operation expenditure allows us to forgo this and pay for what we use. Which provides companies with very high levels of flexibility. 

### Companies using it:
Many of these companies use it in a similar way, but Netflix for example uses CDN CloudFront to tell your geographic location and share content accordingly. Checks IP address. Sage maker for machine learning

### Summary:
To summarise, although there will always be a market for traditional computing, cloud computing has definitely changed the industry and the way companies approach their computing infrastructure. 




### Why use a two-tier architecture in AWS?

Scalability: The separation of the web server and database server allows each tier to be scaled independently, so you can handle more traffic by adding more web servers or increasing the database capacity.
High availability: If one tier goes down, the other tier can still operate, minimizing downtime.
Security: By separating the web server from the database server, you can implement more secure firewall rules and access controls.
When to use a two-tier architecture in AWS?


### When
When you expect high traffic or anticipate the need for scaling in the future.
When you need high availability and fault tolerance.
When you want to separate security and access controls between the front-end and back-end servers.

### Who
Who should use a two-tier architecture in AWS?

Web application developers who want to build scalable and reliable applications.
Organizations that need to meet strict uptime requirements or handle high traffic volumes.
Businesses that need to handle sensitive data and want to implement strict access controls.
How to create a two-tier architecture in AWS?

Here is a general overview of how to create a two-tier architecture in AWS:

Create an Amazon VPC to isolate your application within a virtual network.
Create an Amazon EC2 instance to host your web server and install the necessary software and dependencies.
Create an Amazon RDS instance to host your database server and configure the necessary security and access controls.
Connect the web server and database server using the appropriate networking protocols.
Test your application to ensure it's working as expected.

### How does this fit into DevOps? 
Implementing a two-tier architecture in AWS can fit into DevOps by enabling faster and more efficient application development and deployment processes. DevOps is an approach that aims to integrate development and operations teams to deliver software more rapidly and reliably.

The following are ways a two-tier architecture in AWS can fit into DevOps:

1. Automation: AWS offers various automation tools, such as AWS CloudFormation, AWS Elastic Beanstalk, and AWS CodeDeploy, that allow developers to quickly create and deploy infrastructure and applications. By automating the provisioning and deployment process, developers can focus on writing code, while operations teams can focus on maintaining the underlying infrastructure.

2. Continuous Integration and Continuous Deployment (CI/CD): A two-tier architecture can be integrated with CI/CD pipelines to automate the build, testing, and deployment process. This allows for faster and more reliable software delivery, with the ability to continuously deploy changes to the production environment.

3. Collaboration: By implementing a two-tier architecture in AWS, development and operations teams can work together more closely, with greater visibility into the infrastructure and code. This allows for better collaboration and communication, leading to faster problem-solving and improved application performance.

4. Monitoring: AWS provides a range of monitoring and logging tools, such as Amazon CloudWatch and AWS CloudTrail, that enable teams to monitor application performance, track changes, and troubleshoot issues. This can help teams quickly identify and resolve issues, leading to better application performance and reliability.

In summary, implementing a two-tier architecture in AWS can fit into DevOps by enabling automation, continuous delivery, collaboration, and monitoring. These practices can help teams deliver software more rapidly, reliably, and efficiently.

### How does this fit into agile/ SCRUM?

Implementing a two-tier architecture in AWS can fit into an Agile/Scrum methodology by enabling teams to deliver software more frequently and respond to changes more quickly. Agile/Scrum is an iterative and incremental approach to software development that emphasizes customer collaboration, flexibility, and continuous improvement.

The following are ways a two-tier architecture in AWS can fit into Agile/Scrum:

1. Iterative Development: Agile/Scrum involves iterative development, with frequent and incremental releases. A two-tier architecture in AWS allows teams to rapidly spin up new instances of web and database servers, enabling them to test and deploy new features more quickly.

2. Collaboration: Agile/Scrum emphasizes collaboration between developers, operations, and stakeholders. A two-tier architecture in AWS enables developers and operations teams to work more closely together, with greater visibility into the infrastructure and code. This can lead to better communication and problem-solving.

3. Continuous Integration and Continuous Deployment (CI/CD): Agile/Scrum requires continuous delivery of working software. A two-tier architecture in AWS can be integrated with CI/CD pipelines to automate the build, testing, and deployment process. This allows teams to rapidly deliver new features to customers.

4. Flexibility: Agile/Scrum requires teams to be flexible and adapt to changing requirements. A two-tier architecture in AWS provides the flexibility to quickly experiment and try new things. Developers can easily spin up new instances of web and database servers to test and deploy new features.

5. Retrospectives: Agile/Scrum involves frequent retrospectives to identify areas for improvement. AWS provides a range of monitoring and logging tools, such as Amazon CloudWatch and AWS CloudTrail, that enable teams to monitor application performance, track changes, and troubleshoot issues. This can help teams identify areas for improvement and implement changes more quickly.

In summary, implementing a two-tier architecture in AWS can fit into an Agile/Scrum methodology by enabling iterative development, collaboration, continuous delivery, flexibility, and retrospectives. These practices can help teams deliver software more rapidly, respond to changes more quickly, and continuously improve their processes.

### Amazon Machin Image (AMI) use case:

- We can stop an EC2 instance and also terminate it after making an AMI of it or image and start it in the exact state it was, this will save us a lot of money.

- It takes a snapshot of the EC2 instance and saves the state of the instance also saving all it's dependencies such as security groups.

- The Image will be available in the same region as the Instance.

- After completely coying the EC2 instance into an AMI and making sure it is running we can now Terminate the EC2 instance which is the same as deleting it.



### Creating an AMI (Amazon Machine Image):

First we make sure our instance is running in the AWS Cloud then we `ssh` into our `app` virtual machine. We do this by being in our `.ssh` and then using a command that is similar to this: `ssh -i "devops-tech201.pem" ubuntu@ec2-52-214-144-236.eu-west-1.compute.amazonaws.com` that we get from our AWS instance 

then we navigate to the directory with `app.js` and launch the app using `node app.js` command.

We are launching the `app` as we cannot create an image unless it is in a running state as this is how it will be saved.

then we go back to the AWS website selcet our instance `app` and on the `Actions` tab on the top right we selecet `image and templates` then select `Create Image`.

Then we name it as follows `name-group name- VE - ami`
We will use the same naming convention for our description and also add which ports we will be using as when we come back to it in the future we will remeber which ports we are using and how to use it for example `name-group-VE-ami-port 22-port 3000- ....`

then `create the instance`.

To find our instance from the AWS home page we search EC2 and click on it
On the left hand side, under `Images` then click `AMIs`
We can find our image by typing in the name in the search bar
then we select the image and click `Launch instance from AMI` also we must name it according to:
`name-group-db-ami` we enter our key which for us is `devops 201` 
then we select an existing security group and we choose our security group from previous DB, in this step we realise the practicality of naming our security groups as we know which PORTS can be USED.

We then launch the instance and it should have all previous dependecies such as; storage dependencies, security dependencies and monitoring dependencies to name a few.

Now to launch our 2 tier architecture we simply update the enviromental variable in our `app`VE and change it to the new IP of the new DB and then we follow the same steps.

- We seed the database in the app directory:
`node seeds/seed.js`
- then launch the app
`node app.js`

![Alt text](images/EC2%20to%20AMI%20final.png)


### Why use AMI's:

There are a number of reasons why an organization or individual might use AMIs in AWS:

1. Consistency: By using a pre-configured AMI, you can ensure that every instance you launch is configured in the same way.

2. Efficiency: Creating an AMI with the software and configuration you need can save you time and effort compared to manually setting up each instance.

3. Scalability: AMIs can be used to quickly and easily launch multiple instances that are identical in configuration.

4. Disaster recovery: AMIs can be used to restore your system to a known good state if there is a disaster or outage.

5. Flexibility: AMIs can be customized to meet the specific needs of your organization, and you can create multiple AMIs to support different workloads or use cases.

6. Also AMI's save the business money as they are cheaper and more cost friendly to maintain than even stopped instances.


## AWS S3 (Simple Storage Service):

Amazon S3 (Simple Storage Service) is an object storage service provided by Amazon Web Services (AWS). It is a highly scalable, reliable, and cost-effective cloud storage service that allows users to store and retrieve any amount of data from anywhere in the world.

- Benefits

Some of the key benefits of using S3 are:

Scalability: S3 can scale to handle large amounts of data, and can support a virtually unlimited number of objects.

Durability: S3 is designed to provide 99.999999999% (11 nines) durability for objects stored in it.

Accessibility: S3 can be accessed from anywhere in the world through a variety of APIs, making it an ideal choice for global applications.

Security: S3 provides a range of security features, including access control, encryption, and secure transfer protocols.


- Disaster Recover (DR)

S3 can be used in disaster recovery (DR) scenarios to provide backup and recovery of critical data. S3 can be used to store backups of data, applications, and systems, which can be easily restored in the event of a disaster. S3 can also be used to store data that is required for compliance or archival purposes.

- Use cases

Some of the best use cases for S3 include:

Storing and serving static assets for web and mobile applications.

Storing backups of critical data and systems.

Storing and serving large media files, such as images and videos.

Data archiving and compliance storage.

- Highly available

S3 is designed to be highly available by distributing data across multiple devices and facilities. When data is uploaded to S3, it is automatically replicated to multiple storage devices in different availability zones within a region.

S3 uses an object-based storage model, where data is stored in the form of objects, and each object is identified by a unique key. When a request is made to retrieve an object, S3 automatically retrieves the object from multiple storage devices and serves it to the requester. This ensures that even if one storage device or availability zone goes down, the data is still available from another device or zone.

In addition, S3 provides several other features that enhance its availability and durability, including:

Versioning: S3 allows you to enable versioning for your objects, which means that each version of an object is stored separately, allowing you to recover previous versions if needed.

Lifecycle policies: S3 allows you to define rules that automatically transition objects to different storage classes or delete them when they are no longer needed.

Cross-region replication: S3 allows you to replicate data across different regions, providing additional protection against regional outages or disasters.

Monitoring and alerting: S3 provides a range of monitoring and alerting tools that can be used to track the health and availability of your data.

- Social Media

Many social media companies use S3 for storing and serving media files, such as images and videos. For example, Netflix uses S3 to store and serve their streaming video content, and Airbnb uses S3 to store and serve their property images. Other popular social media companies, such as Pinterest and Vimeo, also use S3 for storing and serving media files.



