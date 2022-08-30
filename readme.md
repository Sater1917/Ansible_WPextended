This playbook will install a WordPress  on an Ubuntu machine
A virtualhost will be created with the options specified in the `vars/default.yml` variable file.
By default, playbook run by root user. Tested on Hetnzer Cloud servers (CX11).
If you see error
ERROR! couldn't resolve module/action 'community.general.snap'.
Please:
1. Update ansible
2. Install core collections:
ansible-galaxy collection install community.general 
ansible-galaxy collection install community.mysql

Check variables:
- `mysql_`: DB, user and passwords forMySQL.
- `http_host`: your domain name. Must be set!!!!!
- `http_conf`: the name of the configuration file that will be created within nginx. Default WP.conf

Security update:
In this installation WP closed by HTTP auth (dev/dev).
Reason: block access to bots to improve SEO and reduce the likelihood of hacking.

Also in script added DEV SSH key.
Also configure backup to run once per day to save DB dump.
Warning:
Before run scripts, set ALL IP and SSH keys!! !!!!!
secureIP: need set before run playbook!! 
Format: AllowUsers *@65.108.52.8 *@31.202.175.251  <-!!!!!!!!!!!!!!!!!!!!!!!!!!!!
Where * present user name.


Quick Steps:

shell
nano vars/default.yml
---
mysql_root_password: "mysql_root_password"
http_host: "your_domain" -- !!!Need change to real path!!!
http_conf: your_domain.conf or WP.conf
sshkey: ```  -DEV SSH key, that added to server


Run the Playbook
Simple run:
./run.sh
```
Playbook install php8.1, Nginx with config for WP, create databse and grant all needed.
Security:
SSH port redirect to 1234;
added SSH key to root user.

Also Install certbot and run it.
First play ping the server for checking connection.


