---
title: Terraform for AWS
layout: post
tags: [server]
---
## Use Terrform for creating AWS Infrastructure


You can use Terraform to create many types of AWS infrastructure like new EC2 instances.

There are many ways to accomplish this and this is how I did it.


___

### File Structure:

+ main.tf  <— main Terraform file
+ variables.tf <— variables used by Terraform
+ terraform.tfvars <— secret values like AWS credentials
+ ./vars/main.yaml <— used by Ansible (optional)
+ ./roles/whatever/tasks/main.yaml <— Ansible tasks (optional)

___


*NOTE:*  **make sure that terraform.tfvars gets placed in your .gitignore file because you don’t want this info broadcasted anywhere.**


Format **terraform.tfvars** as below (replace the quoted entries) : 


~~~bash

aws_access_key = "ENTER-YOUR-ACCESS-KEY-HERE"
aws_secret_key = "ENTER-YOUR-SECRET-KEY-HERE"

~~~


