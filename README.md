# Set-Up-A-Home-Lab

## Objectives
- Create Secure Non-Root User Accounts
- Design and Implement a Virtual Private Cloud (VPC)
- Launch and Manage AWS EC2 Instances
- Configure Security Groups and Firewalls
- Terminate Instances to Avoid Unnecessary Costs

## Methodology
### Step 1: Creating a Non-Root User with IAM
Before creating a non-root user account with Identity and Access Management (IAM), you will need to create a free Amazon Web Service (AWS) account first. This will be your root user account that has complete access to all of the AWS services and resources. Once that is created, go to the IAM console, then to the Users section to create the user account:

![Screenshot 2024-06-11 122503](https://github.com/user-attachments/assets/992aa6ca-1f60-4503-8856-97c75c5fd6c0)

The next step is to create the name of the user, tick the “Provide user access to the AWS Management Console”, and select “I want to create an IAM user” as the user type.

![Screenshot 2024-06-11 122702](https://github.com/user-attachments/assets/4b5afa95-b2a3-4e65-992c-bdbdcad3f3c7)

The next step is to create a user group where the Administrator Access permission policy is assigned to users in this specific user group.

![Screenshot 2024-06-11 124225](https://github.com/user-attachments/assets/90c527a6-ca97-4e1f-8ddc-77900d72fe56)

The multi-factor authentication (MFA) needs to be enabled to the user account for extra security. 

Once that is done, the next step is to create the Virtual Private Cloud (VPC).

### Step 2: Setting up a VPC
The Virtual Private Cloud (VPC) feature is always free and it consists of subnets, internet gateways, and routing tables. Go to the VPC dashboard to create a VPC.

![Screenshot 2024-06-11 125510](https://github.com/user-attachments/assets/e9550d5a-74d0-49a9-a516-6820ed93a28b)

The next step is to create the internet gateway and attach it to the VPC that was just created.

![Screenshot 2024-06-11 132018](https://github.com/user-attachments/assets/9041f9bb-aeeb-4172-b485-2275525fd726)
![Screenshot 2024-06-11 132145](https://github.com/user-attachments/assets/39da5e9e-26be-448f-b523-720b3f57db9f)

The next step is to create a route table which would be assigned to the VPC.

![Screenshot 2024-06-11 132434](https://github.com/user-attachments/assets/ac6df8e7-bb8e-4f6e-b4bf-8dea4f074a20)

Once the route table is created, the route will then need to be edited so that the internet gateway will be added as the target.

![Screenshot 2024-06-11 132832](https://github.com/user-attachments/assets/13453d7e-b254-4482-93f5-66ec7276ec46)

The public subnet needs to be created for this VPC so that the route table is associated with this subnet.

![Screenshot 2024-06-11 133822](https://github.com/user-attachments/assets/34b9f1b7-352e-48b5-aa5a-7bad1ef8e4b1)
![Screenshot 2024-06-11 134103](https://github.com/user-attachments/assets/43032ea1-2a20-4a60-ba3f-80e1bbc6e62f)

The next step is to create a security group which acts as a firewall rule. This is to allow inbound SSH connections to come from anywhere.

![Screenshot 2024-06-11 134417](https://github.com/user-attachments/assets/1df2c7cb-12cc-49df-8b48-df82c5a00d8c)

### Step 3: Launch AWS EC2 Linux Instance
The next step is to create a EC2 instance. The free tier option will be chosen to avoid charges. The Amazon Machine Image chosen is the Amazon Linux 2. This is eligible for the free tier. The instance type chosen is the t2 micro which consists of 1 CPU core and 1GB RAM.  

![Screenshot 2024-06-11 135546](https://github.com/user-attachments/assets/07cde2bf-2b65-4802-a685-fb3fd4b9c3ca)

In terms of network settings, the default VPC will be assigned. The inbound security group rule will allow all traffic. This is not recommended.

![Screenshot 2024-06-11 140148](https://github.com/user-attachments/assets/901d75fe-72ae-4f5f-82c5-66bda9c3cf8e)

The storage for this instance is the default storage which is 8GB.

![Screenshot 2024-06-11 140018](https://github.com/user-attachments/assets/f26e1596-881f-480b-8477-00e2838e0464)

The key pair for this instance needs to be created to allow SSH connections.

![Screenshot 2024-06-11 140339](https://github.com/user-attachments/assets/2527c0a9-80ea-49e6-96f7-021e53639e6a)

Once the instance is created, give it a few minutes for the instance to start running. 

The next step is to connect the instance using the EC2 Instance Connect or an SSH Client such as OpenSSH Client or PuTTY. If you are using OpenSSH, you will need to connect to the Linux server using the following command:
ssh -i “path/to/your-key-pair.pem” ec2-user@ec2-18-130-32-132.eu-west-2.compute.amazonaws.com

The “your-key-pair.pem” is the private RSA key that is assigned to this EC2 Instance. If you are using a OpenSSH to connect to the server, the key needs to be saved under the “.pem” format. If you are using PuTTY to connect to the server, you need to convert the private key to the “.ppk” format using the PuTTYgen application.

This is the output when running the EC2 instance:

![Screenshot 2024-06-11 141814](https://github.com/user-attachments/assets/476f4721-5e30-4884-80d5-3240559102c1)

The next step is to disconnect and terminate the EC2 Instance. 

![Screenshot 2024-06-11 142109](https://github.com/user-attachments/assets/2f3f2031-b4c9-4a0c-81d9-1caa29bf37e9)

### Step 4: Launch AWS EC2 Windows Instance 
The next step is to create an EC2 Windows Instance. The AMI chosen for this is the Microsoft Windows Server 2019 base. The following steps are the same as shown for the Linux Instance. All of the default settings should remain as it is. As for the key pair, a new one would be created. 

![Screenshot 2024-06-11 142820](https://github.com/user-attachments/assets/cf5aa7c0-07e2-4c7b-9743-05dd29218be1)

For the network settings, the default VPC should be assigned and the inbound security group rule should only allow RDP connections and the source is “Anywhere”. This is not recommended, however, for this project, it is tolerable because the instance will be shut down by the end of this project.

![Screenshot 2024-06-11 143218](https://github.com/user-attachments/assets/b8b277e6-1c74-4fe5-91d1-cb8b20f4ab5a)

The next step is to launch the instance and wait for a few minutes to allow the instance to run.

To connect to the instance, you will need to connect to it using the Remote Desktop Connection on the PC. Before doing so, the remote desktop file for this instance needs to be downloaded first.

![Screenshot 2024-06-11 144030](https://github.com/user-attachments/assets/0eec1b1c-f614-46d5-8da9-abca15976d43)

The Windows password for this instance needs to be decrypted using the instance’s private key to log in.  

![Screenshot 2024-06-11 144316](https://github.com/user-attachments/assets/fe3f8243-520c-47f3-a297-eaad4e495b3f)

Now that the instance remote desktop file is downloaded and the password is decrypted, the next step is to login to the remote desktop.

![Screenshot 2024-06-11 144719](https://github.com/user-attachments/assets/12285b76-637d-4583-92ed-af14864e5d05)

This is the result:

![Screenshot 2024-06-11 145034](https://github.com/user-attachments/assets/f9702664-d070-4f16-bed3-e7dbd56afae0)

The instance will then be disconnected and terminated. This is to avoid any charges. 

## Conclusion
To summarise this project, the secure AWS cloud environment has been successfully set up by configuring IAM user accounts, creating a VPC, and configuring the firewall. The EC2 Linux and Windows instances were successfully deployed as well. The purpose of this project is to demonstrate that this secure cloud environment can be accessed anywhere, no additional hardware is required, and have access to commercial software.

## Reference
<a href="https://youtu.be/uo_Xf_pGTvg?si=Q6YfiGep0XDQVjej">HOW TO Build a Home Lab in AWS For FREE // Cyber Security and IT</a> 




















