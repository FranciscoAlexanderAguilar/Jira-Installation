Lets Install MySQL as I mentioned we need to have MySQL setup and running before installing Jira.

First check if you system is up to date.

$ sudo apt-get update

if you get something like:

![image](https://user-images.githubusercontent.com/45543969/220735806-e854b477-aa1c-4720-bf91-73f4a1fff0ef.png)

Then proceed and install MySQL

$ sudo apt install mysql-server

provide root password and you will see the following screen.

![image](https://user-images.githubusercontent.com/45543969/220824052-cee7b2e4-d9cb-47de-ae3a-1538b90d355a.png)

say Y to proceed to install MySQL Server

After the installation is complete check status of MySQL with the command

$ systemctl status mysql

where

systemctl is a command used to control the systemd system and service manager in Linux
It allows to start, stop, restart, enable, and disable system services.

![image](https://user-images.githubusercontent.com/45543969/220825513-3755ae68-ea95-4a9a-882f-31903375f321.png)

if you Install MySQL in a local host you may notice the issue show in the image bellow

![image](https://user-images.githubusercontent.com/45543969/220825831-94900c52-95c1-4140-a026-1df7bccaa499.png)

even if you use the -p flag  we gotthe Access Denied error message. the question is why?

The root user may be configured to use an authentication plugin that requires additional steps to authenticate. 
For example, in MySQL 8.0 and later (which is my case) use a default authentication plugin called caching_sha2_password,
which requires clients to send an additional authentication packet after connecting to the server. If you are using 
an older client that does not support this plugin so that is why you got that error.

Solution:
Login in to Mysql with sudo privileges

$ sudo mysql -u root -p

![image](https://user-images.githubusercontent.com/45543969/221029825-74078091-2165-4a69-a864-846f55fee31d.png)

After you are in Run the following SQL command to change the root user's authentication plugin:

mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'YOUR NEW PASSWORD HERE';

Now we can Run mysql_secure_installation

When prompt for the root password use password set for user root mysql. and say Y for Validate password component

![image](https://user-images.githubusercontent.com/45543969/221031582-58ffc480-b9c0-4d9c-837b-6288665e3c36.png)

As a side note: if you go and configure mysql_secure_installation before changing the password for user root in 
MySQL you will get an error like:
"Failed! Error: SET PASSWORD has no significance for user 'root'@'localhost' as the authentication method used doesn't store authentication data in the MySQL server. Please consider using ALTER USER instead if you want to change authentication parameters."

After that Respond Yes to all the questions that will appear while the script is running.

![image](https://user-images.githubusercontent.com/45543969/221033306-88736e99-527d-4727-b065-b4e38c3a70c2.png)

Now Lets create a database user and database for Jira.

