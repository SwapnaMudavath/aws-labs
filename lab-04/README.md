# Lab-04

## Elastic Load Balancing 

In this lab, you will learn how to configure an Auto Scaling Group using a launch template

Launch template is similar to the launch configuration to specify instance configuration information

Here are some important advantages

1. Version support – you can build a base template and create new versions. This, in theory, should allow you to rapidly update your template with the latest version of your application

2. You can defer decisions such as type of instances to use, purchasing options spot-versus-on-demand , and so forth in the Autoscaling group

3. AWS does recommend that we use launch templates with Auto scaling groups as it provides access to the latest EC2 features

