# VPC

### How to create a VPC with and Internet gateway, public subnet and a route table:


So firstly we make our VPC we can do this by going to our AWS console at the top searching for VPC nd selecting the first VPC option once there we click `Create VPC` we then select `VPC only` we enter the name we would like to call it so for example `belal-tech201-VPC-Demo` we then select 
`IPv4 CIDR manual input`
we then enter our VPC CIDR block number which is `10.0.0.0/16` we keep tenancy at `default` then we click `create`.

Afterward on the left hand side tab we select `Internet gateways` we give it a name as per our naming convention, then we select `create internet gateway` 

Once our IGW is made we select it and then go to the top right where is says `Actions` and we select `Attach` and we attach it to our VPC.

Next we go to the left and select `Subnets` we then select `create subnet` we select our VPC at the first option and then we give it a clear name that it is `public` for example and we select our unique CIDR block. 


Next we go to our route table and edit our options there, so it can recieve traffic and know where to send it.  

And then we are done and now we can run an instance with this VPC while creating a new security group as our other security group was for another VPC and we should have the APP page working like this:

![Alt text](../images/Sparta_test_app.png)



### Launching a 2 tier architecture on your personal VPC, with the app and db instances on your two, separate subnets:

So once we have created a public subnet as in the task above we now go to our AWS website and from there we search for VPC at the top and select `VPC` then in the left side tool-bar `Subnet` then we select `create subnet` and for our options we select our VPC in `VPC ID` then we select a `Subnet name`using our naming convention the we select a CIDR block that is not in use the we click `Create subnet`.

We then go to the left side tab and select `Route tables` once there we select our subnet that we wish to make private. we then select `Routes` in the taskbar below we then select `Edit routes` making sure the only options available is the one shown below.

![Alt text](../images/edit%20route.png)


After this we got to our instances and select `create an instance` we choose a name as per our convention the we choose an `AMI` that has all the pre-requesites of our database which choose our `instance type` and `key pair`

we then go to `Network settings` and click `Edit` at the top right corner and select the VPC we created and it should also automatically select the private subnet we created, we `Disable` Auto assign public IP 
we then scroll down a very little and select `Select an existing security group` and we select one we had already created but if it hasn't been create we can select `Create security group` and the make sure port `3000` and `27017` are available after this we select `Create instance`

Now we make sure both our `app` and `DB` instance are running and then `ssh` in to our app instance and change our instance variable with the following command `export DB_HOST=mongodb://INSERT DB PRIVATE IP:27017/posts` then we enter the command `printenv DB_HOST` to make sure it has changed then we cd to our folder we our app.js file is located and then we enter `npm install`









### What is a VPC, how does it work and what are it's benefits to AWS cloud:

A Virtual Private Cloud (VPC) is a logically isolated virtual network in the Amazon Web Services (AWS) cloud. It allows users to create a private network within the public AWS infrastructure, which can be used to host resources such as EC2 instances, RDS databases, and other AWS services.

A VPC is created by defining a range of IP addresses, known as a CIDR block, and dividing it into subnets. Users can then create resources within these subnets, which are isolated from resources in other subnets and can communicate with each other through a VPC peering connection or VPN connection.

Some of the benefits of using a VPC in AWS cloud include:

Security: A VPC provides a secure environment by allowing users to control access to resources within the VPC through security groups and network access control lists (ACLs). Users can also use VPN connections or Direct Connect to connect their on-premises data centers to their VPC, providing an additional layer of security.

Customizability: Users have complete control over the network topology, IP address range, and subnets within the VPC, allowing them to design a network that meets their specific requirements.

Scalability: A VPC can be easily scaled by adding or removing resources within the subnets. Users can also create multiple VPCs within an AWS account, allowing them to segregate resources and manage their network architecture more efficiently.

Cost savings: By using a VPC, users can avoid the cost of setting up and maintaining their own physical network infrastructure, as well as the associated hardware and software costs.

In summary, a VPC is a powerful feature of the AWS cloud that allows users to create a private network within the public AWS infrastructure, providing them with enhanced security, customizability, scalability, and cost savings.

### Subnet

