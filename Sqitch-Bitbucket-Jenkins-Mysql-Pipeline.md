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
## Bitbucket
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
6. Now we are ready to run the queries using "add" function
```console
pankaj@pankajv:~/star_db$ sqitch add query -n 'General query'
Created deploy/query.sql
Created revert/query.sql
Created verify/query.sql
Added "query" to sqitch.plan
```
In above command we are adding file named "query" to store or db query in it

7. We have to open the file deploy/query.sql and write the query like below
```console
pankaj@pankajv:~/star_db$ vim deploy/query.sql
```
```console
-- Deploy star_db:query to mysql

BEGIN;

CREATE TABLE user_data  
(email varchar(30),    
 name varchar(50),    
 mobile varchar(50)  
);

COMMIT;
```
In between BEGIN; and COMMIT; we have to write our query
Here we are creating table in star_db database which is already there on mysql server

8. Now just add and commit push the files
```console
pankaj@pankajv:~/star_db$ git add .
pankaj@pankajv:~/star_db$ git status 
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   deploy/query.sql
	new file:   revert/query.sql
	modified:   sqitch.plan
	new file:   verify/query.sql

pankaj@pankajv:~/star_db$ git commit -m "creating user_data table"
[master b7dacce] creating user_data table
 4 files changed, 26 insertions(+)
 create mode 100644 deploy/query.sql
 create mode 100644 revert/query.sql
 create mode 100644 verify/query.sql
pankaj@pankajv:~/star_db$ git push
Enumerating objects: 14, done.
Counting objects: 100% (14/14), done.
Delta compression using up to 8 threads
Compressing objects: 100% (9/9), done.
Writing objects: 100% (9/9), 1.01 KiB | 517.00 KiB/s, done.
Total 9 (delta 1), reused 0 (delta 0)
To https://bitbucket.org/pankajrdbreak/star_db.git
   fadc4a4..b7dacce  master -> master
   ```
Note: sqitch.plan file will store all the things you did step by step
```console
pankaj@pankajv:~/star_db$ cat sqitch.plan
%syntax-version=1.0.0
%project=star_db
%uri=https://pankajrdbreak@bitbucket.org/pankajrdbreak/star_db/

sqitchuser 2022-07-11T06:35:48Z pankaj,,, <pankaj@pankajv> # Creates an application user.
query 2022-07-11T06:40:21Z pankaj,,, <pankaj@pankajv> # General query
```
## Jenkins Setup
9. Now we will configure Jenkins to push db changes from repo to mysql server
-> go to your jenkins and add new item to create job
![image](https://user-images.githubusercontent.com/76647860/178212831-7db1e2a7-0c23-45e2-b400-a24d7c443c7b.png)

![image](https://user-images.githubusercontent.com/76647860/178213122-e8d5aeff-cd63-4371-a1ef-c7387f517da8.png)

![image](https://user-images.githubusercontent.com/76647860/178465108-b7f21cb3-62ec-4ce2-84e2-52d8be8e0df4.png)

![image](https://user-images.githubusercontent.com/76647860/178465185-2b20ef1b-b3b1-43c0-ab6c-ef1c34a057b7.png)

![image](https://user-images.githubusercontent.com/76647860/178465264-2a667045-bf94-4dcd-a55c-4bd158e88eb1.png)

![image](https://user-images.githubusercontent.com/76647860/178465356-d2a7fa03-5d8f-407a-9c4e-1a1465f6adb0.png)

![image](https://user-images.githubusercontent.com/76647860/178465507-41fbf6f4-8ce1-435e-81ec-58b230a06dda.png)


