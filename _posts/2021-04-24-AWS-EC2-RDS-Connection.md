---
layout: posts
title: "Connecting to an Amazon MySQL RDS database"
---

I recently received my AWS Solutions Architect Associate Cert, and I inadvertently  learned more about Ops and DevOps in respect to automation, deployment and most importantly secrets and access. So I wanted to share my knowledge on creating short lived credentials for database users and administrators. In that vain, this blog post is the lab setup for a Secrets management post that uses Vault.

The blog post for a tutorial to rotate database credentials via Hashicorp Vault can be found [here](https://haydz.github.io/2021/04/25/Secrets-Managent-Vault.html)



In this blog post, the term Vault will be used to refer to [Hashicorp Vault](https://www.vaultproject.io/)



This blog post will cover:
- Setting up a MySQL Server in AWS RDS
- Setting up an EC2 instance in AWS



Requirements:
* an AWS account 
    * you can  do all of this locally if you prefer. It could be completed on one system such as Ubuntu (But will need to install MySQL)

<br>
# The Setup in AWS:
For the lab setup will include:
* An EC2 instance 
* MySQL Server installed on AWS Relational Database Service

Both the RDS database and EC2 instance will be created in the Ohio region:


![](/images/vault_db/image_33.png)


## Creating a new user
It is best practice not to use an AWS root account, as such a new user will be created, a policy to access EC2 and RDS will be applied to the new user.

The new user having only access to EC2 and RDS and nothing else is in alignment with the principle of least privilege.

AWS documentation for creating an Administrator user that is not ROOT can be found here: [here](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html)

The below instructions will create a new user with only the correct permissions to access EC2 and RDS

Sign into the root account in AWS:  
![](/images/vault_db/image_1.png)

Go to the Identity and Access Management section:  
![](/images/vault_db/image_2.png)

Select Users and click add users

Create a new user:
Check `AWS Management Console Access`
Create a custom password
Uncheck the `User must create a new password at next sign-in`

It should look like the below image:

![](/images/vault_db/image_3.png)

Click `Next:Permissions`.

Ideally, in an organization there would be groups that the user could be placed in. However for this tutorial and testing we are going to attach existing policies to the new user directly.

The Permissions page will look something like:  
![](/images/vault_db/image_12.png)

Please select `Attach existing Policies Directly`:

![](/images/vault_db/image_11.png)

Within the 'Filter policies' section type `EC2`, and then choose `AmazonEC2FullAccess`.

This will give the user admin access over the EC2 service. The `AmazonEC2FullAccess` can be seen here:

![](/images/vault_db/image_13.png)"

Now the EC2 permissions have been attached, the RDS permissions should be attached. Within the `Filter policies` section type RDS, and then choose "AmazonRDSFullAccess".

The `AmazonRDSFullAccess` can be seen here:
![](/images/vault_db/image_14.png)

Click `Next:tags`, and then click `Next:Review`.

In the review page, ensure the permissions summary includes:
* "AmazonEC2FullAccess"
* "AmazonRDSFullAccess"

It will look like:
![](/images/vault_db/image_15.png)

Click `Create user`, and the user should have been created.

The success page will look like:  
![](/images/vault_db/image_16.png)

*Please take note of the sign-in address*


### Sign in as the new user:
Now the a non-root user has been created (least privilege), the rest of the setup will take place as that user. To login, follow the steps below:
  
Use the sign in link shown in the success screen from creating the user to login:
![](/images/vault_db/image_17.png)

Login with the new users credentials:

![](/images/vault_db/image_18.png)


## Creating a MySQL RDS:
The infrastructure will include a MySQL server hosted on the AWS Relationship Database Service. The steps below will go through setting up one:

Ensure you are signed in as the non-root user:

![](/images/vault_db/image_19.png)

Go to the Amazon Relational Database Service:

![](/images/vault_db/image_21.png)
![](/images/vault_db/image_20.png)

Once on the RDS section, the next steps are:

* Click "Create a Database"
* Select "Standard Create"
* Select "MySQL"
* Ensure "Free tier" is selected

It will look like:

![](/images/vault_db/image_22.png)
![](/images/vault_db/image_25.png)

Choose a MySQL version of 5.7.x:

![](/images/vault_db/image_23.png)

Name the database within "DB instance identifier" and create an admin password:

![](/images/vault_db/image_24.png)


Settings for the database:
* Most of the settings can be default.
* The default VPC will be used, because the EC2 server that will be connecting to the RDS will also be within the default VPC.

Ensure Public access is set to no.

![](/images/vault_db/image_26.png)

For VPC security groups select "Create new" and give it a name.
We will edit the RDS security group later, to allow only traffic from the Security Group the EC2 server is in.

![](/images/vault_db/image_27.png)

Ensure database authentication is set to password authentication (this is by default).


Then select Create database:

![](/images/vault_db/image_28.png)

The database will show up within the Databases section

![](/images/vault_db/image_29.png)

## Creating the EC2 instance:
This section is for creating the EC2 instance/server that will be used to host Vault and connect to the MySQL RDS server.

For these steps please ensure you are logged in as the non-root user again.

Go to the EC2 service:

![](/images/vault_db/image_30.png)


![](/images/vault_db/image_31.png)

Click "Launch Instance" on this page to begin creating an EC2 instance:

![](/images/vault_db/image_32.png)


Within "Step 1: Choose an Amazon Machine Image (AMI)" type Ubuntu and press enter:

![](/images/vault_db/image_34.png)

Choose either of the Ubuntu servers (18,20) and click select. Ensure you choose the "free tier" eligible ones.


Within "Step 2: Choose an Instance Type" Choose the free tier option and click "Next: Configure Instance Details

![](/images/vault_db/image_35.png)


Within "Step 3: Configure Instance Details" ensure the default VPC is chosen. All default permissions are fine, click "Next: Add Storage":

![](/images/vault_db/image_36.png)

Within: "Step 4: Add Storage" keep all default options and click "Next: Add Tags":

![](/images/vault_db/image_37.png)

Within "Step 5: Add Tags" click "Next: Configure Security Group":

![](/images/vault_db/image_38.png)

Within "Step 6: Configure Security Group" you may be able to select a default security group. But for this tutorial we are going to create a new security group and name it "ec2_secret_demo_sg".


Ensure the port 22 is allowed:
![](/images/vault_db/image_39.png)


Now select "Review and Launch"

Within "Step 7: Review Instance Launch" ensure the settings are correct and then click launch.

It will ask you to use an existing key pair or create a new key pair. I have created a new pair called demo_key:

![](/images/vault_db/image_40.png)

Download the key and then click "Launch Instances". This take you to a "Launch Status Page", click "View Instances".

From here, it will take you back to the EC2 main page, and you should be able to see the instance running like so:

![](/images/vault_db/image_42.png)



### Testing EC2 access
Once the EC2 has been created, it is a good idea to test that the key pair works and you can login.

Select your instance, and then click connect:

![](/images/vault_db/image_42.png)


Select SSH client and read the instructions. The most important part is the connect example, which can be copied and pasted into a terminal to test access:

![](/images/vault_db/image_43.png)

Attempt to login with your key pair and instance Public DNS like so:

![](/images/vault_db/image_44.png)

Successfully logging in will give an Ubuntu command prompt:

![](/images/vault_db/image_45.png)

## Install MySQL client on EC2
The EC2 instance needs the mysql client installed so that it can connect to the MySQL RDS database.

When logged onto the EC2 server please install the client with:
{%highlight bash linenos %}
sudo apt-get install mysql-client
{% endhighlight %}


![](/images/vault_db/image_46.png)


## Allowing access to the RDS database
When creating the RDS database a new security group was created. This security group needs to be configured to allow the EC2 server to connect to it.

Attempting to connect from the EC2 server with the `mysql` client will not work, and will simply hang like so:

![](/images/vault_db/image_47.png)

To fix this, the  the Security Group for the database needs to be configured.

The easiest way is to go to the EC2 service and select Security Groups, this is under Network and Security:

![](/images/vault_db/image_48.png)

Select the Security Group that the RDS database is using, in the tutorial it was called "db_securitygroup":

![](/images/vault_db/image_49.png)

Edit the Inbound rules and under source select the EC2 Security group, which in this tutorial was named "ec2_secret_demo_sg":

![](/images/vault_db/image_50.png)

If selected correctly it will look like:

![](/images/vault_db/image_51.png)

Click "Save rules", and the next page will show the `db_securitygroup` rules. The rule you updated with the EC2 Security Group should be showing:

![](/images/vault_db/image_52.png)

## Test connection to the MySQL RDS database
Now that the Security Group for the RDS database allows  connection from the EC2 servers Security Group, we should test that it works.

AWS documentation for connecting to a MySQL RDS database is [here](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ConnectToInstance.html).

The command to connect from the mysqlclient is:

{%highlight bash linenos %}
mysql -h <RDS endpoint> -P 3306 -u <username> -p
{% endhighlight %}


To find the endpoint of the database, go to the AWS RDS service and select the database:  

![](/images/vault_db/image_53.png)

Select the database within Databases:

![](/images/vault_db/image_54.png)


Under Connectivity and security will be the endpoint:

![](/images/vault_db/image_55.png)

For this tutorial, the MySQL RDS server, the command becomes:
{%highlight bash linenos %}
 mysql -h database-1.csbn9npl7lxh.us-east-2.rds.amazonaws.com -P 3306 -u admin -p
{% endhighlight %}

 
 Enter the password you gave for the user and login
 
 If successful you will see a banner and mysql prompt:
 
![](/images/vault_db/image_56.png)
 
 Congratulations, you have created an EC2 server, a MySQL RDS database and connected to the database.
 
 Again, this is used as the infrastructure setup for the tutorial on configuring Hashicorp Vault to rotate database credentials.
 
 That can be found [here]([here](https://haydz.github.io/2021/04/25/Secrets-Managent-Vault.html)