# SBJM Database Pipeline

## Install Sqitch 
1. On local machine install sqitch
```console
pankaj@pankajv:~/star_db$ sudo apt install sqitch
[sudo] password for pankaj: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  libalgorithm-c3-perl libappconfig-perl libb-hooks-endofscope-perl libb-hooks-op-check-perl libclass-c3-perl libclass-c3-xs-perl libclass-inspector-perl libclass-load-perl
```
2. Create Bitbucket repo for database project
For this tutorial I have created below repository in bitbucket
https://pankajrdbreak@bitbucket.org/pankajrdbreak/star_db.git

3. Clone this repo on your local machine
4. Then inside cloned folder give the following command to initialize sqitch 
```console
pankaj@pankajv:~/star_db$ sqitch init star_db --uri https://pankajrdbreak@bitbucket.org/pankajrdbreak/star_db/ --engine mysql
Created sqitch.conf
Created sqitch.plan
Created deploy/
Created revert/
Created verify/
```
5. By default, Sqitch will read sqitch.conf in the current directory for settings. But it will also read ~/.sqitch/sqitch.conf for user-specific settings. Since MySQL’s mysql client is not in the path on my system, let’s go ahead an tell it where to find the client on our computer.
```console
pankaj@pankajv:~$ sqitch config --user engine.mysql.client /usr/bin/mysql
```
And let’s also tell it who we are, since this data will be used in all of our projects:
```console
pankaj@pankajv:~$ sqitch config --user user.name 'pankaj vare'
pankaj@pankajv:~$ sqitch config --user user.email 'pankaj.vare@samco.in'
pankaj@pankajv:~$ cat ~/.sqitch/sqitch.conf
[engine "mysql"]
	client = /usr/bin/mysql
[user]
	name = pankaj vare
	email = pankaj.vare@samco.in
```
