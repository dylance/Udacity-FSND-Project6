create droplet on digital ocean

add SSH keys for dylan

hostname: UdacityServer

ip: 198.199.114.89

1. ssh root@IP

2. `sudo apt-get update`
3. `sudo apt-get upgrade`
4. `sudo adduser grader`
5. `sudo nano /etc/sudoers.d/grader`
6. add text `grader ALL=(ALL) NOPASSWD:ALL`
7. copy key file to desktop.
8. `ssh keygen`  save new file


9. log on to server as grader  
10. `cd ~`
11. `mkdir .ssh`
12. `touch .ssh/authorized_keys`
14. `nano .ssh/authorized_keys`
13. copy paste text from pub key onto .ssh/authorized keys
14. `chmod 700 .ssh`
15. `chmod 644 .ssh/authorized_keys`

16. exit server

17. `ssh grader@198.199.114.89 -i ~/Desktop/id_rsa` to log on server

enable  forced key based authentication

18. `sudo nano /etc/ssh/sshd_config`
19. change PasswordAuthentication to no
20. restart configeration service to it uses new changes. `sudo service ssh restart`


set up firewall
`sudo ufw status` - checks firewall status
21. `sudo ufw default deny incoming` -deny all incoming requests
 firewall is not enabled yet so this is ok.
22. `sudo ufw default allow outgoing` - allow outgoing requests

23a. change default port
`ssh grader@198.199.114.89 -i ~/Desktop/id_rsa`
change line that says ssh to desired port.



23. `sudo ufw allow 2200/tcp`
24. `sudo ufw allow www`
25. `sudo ufw enable`
`sudo ufw allow 2200/tcp
 sudo ufw allow 80/tcp
 sudo ufw allow 123/tcp
 sudo ufw enable`


 to log in

 ssh -i ~/Desktop/id_rsa grader@198.199.114.89 -p 2200



 configure local timezone to UTC

 `sudo dpkg-reconfigure tzdata`
 select none of above, then UTC
