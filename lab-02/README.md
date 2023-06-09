# Lab-02

## How to create Keypair for EC2

In this lab, we are going to create a keypair required for logging into EC2 instances

Amazon Linux EC2 instances do not use user id and passwords as they are generally easy to guess

Instead, they are protected using keypairs that you specify when launching the instance

Keypair consists of a public key, which is like a user id and a private key, which is similar to a password

So, when launching an instance, we need to specify the public key

And when you log in, we need to present the matching private key and EC2 logs 

## Architecture Diagram
![lab-02-arch-00](images/lab-02-arch-00.png)

## Steps - Keypair

1. Login to AWS console using your myadmin user

2. Open EC2 service console

3. Make sure you don’t have any popup blockers for this site

4. Ensure you are in the correct region – I am using US West Oregon. The keypair that we create are region-specific

5. Select Key Pairs from the left navigation pane

![lab-02-scrn-01](images/lab-02-scrn-01.png)

![lab-02-scrn-02](images/lab-02-scrn-02.png)

6. You can create a new one or import your existing key

7. Let’s quickly look at the import option

8. Action and Import Key pair

a. You need to provide only the public key of your existing key pair

b. This option is useful if you want to use the same key across different regions

c. You can use tools like openssh or putty to generate your own keys

https://www.ssh.com/academy/ssh/keygen

9. The other option is we can ask AWS to create one for us

10. Create Key Pair

a. Name: my_ore_keypair

I generally specify the username followed by region

b. KeyPairType: RSA

c. Private Key Format: Choose PPK format if you use a windows laptop. This format is compatible with the Putty tool that we will use on Windows. If you are on Mac or Linux laptop, you can select the PEM format. This format is compatible with the openssh tool

d. I will select PPK format as I primarily work on Windows Laptop

![lab-02-scrn-03a](images/lab-02-scrn-03a.png)

e. Using Putty tool, it is also possible to convert one format to another https://aws.amazon.com/premiumsupport/knowledge-center/ec2-ppk-pem-conversion/

11. Create Keypair

12. The page will automatically download the keypair to your machine. This is the only opportunity to download the keypair. EC2 will store only the corresponding public key in the console

13. Keep this file in a safe location. Treat it like a user id and password. [For example, C:\AWSTraining\Labs]

14. We can now use the key pair to log in to EC2 instances

15. If you are on Mac, Lab - Connect to your EC2 Linux from Mac lecture shows you how to connect to the EC2 instance

Steps – Putty Tool
1. If you are on windows, please install the Putty Tool

2. Go to https://www.putty.org/

3. Download Putty

4. Download 64-bit x86 MSI

5. Install the app

##  Launch EC2 instance, Login, Explore Private, Public, and Elastic IP

## Goal 
In this lab, we will launch an EC2 instance in a public subnet of the default VPC. We are then going to log in to the instance using SSH. Finally, we will also explore private, public, and Elastic IP address that you can assign to an instance

## Architecture Diagram

![lab-02-arch-03](images/lab-02-arch-03.png)

## Overview

Steps to launch

1. From AWS, open EC2 console

2. Make sure you are in the correct region

3. We will use the default VPC and Keypair that we created earlier

4. Select Instances in the left navigation pane

5. And launch instances

6. Name the instance: LinuxServer

7. For Amazon Machine Image

a. Choose Amazon Linux AMI

b. From AMI drop down: Select Amazon Linux 2


![lab-02-scrn-05](images/lab-02-scrn-05.png)

8. For instance type, use t2.micro or t3.micro – these are free-tier eligible instances. If you don’t see t2.micro, simply choose t3.micro

9. Key pair: Now, we need to specify the Keypair that can Login to the machine

a. If you don’t specify a keypair, you will not be able to Login to the machine

b. So, choose the Keypair that we created earlier

10. Network settings: we can provide VPC information

a. Edit

b. VPC: Select default VPC

c. Subnet: let’s pick the subnet in Availability Zone 2A (scroll the list and find the Availability Zone ending with 2A)

d. Auto-assign Public IP: Enable

e. Let’s create a new Security Group – we are going to allow SSH access so that we can log in to the machine

f. Security group name: SSHAccess

g. Type: SSH

h. Protocol: TCP

i. Port: 22

j. Source type: Select Anywhere. All 0s mean any IPv4 address. The ::/0 refers to any IPv6 address. So, anyone can connect to the SSH port.

k. Usually, you would want to limit SSH access to a specific IP address. For example, I can limit access only from my IP address. For this lab, let’s use it anywhere

11. For storage, we will use the default storage of 8GB

a. Go to the next page

12. Launch the Instance

![lab-02-scrn-06](images/lab-02-scrn-06.png)

13. Click on Instances

14. We can see our LinuxServer and wait until the instance state changes to Running

15. Click on the Instances Id link to open the detail page

16. And we can see the details

a. This server has a public IP address assigned

b. And it also has a private IP address

c. Scroll down and view the Security tab

![lab-02-scrn-07](images/lab-02-scrn-07.png)

d. We can see that under security group inbound rules, SSH Access is allowed on port 22 from anywhere

e. Let’s copy the public IP (scroll up)

