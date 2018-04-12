# Configuring Server for a Python Flask Application

## About

This is the final project for the Udacity Full Stack Nanodegree. The goal
is to securely put the fourth project, an item catalog, onto a web server with firewalls, root login disabled, and make sure all packages are up to date on the server.

A virtual environment is created for the item catalog to avoid any installed dependencies interfering with different versions of the same software on the server. A WSGI entry point is made by importing the main server file into the WSGI app. uWSGI is then configured to server the files. SystemD service file is then used to automatically launch the app on when the server is running. nginx is then used to pass http requests to the server from outside of the server.

The fourth project can be seen here: https://github.com/dylance/Udacity-FSND-Project4

IP Address Used: 198.199.114.89

url: http://198.199.114.89/

SSH port: 2200

## Software Installed on Server

- Python 2
- Git
- Nginx
- PostgreSQL
- Mod_wsgi

## Steps to Configure Server

create droplet server on digital ocean

Create a hostname for you server.

my server's name hostname: UdacityServer

My server's ip: 198.199.114.89

remotely connect to server - `ssh root@198.199.114.89`

above line uses ssh keys already set up on my local machine and with digital ocean

#### Update server

 check ubuntu for updates - `sudo apt-get update`

 get updates - `sudo apt-get upgrade`

#### Create new user

Create User -  `sudo adduser <YOUR USER NAME>`

Give user sudo privelages - `sudo nano /etc/sudoers.d/<YOUR USER NAME>`

Add this text to user's file in sudoers.d -  `<YOUR USER NAME> ALL=(ALL) NOPASSWD:ALL`

Exit server - `exit`

#### Create SSH keys

On your local machine:

Create new Key `ssh-keygen`  

Save key in desired location with desired name - `/Users/austin/.ssh/id_rsa` is the default location and file name for locatl ssh keys

Log on to server as grader  

Ho to root directory - `cd ~`

Make directory to store public key - `mkdir .ssh`

Make file with authorized keys - `touch .ssh/authorized_keys`

Open nano to edit file -  `nano .ssh/authorized_keys`

Copy paste text from public key on your local machine to  .ssh/authorized keys on your server

Give only the user you created access to .ssh folder. `chmod 700 .ssh`

Change permission for authorized keys to read only for other users - `chmod 644 .ssh/authorized_keys`

Exit server and close ssh connection `exit`

log onto server for me -  `ssh grader@198.199.114.89 -i <YOUR SSH KEY FILE PATH>`


#### Enable  forced key based authentication

`sudo nano /etc/ssh/sshd_config`

 Change PasswordAuthentication to no

 Restart configuration service so it uses new changes - `sudo service ssh restart`


#### Set up Firewall


Checks firewall status - `sudo ufw status`

Deny all incoming requests

Firewall is not enabled yet so this is ok. - `sudo ufw default deny incoming`

Allow outgoing requests - `sudo ufw default allow outgoing`

Change default port `sudo nano /etc/ssh/sshd_config`

Locate the line `# Port 22`

uncomment the line and change port to 2200

Can also disable root log in in this file

Restard sshd service by running command `service sshd restart`

Can also disable root log in in this file

Set up firewall to allow certain port numbers:

`sudo ufw allow 2200/tcp`

 `sudo ufw allow 80/tcp`

 `sudo ufw allow 123/tcp`

Enable firewall - `sudo ufw enable`


 To log in

 `ssh -i <YOUR SSH KEY> grader@198.199.114.89 -p 2200`



#### configure local timezone to UTC

 `sudo dpkg-reconfigure tzdata`

 select none of above, then UTC



#### Set up uWSGI with nginx

follow instructions on this link:
 https://www.digitalocean.com/community/tutorials/how-to-set-up-uwsgi-and-nginx-to-serve-python-apps-on-ubuntu-14-04#definitions-and-concepts

#### Install git on server

 `apt-get install git`


## Resources to help with project

 Udacity Server Course

Digital ocean tutorial on setting up uwsgi and nginx to server flask applications:

 https://www.digitalocean.com/community/tutorials/how-to-set-up-uwsgi-and-nginx-to-serve-python-apps-on-ubuntu-14-04#definitions-and-concepts
