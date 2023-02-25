REMEMBER THE DB NAME, USER NAME AND PORT NUMBER. will be need it to connect to Jira.

Lets create a user we will use to connect Jira. run the command

$ mysql -u root -p

notice how we can run it now with no issues.

![image](https://user-images.githubusercontent.com/45543969/221036704-0e632aee-ef28-4f0d-a802-40413b2db92d.png)

Thinking about security here, when creating a user is a good practice to specify the host from where the user will connect.
with the following SQL query:

CREATE USER 'username' IDENTIFIED BY 'YOUR_PASSWORD_HERE'; 

it will do the job, but if only use 'username' a wild card will be use and is generally considered bad security practice
because it allows anyone from any IP address to connect to the MySQL server, as long as they provide valid credentials.
This can make your MySQL server vulnerable to various types of attacks, including brute-force attacks and SQL injection attacks.

so this is a better query:

CREATE USER 'jirauser'@'localhost or IP' IDENTIFIED BY 'YOUR_PASSWORD_HERE';

Take into account that VALIDATE PASSWORD COMPONENT is enabled (in case you don't remember we ran mysql_secure_installation)
to test the strength of passwords if the password is weak an error will let us know if our password pass the test or not


Now create the Database that will store Issues in Jira. one important thing is
the DB MUST HAVE CHARATER SET OF UTF8 use the SQL query:

CREATE DATABASE jiradb CHARACTER SET utf8mb4 COLLATE utf8mb4_bin;

![image](https://user-images.githubusercontent.com/45543969/221289150-88350d5e-60e4-4892-a5b0-a8df8dc002ab.png)


Where 

CREATE DATABASE: is the SQL command used to create a new database in a MySQL.

CHARACTER SET utf8mb4: this sets the character set to utf8mb4, which is a character encoding scheme that can store
              a wider range of characters than the traditional utf8 character set. utf8mb4 is recommended for databases
              that need to store characters from non-Latin.
              
COLLATE utf8mb4_bin: sets the collation for the database to utf8mb4_bin, which specifies a binary collation that sorts 
        strings based on the numeric value of each character's binary representation.


Ok lets continue, now set the permission to connect to the database, and permission to create and populate tables.
with the SQL query:

GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,REFERENCES,ALTER,INDEX on jiradb.* TO 'jirauserdb'@'localhost or IP';

Its time to edit the file my.cnf that is usually located at /etc/mysql in my case i will use vi.

$ sudo vi my.cnf

![image](https://user-images.githubusercontent.com/45543969/221380948-668e6114-8add-4f5d-b3ae-f4bf85e9a30d.png)

Set the default storage engine to InnoDB: character_set_server=utf8mb4
Specify the character set used by the database server: character_set_server=utf8mb4
Set the default row format to DYNAMIC: innodb_default_row_format=DYNAMIC
Specify the value of innodb_log_file_size to be at least 2G: innodb_log_file_size=2G

Save the changes and lets work with the JDBC driver(conector).




