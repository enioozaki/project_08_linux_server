PROJECT_08_LINUX_SERVER
=======================

## Project Overview
Install a Linux server, preparing it to host a web application and securing it from attacks.
Install and configure a database server and deploy one web application on it.

## Tasks to be accomplished
- Create an instance in AWS
- b

### Create an instance in AWS
- Login to [AWS](https://aws.amazon.com/pt/console/) . If you don't have an AWS account, create one.
- Access [Lightsail](https://lightsail.aws.amazon.com/ls/webapp/home/instances) service in Console Home 
- Create an instance:
  - Select platform: Linux/Unix
  - Select OS Only/Ubuntu 16.04 LTS
  - Choose an instance plan: $3.50 (the first month is free)
  - Identify the instance: Udcty_server (or any other name you want)
  - Click `Create instance`
- You will be given a public IP number (for ex.: `3.222.110.15`) and a user name: `ubuntu`

### Access the server
- Click over the name of the instance you have just created
- Connect to the server clicking `Connect using SSH`
- A new window will pop up with the access to the server
