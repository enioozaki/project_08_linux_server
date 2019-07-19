PROJECT_08_LINUX_SERVER
=======================

## Project Overview
Install a Linux server, preparing it to host a web application and securing it from attacks.
Install and configure a database server and deploy one web application on it.

## Tasks to be accomplished
- [Create an instance in AWS](#create-an-instance-in-aws)
- [Access the server](#access-the-server)
- [Update installed packages](#update-installed-packages)
-


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

### Update installed packages
- In the SSH opened window, update the software source list

`sudo apt-get update`
- Now update the software 

`sudo apt-get upgrade`
- Remove unnecessary software

`sudo apt-get autoremove`
- Install finger

`sudo apt-get install finger`

### Change SSH port
- Change the SSH port from 22 to 2200
`sudo nano /etc/ssh/sshd_config`
- Reload SSH service
`sudo service ssh restart`

```
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw allow 2200/tcp
sudo ufw allow www
sudo ufw allow ntp
sudo ufw enable
````
### Create a new user
- Create a new user called grader. You will have to define a passsword and full name

`sudo adduser grader`
- 

### Give the new user sudo permission
- Copy the ubuntu  in /etc/sudoers.d to grader

`sudo cp /etc/sudoers.d/ubuntu /etc/sudoers.d/grader`
- Edit the file grader with nano
`sudo nano /etc/sudoers.d/grader`
- In nano substitute the word ubbuntu for grader and save it




### Create SSH pair for new user
- Open a terminal in your computer
- In the termnal create a SSH key pair. Define a name for the key file and a passphrase

`ssh-keygen`
- 




