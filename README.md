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

### Access the server from your terminal
- On the terminal in your computer, access the server

`ssh grader@3.222.110.15 -p 2200 -i ~/.ssh/udcty_key`
- As you changed the ssh port to 2200, you will no longer have access through `Connect using SSH` from AWS dashboard

### Alternatively install PuTTY to access server
- [Download PuTTY](https://www.putty.org/) and install it.
- Run PuTTYgen to generate a `.ppk` file
- Click Load button and locate the `udcty_key`
- Insert passphrase if you created so.
- Choose Save private key and a `udcty_key.ppk` will be created

- Run PuTTY
- Insert the IP address ``3.222.110.15`` in Host Name and 2200 in Port
- Under Category, select Connection -> Data. Insert `grader` in Auto-login username
- Under Category, expand SSH and choose Auth
- Click Browse and select `udcty_key.ppk` in the directory you saved it.
- Select Session and save it as `AWS_grader` or any other name you like
- Click Open to access the server

### Configure the local timezone to UTC
- On the terminal you are accessing the server, type
`sudo timedatectl set-timezone UTC` 

### Install and configure Apache
- Install Apache

`sudo apt-get install apache2`
- Install mod_wsgi

`sudo apt-get install libapache2-mod-wsgi`
- Restart Apache with 

`sudo apache2ctl restart`

### Install Python3
- Install the Python 3 mod_wsgi package on your server

`sudo apt-get install libapache2-mod-wsgi-py3`

### Install PostgreSQL
- Install PostgreSQL
`sudo apt-get install postgresql`


### Create and config database
- Change user to postgres

`sudo su - postgres`
- Get into postgres shell

`psql`
- Create a new database named **clubs** and create a new user named **grader** in postgreSQL shell

```
CREATE DATABASE clubs;
CREATE USER grader;
```
- Set a password for user **grader**

`ALTER ROLE grader WITH PASSWORD 'password';`
- Give user **grader** permission to the database **clubs**

`GRANT ALL PRIVILEGES ON DATABASE clubs TO grader;`
- Quit PostgreSQL

`\q`
- Logout from user postgres

`exit`



Check if no remote connections are allowed sudo vim /etc/postgresql/9.3/main/pg_hba.conf





--------------------
Do not allow remote connections
Create a new database user named catalog that has limited permissions to your catalog application database.
12. Install git.

Deploy the Item Catalog project.
13. Clone and setup your Item Catalog project from the Github repository you created earlier in this Nanodegree program.
14. Set it up in your server so that it functions correctly when visiting your server’s IP address in a browser. Make sure that your .git directory is not publicly accessible via a browser!

