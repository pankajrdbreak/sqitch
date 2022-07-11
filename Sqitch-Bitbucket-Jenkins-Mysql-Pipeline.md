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

