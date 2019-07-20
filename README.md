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
- On the SSH opened window, update the software source list

`sudo apt-get update`
- Now update the software 

`sudo apt-get upgrade`
- Remove unnecessary software

`sudo apt-get autoremove`
- Install finger

`sudo apt-get install finger`

### Create a new user
- In the SSH opened window, create a new user called grader. You will have to define a passsword and full name

`sudo adduser grader`

### Give the new user sudo permission
- Check that the file etc/sudoers have the line #includedir /etc/sudoers.d
- It means that you need to include the permission file in this directory
- As you want to give sudo access to grader user, so create a file grader in /etc/sudoers.d

`sudo touch /etc/sudoers.d/grader`
- Edit the file with nano and paste the following `grader ALL=(ALL:ALL) ALL`

`sudo nano /etc/sudoers.d/grader`
- In nano type `grader ALL=(ALL:ALL) ALL` and save it.


### Create SSH pair for new user
- Open a terminal in your computer
- In the terminal create a SSH key pair. 

`ssh-keygen`
- Define a name for the key file e.g. `udcty_key` and a passphrase
- Use the same suggested directory to create the key files `/c/Users/<YOU>/.ssh/`
- Two files will be created: the private key `/c/Users/<YOU>/.ssh/udcty_key` and the public key `/c/Users/<YOU>/.ssh/udcty_key.pub`

### Place the public key on the remote server
- On the server terminal change the user to grader

`su - grader`
- Create `.ssh` directory

`mkdir .ssh`
- Create file `authorized_keys`

`touch .ssh/authorized_keys`

- Open the file with nano and copy the contents the public key file `/c/Users/<YOU>/.ssh/udcty_key.pub` created in the previous item

`nano .ssh/authorized_keys`

- Change privileges accesses as follows:

```
chmod 700 .ssh
chmod 644 .ssh/authorized_keys
```

- On the terminal in your computer, access the server

`ssh grader@3.222.110.15 -p 22 -i ~/.ssh/udcty_key`

### Change SSH port
- Change the SSH port from 22 to 2200
`sudo nano /etc/ssh/sshd_config`
- Reload SSH service
```
sudo service ssh restart
sudo service sshd restart
```

### Configure the Firewall
- Configure the firewall to allow ssh using port 2200, HTTP through port 80 and NTP through port 123

```
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw allow 2200/tcp
sudo ufw allow www
sudo ufw allow ntp
sudo ufw enable
````


