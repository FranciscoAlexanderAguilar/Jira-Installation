On ubuntu check if $JAVA_HOME is set.

$ echo $JAVA_HOME

If a path is not returned then means we need to setup the java home variable.

![image](https://user-images.githubusercontent.com/45543969/220449141-298a8b17-35d2-476b-91ab-3b3e4cecd07f.png)


JDK 17 according to jira documentation is supported with jira 9.6 so proceed to install JDK 17
with the following command 

$ sudo apt install openjdk-17-jdk

![image](https://user-images.githubusercontent.com/45543969/220457436-e0dc7a63-95ec-4c32-84d4-38a95f537600.png)

Proceed and say Y to proceed with the installation. if everything goes well you should see something 
similar to the image below.

![image](https://user-images.githubusercontent.com/45543969/220458662-2cdc0965-7fb1-414e-addc-69040e7f0570.png)

Lets check is java was properly installed with the following command:

$ java - version

and it should output the following:

![image](https://user-images.githubusercontent.com/45543969/220459830-5ff83122-1bde-479f-a92a-38e19e89e38f.png)

Let finish the job because if you run the following command:

$ echo $JAVA_HOME

No output should be display since we just install Java but the JAVA_HOME variable has not been set yet.

![image](https://user-images.githubusercontent.com/45543969/220464510-2a71be35-1c6c-4a07-8313-6098e0a718d0.png)

and this step will depend on if you want to setup the JAVA_HOME variable just for a specific user or all users in the system.
In this example I will do it for all users.

$ vi /etc/profile
You can use you prefer editor like nano for example.

at the end of the file on its own line add the following:

export JAVA_HOME=/usr/lib/jvm/java-version-1  (where "java-version-1" will be the version of java you installed)
export PATH=$JAVA_HOME/bin:$PATH

you should end up with something like the image below 

![image](https://user-images.githubusercontent.com/45543969/220480426-11a24fab-b1f5-43b1-a02f-0234c6bbbc22.png)

if you run the command 

$ echo $JAVA_HOME

the output will be the same as the first time we tried. That is because we need to restart ubuntu.
and after restarting ubuntu we can run the echo $JAVA_HOME and the output should be like:

/usr/lib/jvm/java-1.17.0-openjdk-amd 

