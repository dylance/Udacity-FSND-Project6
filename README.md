create droplet on digital ocean

hostname: UdacityServer

ip: 198.199.114.89

 remotely connect to server - `ssh root@198.199.114.89`

### Update Server
 check ubuntu for updates - `sudo apt-get update`
 
 get updates - `sudo apt-get upgrade`

### Create New User

Create User -  `sudo adduser grader`

Give user sudo privelages - `sudo nano /etc/sudoers.d/grader`
 add text to grader file in sudoers.d -  `grader ALL=(ALL) NOPASSWD:ALL`

 exit server `exit`

### Create SSH keys



Create new Key `ssh keygen`  
save key in desired location with desired name


 log on to server as grader  
 go to root directory - `cd ~`
 make directory to store public key - `mkdir .ssh`
make file with authorized keys - `touch .ssh/authorized_keys`
open nano to edit file -  `nano .ssh/authorized_keys`
 copy paste text from pub key onto .ssh/authorized keys
give only user, grader, access to .ssh folder. `chmod 700 .ssh`
change permission for authorized keys to read only for other users - `chmod 644 .ssh/authorized_keys`

 exit server and close ssh connection `exit`

log onto server -  `ssh grader@198.199.114.89 -i ~/Desktop/id_rsa`

### enable  forced key based authentication

18. `sudo nano /etc/ssh/sshd_config`
19. change PasswordAuthentication to no
20. restart configeration service so it uses new changes. `sudo service ssh restart`


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
