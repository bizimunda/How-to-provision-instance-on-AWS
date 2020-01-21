### How to provision instance on AWS

In this mini lab/lesson we are going to provision an EC2 using Hashicorps's terraform.

### Tools
    - Linux (Debian)
    - Terraform

Reference: https://www.terraform.io/docs/providers/aws/index.html

### What is Terraform?

Terraform is a tool made by Hashicorp for building, changing, and versioning infrastructure safely and efficiently. 
Terraform can manage existing and popular service providers ( aws, azure, Google cloud) as well as custom in-house solutions.
You can compare Terraform to Cloudformation but Cloudformation is specifically for AWS . They are simililar but at the same time have differences.

#### Steps to provision
Download the terraform binary file https://www.terraform.io/downloads.html according to your system. I'm using 64bits


#### Step 1 - Extract the zip file
<pre><code>wget https://releases.hashicorp.com/terraform/0.12.19/terraform_0.12.19_linux_amd64.zip
</code></pre>


You will see the terraform binary executable file

#### Step 2
Now you have to execute this command to unzip 
<pre><code>unzip terraform
</code></pre>

If you don't have zip installed on your OS then execute this command
<pre><code>sudo apt install zip
</code></pre>

Make sure that the terraform binary is available on the PATH.

#### Step 3
Now you have to execute 2 commands
<pre><code>echo $"export PATH=\$PATH:$(pwd)" >> ~/.bash_profile
</code></pre>
<pre><code>source ~/.bash_profile
</code></pre>

On the shell/terminal, go to the folder where terraform binary is extracted

#### Step 4
Make a new directory(can be named anything) and go inside the directory by this command
<pre><code>mkdir terraformWork && cd terraformWork
</code></pre>

Now you have to open the nano editor to wirte code in it
#### Step 5
Command
<pre><code>nano ec2.tf
</code></pre>

Paste this following code to a file called ec2.tf (can be anything.tf)

<pre><code>provider "aws" {
  access_key = "ACCESS_KEY_HERE"
  secret_key = "SECRET_KEY_HERE"
  region     = "us-east-1"
}

resource "aws_instance" "example" {
  ami           = "ami-2757f631"
  instance_type = "t2.micro"
}
</code></pre>



#### Note:
Replace the access_key and secret_access with your AWS IAM user credentials with enough permissions attached. 
You can go to IAM console on AWS to do this. First, go to the IAM management 

<b>IAM</b>
![alt text](https://github.com/bizimunda/How-to-provision-instance-on-AWS/blob/master/images/Iam.jpg "Iam")


<b>Then Click on the users</b>
![alt text](https://github.com/bizimunda/How-to-provision-instance-on-AWS/blob/master/images/users.jpg "users")


<b>Now click on the user name</b>
![alt text](https://github.com/bizimunda/How-to-provision-instance-on-AWS/blob/master/images/hamid.jpg "user name")

And navigate to the security credentials tab. 

<b>Click Create access key</b> 
![alt text](https://github.com/bizimunda/How-to-provision-instance-on-AWS/blob/master/images/Create%20access%20key.jpg "Acces key")


Either download the csv file or, click show keys. Now you have both the access_key and secret_key required for the terraform code above. iam

If you've setup the AWS CLI and have credentials stored , you may skip the credential portion. This is what Hashicorp says "If you simply leave out AWS credentials, Terraform will automatically search for saved API credentials (for example, in ~/.aws/credentials) or IAM instance profile credentials. 
This option is much cleaner for situations where tf files are checked into source control"


#### Step 6
Initialize the working directory for terraform
<pre><code>terraform init
</code></pre>

The terraform init command is used to initialize a working directory containing Terraform configuration files. This is the first command that should be run after writing a new Terraform configuration or cloning an existing one from version control. It is safe to run this command multiple times.



#### Step 7
Provision the ec2 with this command
<pre><code>terraform apply
</code></pre>

Login to the AWS management console and navigate to the EC2 management console. Check if the instance got provisioned

#### Step 8
Make sure that you are in US East (N. Virginia) zone.

<b>Verify the instance we have just created</b> 
![alt text](https://github.com/bizimunda/How-to-provision-instance-on-AWS/blob/master/images/instace.jpg "Iam")

From your terminal/command prompt/ shell , destroy the resources
<pre><code>terraform destroy
</code></pre>