![lab-02-scrn-08](images/lab-02-scrn-08.png)

Steps to Login
1. Now, we are going to Login into the server

2. How you Login depends on your laptop Operating system

3. If you are using Mac or Linux, click on Connect button to see the instructions. You can also watch the next video Lab - Connect to your EC2 Linux from Mac

4. Go to the SSH Client tab

a. If you are using Mac or Linux client, you need to open the terminal and run these commands

b. You need to run the chmod command to ensure your key is not publicly visible

c. Now you can connect using SSH. You can copy and paste the command

5. I will show you how to connect from Windows using Putty

a. Copy the server’s public IP address

b. Launch Putty

c. In the Host Name or IP Address, paste the public IP

d. We need to specify the username. Amazon Linux default user name is ec2-user

e. We can specify both username and IP address using this convention ec2-user@publicIP

f. Now, we need to configure the key file to use

g. Expand SSH in the left navigation pane

h. Select Auth

i. In the Private key file for authentication, we need to browse to the keypair file [C:\AWSTraining\Labs]

![lab-02-scrn-09](images/lab-02-scrn-09.png)

j. And Open

k. Now you can save all these configurations

l. Go to Session

m. In the Saved Sessions text box, provide a name. I use the region name – OregonServer

n. And click Save

o. Now, we can click on the saved configuration and load it when needed

p. To connect to the server, click Open

q. And we are connected to the server

6. Let me adjust the font size – exit the server

a. Start Putty again

b. Load the saved session

c. Select Appearance

d. Change Font – I am going to use a 16 size

e. Go back to the session and save it again

f. And open

![lab-02-scrn-10](images/lab-02-scrn-10.png)

7. And it is much better

8. You now have full administrative access to this server

9. Now we can exit

Steps – Stop and Start
1. Let’s now understand how the Public IP address is assigned

2. Let me copy and paste public and private IP to a text file

3. Now, we are going to stop the server

![lab-02-scrn-11](images/lab-02-scrn-11.png)

4. From Instance State Menu, choose Stop Instance

5. Wait until the Instance state changes to Stopped

6. Now, if you look at the instance details

a. Public IP is missing

![lab-02-scrn-12](images/lab-02-scrn-12.png)

b. Private IP is still the same

c. When you stop an EC2 instance, the public IP is automatically released. Whereas Private IP stays with the Instance

7. Let’s start the Instance again

a. Instance state Menu and Start instance

b. Wait until Instance is running

8. A new public IP is assigned to the Instance

9. To Login to the server from your laptop, you now need to use this new IP

10. Launch Putty

11. Load the session

a. Change Host Name to use the new IP address

b. Save

c. Open

12. So, this is an important point to remember. Anytime you stop the EC2 Instance and start it, the Instance Public IP will change

a. Exit from terminal

## Steps – Elastic IP

1. Let’s now look at Elastic IP

2. Elastic IP is a static public IP address

3. From EC2 Console left navigation pane, scroll down and select Elastic IPs

4. Choose Allocate Elastic IP Address

![lab-02-scrn-13](images/lab-02-scrn-13.png)

5. Use default settings and Allocate

![lab-02-scrn-14](images/lab-02-scrn-14.png)

6. An Elastic IP is now assigned to your account from Amazon’s pool

7. This IP address is yours until you release it

8. Let’s associate this IP address to our Instance

9. From Actions, select Associate Elastic IP address

![lab-02-scrn-15](images/lab-02-scrn-15.png)

10. For Resource type, select Instance

11. And choose the Linux Server in the instance text box

12. Associate

![lab-02-scrn-16](images/lab-02-scrn-16.png)

13. Now go back to the instance detail page and refresh the page

14. If you look at the Elastic IP address, our Instance now has the Elastic IP assigned, and this IP address is also shown under public IP

![lab-02-scrn-17](images/lab-02-scrn-17.png)

15. We can now connect to the server using this Elastic IP

a. Login

b. Exit

16. Now let’s see what will happen if we stop the Instance

a. From Instance State, Stop Instance

b. The Instance is stopped now

c. If you look at the details, Public IP and Elastic IP is still assigned

![lab-02-scrn-18](images/lab-02-scrn-18.png)

d. The Elastic IP stays with the Instance until we explicitly disassociate or terminate the Instance

![lab-02-scrn-19](images/lab-02-scrn-19.png)

## Steps – Cleanup

1. To Cleanup, let’s terminate the Instance

![lab-02-scrn-21](images/lab-02-scrn-21.png)

a. From instance state, choose Terminate instance

b. Wait until the instance state changes to Terminated

2. Go to the Elastic IPs page

a. Select the Elastic IP

b. From Actions, choose Release Elastic IP Address

![lab-02-scrn-20](images/lab-02-scrn-20.png)

c. If the Release Elastic IP address option is disabled or if you see an error that it is currently associated, wait for a minute and refresh the page, and try again

3. To avoid unnecessary charges, ensure you terminate the Instance and release the elastic IP

![lab-02-scrn-22](images/lab-02-scrn-22.png)

## Summary

In this lab, we launched an EC2 instance and connected using Putty

We also observed the behavior of Public IP and Elastic IP addresses