In AWS, a subnet is a logical division of a Virtual Private Cloud (VPC) that allows users to group and isolate resources based on their function or requirements. Each subnet is associated with a specific CIDR block, route table, and security group, and can be located in one of the availability zones within a given region. By using subnets, users can ensure the security and high availability of their resources, and take advantage of the scalability and fault tolerance of the AWS infrastructure.

One of the key benefits of using subnets in AWS is that it allows users to take advantage of the high availability and fault tolerance of the AWS infrastructure. By placing resources in multiple subnets within different availability zones, users can ensure that their applications remain available even if one availability zone or subnet experiences an outage.

### Private and Public Subnets in AWS:

In AWS, public and private subnets are defined based on their accessibility from the internet. A public subnet is directly accessible from the internet and typically hosts resources that need to be accessed from outside the VPC, while a private subnet is not directly accessible from the internet and typically hosts resources that should not be directly accessible from the internet. Private subnets rely on resources in a public subnet, such as a NAT instance or NAT Gateway, to access the internet. Public and private subnets are often used together in a VPC to create a secure and scalable infrastructure.


### CIDR block:

A CIDR block, which stands for Classless Inter-Domain Routing block, is a range of IP addresses that can be used to define the network address space for a VPC or subnet in AWS. 

For example, a CIDR block of 10.0.0.0/16 specifies a range of IP addresses from 10.0.0.0 to 10.0.255.255, where the first 16 bits represent the network address and the last 16 bits represent the host address.

CIDR blocks are an important aspect of network design in AWS, as they help to ensure that the IP address space is used efficiently and can accommodate the required number of resources. Users can choose from a range of CIDR block sizes when creating a VPC or subnet, depending on their requirements and the number of resources they plan to deploy.

### Internet gateway and Route table/s:


In AWS, an internet gateway is a horizontally scaled, redundant, and highly available VPC component that allows resources within a VPC to communicate with the internet. An internet gateway serves as a bridge between the VPC and the internet, and allows resources within the VPC to access the internet and be accessed from the internet.

A route table, on the other hand, is a set of rules, known as routes, that determine where network traffic is directed within a VPC. Each subnet within a VPC must be associated with a route table, which specifies the destination for traffic that is destined for different IP addresses or CIDR blocks.

To enable resources within a VPC to access the internet, users typically create a default route in the VPC route table that points to an internet gateway. This route ensures that any traffic with a destination outside of the VPC, such as traffic to the internet, is routed to the internet gateway for processing.

Users can also create custom routes in a route table to direct traffic to specific resources within the VPC, or to other VPCs or networks that are connected to the VPC via a VPN or Direct Connect.

In summary, an internet gateway in AWS is a VPC component that allows resources within the VPC to communicate with the internet, while a route table is a set of rules that determine where network traffic is directed within a VPC. To enable resources within a VPC to access the internet, users typically create a default route in the VPC route table that points to an internet gateway. Users can also create custom routes in a route table to direct traffic to specific resources within the VPC or to other VPCs or networks that are connected to the VPC.


### Example of a route table 

Let's say you have a VPC with a CIDR block of 10.0.0.0/16, and you've created two subnets within that VPC - a public subnet with a CIDR block of 10.0.1.0/24 and a private subnet with a CIDR block of 10.0.2.0/24. To allow resources within the public subnet to access the internet, you would create a route table for that subnet with the following routes:

Destination: 10.0.0.0/16 (local)
Target: local
This route ensures that traffic destined for the VPC itself is handled by the local VPC router.

Destination: 0.0.0.0/0 (default)
Target: internet gateway
This route ensures that any traffic with a destination outside of the VPC, such as traffic to the internet, is routed to the internet gateway for processing.

Now, let's say you want to create a custom route to allow resources within the public subnet to access resources within the private subnet. You would add the following route to the public subnet's route table:

Destination: 10.0.2.0/24
Target: local
This route ensures that any traffic destined for the private subnet is handled by the local VPC router and directed to the resources within the private subnet.


In this Image we have a basic example of how all these different aspects would come together. The user would connect to our website access being granted using the internet gateway and the user being routed there by our route table and they would only have access to our public subnet and not our private subnet.


![Alt text](../images/VPC-internetgateway-route.jpeg)