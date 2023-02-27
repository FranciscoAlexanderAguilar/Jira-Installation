Time to install Jira

Download it from:
https://product-downloads.atlassian.com/software/jira/downloads/atlassian-jira-software-9.6.0.tar.gz

$ sudo wget https://product-downloads.atlassian.com/software/jira/downloads/atlassian-jira-software-9.6.0.tar.gz

![image](https://user-images.githubusercontent.com/45543969/221382403-959705b4-7d5d-41c1-aba5-33e88e6d53e4.png)

<h3>Now let's create the installation directory to install jira in /opt/</h3>

$  sudo mkdir jirasoftware

![image](https://user-images.githubusercontent.com/45543969/221387218-ed0ced11-7e7f-4a33-9766-3a8cc4e3e581.png)

Now extract the Jira tar.gz file to the installation directory.

$ sudo tar -xzf atlassian-jira-software-9.6.0.tar.gz -C jirasoftware 

x: Extract files from an archive
z: Filter the archive through gzip to decompress it
f: Use the following archive file
-C tells tar to change the directory before performing the extraction.  

![image](https://user-images.githubusercontent.com/45543969/221387808-d620b8a6-0b47-4fcc-ba39-1560954b65cc.png)

Next Igive the Jira dedicated user read, write and execute permission to the jirasoftware directory.

$ sudo chown -R jira jirasoftware

chown: is used to change the ownership of files and directories.
-R flag: is used to change the ownership of files and directories recursively.

$ sudo chmod -R u=rwx,go-rwx jirasoftware

chmod: is used to change the file permissions of a file or directory.
u=rwx: The u specifies the owner of the file or directory. rwx specifies the permissions 
that are being granted to the owner, which in this case are read, write, and execute.

go-rwx: The go specifies the permissions being granted to the group and others. -rwx specifies 
the permissions that are being removed from the group and others, which in this case are read,
write, and execute.

<h3>Create the home directory</h3>

This directory should be separate to your installation directory

![image](https://user-images.githubusercontent.com/45543969/221395531-e76b37cc-34b5-4c80-88ff-345f34062dc5.png)

Give the Jira user read, write and execute permissions to the jira-home directory.

chown -R jira jira-home
chmod -R u=rwx,go-rwx jira-home

![image](https://user-images.githubusercontent.com/45543969/221395666-f69182e3-f680-4c86-af1a-9f7b8d2fb66b.png)

Lets tell Jira where to find your jira-home directory when it starts up

use any editor you prefer and edit:

$ nano /opt/jirasoftware/atlassian-jira-software-9.6.0-standalone/atlassian-jira/WEB-INF/classes/jira-application.properties









