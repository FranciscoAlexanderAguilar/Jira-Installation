REMEMBER THE DB NAME, USER NAME AND PORT NUMBER. will be need it to connect to Jira.

Lets create a user we will use to connect Jira. run the command

$ mysql -u root -p

notice how we can run it now with no issues.

![image](https://user-images.githubusercontent.com/45543969/221036704-0e632aee-ef28-4f0d-a802-40413b2db92d.png)

To create a user run the SQL query:

CREATE USER 'jirauser' IDENTIFIED BY 'PASSWORD';

Take into account that because VALIDATE PASSWORD COMPONENT to test the strength of passwords if 
a weak an error will let us know if our password was accept it or not.

Now create the Database that will store Issues in Jira. one important thing is
the DB MUST HAVE CHARATER SET OF UTF8 use the SQL query:

CREATE DATABASE jiradb CHARACTER SET utf8mb4 COLLATE utf8mb4_bin;

Where 

CREATE DATABASE: is the SQL command used to create a new database in a MySQ.
CHARACTER SET utf8mb4: this sets the character set to utf8mb4, which is a character encoding scheme that can store
              a wider range of characters than the traditional utf8 character set. utf8mb4 is recommended for databases
              that need to store characters from non-Latin.
COLLATE utf8mb4_bin: sets the collation for the database to utf8mb4_bin, which specifies a binary collation that sorts 
        strings based on the numeric value of each character's binary representation.


Ok lets continue, now set the permission to connect to the database, and permission to create and populate tables.
with the SQL query:

to be continue..




