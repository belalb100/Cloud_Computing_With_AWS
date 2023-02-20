## Creating and S3 Bucket:

First we go onto the AWS Website then we select `Amazon EC2` then we select `Launch Instance` we give our bucket a name using `name-group-s3` model, we then select `Ubuntu version 18` then we select `instance type` then next we choose our `key pair` then in the `Network settings` we select `Allow SSH traffic from` and `Allow HTTP traffic from the internet` we then select edit to make sure we have SSH Oon port 22 and HTTP on port 80. 
We check every is correct in the summary the we create the instance.

Next we move to gitbash and we SSH in to our S3 Bucket instance

we run `sudo apt-get update` and then `upgrade` then we run `sudo apt-get install python` then we run `alias python=python3` this way we use version 3 of python rather than the default version 2.
then we run `sudo apt install python3-pip` then `aws configure` then from here we will be prompted to enter our information firstly with `access key` ,then `Secret key`, then `region` then we choose `json` for the last option.

Once we we have access to our S3 bucket we now need to make a bucket using the `aws s3 mb s3://belal-tech201` command then we go onto our AWS account and confirm it has been made. Then we make a file in git bash as follows `touch filename.txt` once this has been made we now move it to our S3 Bucket using the following command `aws s3 cp test.txt s3://belal-tech201`: Here we are telling it we would like to copy this file into our s3 bucket named `belel-tech201` 

Next in order to access this we need to change permissions we simply do this by going to our S3 bucket on the AWS menu we select our `Bucket` we select our `file` we go to permissions we `edit` permission to read by selecting the following as shown in the image.
![Alt text](../images/permissions.png)
We then `save changes` and now we can see our file if we click on the `object URL` found `properties` section of our file and it should look like this:

![Alt text](../images/s3%20file%20URL.png)



Furthermore in this image below we can see a summary of the whole process and how we used our local host to SSH into our S3 Instance and then from the we were able to use Git Bash to install all the required dependencies and then creat our S3 Bucket and then our file.
![Alt text](../images/s3%20diagram.png)



## How to automate file creation and deletion of an S3 Bucket:

First we made an EC2 instance and then we opened Git Bash and `ssh` inside out EC2 instance after that we installed the following dependencies using the following commands.

`sudo apt install python`
then
`sudo apt install python3-pip`
then
`sudo apt install awscli`
then
`aws configure` and here we enter our "Access Key" and "Secret access key" also our region and prefered file type.
then
`pip3 install boto3` if we get an error message do `sudo apt install python-pip` then the previous command.

from there we create a python file for using `nano file_name.py` we enter the following python code:

`import boto3`

#### S3 authentication setup - with aws configure on EC2

#### Create S3 bucket using python-boto3
`s3 = boto3.resource('s3')`
`s3.create_bucket(Bucket='belal-tech201-python2', CreateBucketConfiguration={'LocationConstraint': 'eu-west-1'})`

#### Upload data/file to S3 bucket using python-boto3
`bucket = s3.Bucket('belal-tech201-python2')`
`bucket.upload_file('C:/Users/belal/.ssh/test1.txt', 'test1.txt')`

# Retrieve content/file from S3 using python-boto3
`bucket.download_file('test1.txt', 'C:/Users/belal/.ssh/test1.txt')`

# Delete Content from S3 using python-boto3
`bucket.Object('test1.txt').delete()`



#### Delete the bucket using python-boto3
`s3.Bucket('belal-tech201-python2').delete()`

we then save this code and the run it using `python file_name.py` and our bucket should be created with the contents of the bucket also being deleted.

