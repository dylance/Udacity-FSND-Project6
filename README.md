# Configuring Server for a Python Flask Application

## About

this is the final project for the Udacity Full Stack Nanodegree. The goal
is to securely put the fourth project onto a web server with firewalls enabled and root login disabled. The fourth project is a flask application that gets data from a sql database. the project can be seen here:

IP Address Used: 198.199.114.89

## Software Installed on Server

-Python 2
- git
-nginx
PostgreSQL

## Steps to Configure Server

create droplet on digital ocean

Create a hostname for you server.

my server's name hostname: UdacityServer

My server's ip: 198.199.114.89

remotely connect to server - `ssh root@198.199.114.89`

above line uses ssh keys already set up on my local machine and with digital ocean

### Update Server
 check ubuntu for updates - `sudo apt-get update`

 get updates - `sudo apt-get upgrade`

### Create New User

Create User -  `sudo adduser <YOUR USER NAME>`

Give user sudo privelages - `sudo nano /etc/sudoers.d/<YOUR USER NAME>`

Add this text to user's file in sudoers.d -  `<YOUR USER NAME> ALL=(ALL) NOPASSWD:ALL`

 exit server `exit`

### Create SSH keys

On your local machine:

Create new Key `ssh-keygen`  

save key in desired location with desired name

log on to server as grader  

go to root directory - `cd ~`

make directory to store public key - `mkdir .ssh`

make file with authorized keys - `touch .ssh/authorized_keys`

open nano to edit file -  `nano .ssh/authorized_keys`

copy paste text from public key on your local machine to  .ssh/authorized keys on your server

give only the user you created access to .ssh folder. `chmod 700 .ssh`

change permission for authorized keys to read only for other users - `chmod 644 .ssh/authorized_keys`

exit server and close ssh connection `exit`


log onto server for me -  `ssh grader@198.199.114.89 -i ~/Desktop/id_rsa`

log onto server -  `ssh grader@198.199.114.89 -i <your ssh key>`

### enable  forced key based authentication

`sudo nano /etc/ssh/sshd_config`

 change PasswordAuthentication to no

 restart configeration service so it uses new changes. `sudo service ssh restart`


### Set up Firewall


checks firewall status - `sudo ufw status`

-deny all incoming requests

firewall is not enabled yet so this is ok. - `sudo ufw default deny incoming`

 allow outgoing requests - `sudo ufw default allow outgoing`

 change default port `sudo nano /etc/ssh/sshd_config`

locate the line `# Port 22`

uncomment the line and change port to 2200

can also disable root log in in this file

restard sshd service by running command `service sshd restart`

can also disable root log in in this file


`ssh grader@198.199.114.89 -i ~/Desktop/id_rsa`

`-i ~/Desktop/id_rsa` is just where I have my private key stored instead of default location.


set up firewall to allow certain port numbers:

`sudo ufw allow 2200/tcp`

 `sudo ufw allow 80/tcp`

 `sudo ufw allow 123/tcp`

enable firewall - `sudo ufw enable`


 to log in

 `ssh -i ~/Desktop/id_rsa grader@198.199.114.89 -p 2200`

`-i ~/Desktop/id_rsa` is just where I have my private key stored instead of default location.


### configure local timezone to UTC

 `sudo dpkg-reconfigure tzdata`

 select none of above, then UTC



 #### set up uwsgi with nginx

### install git

 `apt-get install git`



 ### Links to help with project

 Udacity Server Course


 https://www.digitalocean.com/community/tutorials/how-to-set-up-uwsgi-and-nginx-to-serve-python-apps-on-ubuntu-14-04#definitions-and-concepts
