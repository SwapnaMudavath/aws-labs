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

![lab-02-scrn-00](images/lab-02-scrn-01)

![lab-02-scrn-00](images/lab-02-scrn-02)





##  Launch EC2 instance, Login, Explore Private, Public, and Elastic IP

## Goal 
In this lab, we will launch an EC2 instance in a public subnet of the default VPC. We are then going to log in to the instance using SSH. Finally, we will also explore private, public, and Elastic IP address that you can assign to an instance

## Architecture Diagram
![lab-02-arch-01](images/lab-02-arch-01.png)

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