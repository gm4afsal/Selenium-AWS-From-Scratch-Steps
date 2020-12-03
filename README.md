# Selenium-AWS-From-Scratch-Set Up-Steps


Selenium- Maven – AWS EC2- Jenkins


Jenkins configuration details


Install Jenkins in AWS EC2

https://www.youtube.com/watch?v=8s71mIOpOAI


Manage Jenkins: Global Tool Configuration:


JDK:
JAVA_HOME
/usr/lib/jvm/java-1.8.0-openjdk

Git:
Name: Default
Path to Git Executable: git

Maven:
Name: M2_HOME
Maven_Home: /opt/maven/apache-maven-3.6.3

Manage Plugins:
Maven Integration plugin
Maven Invoker plugin
GitHub Integration Plugin


Item:
Configure:
Pre Steps:
Execute Shell: chmod 777 /var/lib/jenkins/workspace/IBAutomation/drivers/chrome/linux_chromedriver

Build:
Root POM: AWSAutomation/pom.xml
Goals and options: clean install










AWS Configuration details
=========================



Login and create a key, keep it in local system.

chmod 400 /Users/myUser/Akey/jenkinsKey.pem 

ssh -i "/Users/ myUser /Akey/jenkinsKey.pem" ubuntu@ec2-3-1x4-xxx-x9.us-east-2.compute.amazonaws.com

sudo yum update

Install Java (JVM and JDK)
sudo yum install java-1.8.0 (verify if this command install JDK also. If installed correctly command javac -version will give result)

Set path:
find /usr -name java
Copy Path from line which has /Bin
Copy only till “/usr/lib/jvm/java-1.8.0-openjdk”
https://stackoverflow.com/questions/24641536/how-to-set-java-home-in-linux-for-all-users




Set Path
==========


$vim .bash_profile
JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk
M2_HOME=/opt/maven/apache-maven-3.6.3
M2=$M2_HOME/bin

PATH=$PATH:$JAVA_HOME:$M2_HOME:$M2:$HOME/bin

Set Key Permissions:

sudo chmod 600 /Users/myUser /AWS/Keys/jenkinsKey.pem



Before connecting:
Security Groups: 
Add Inbound Rule: Custom TCP, Port 8080, 0.0.0.0/0, ::/0

Use IPv4 Public IP with Port like : 18.1xxx.1x.1xx:8080

EC2 connection: ssh -i "/Users/ myUser /AWS/Keys/jenkinsKey.pem" ec2-user@ec2-18.1xxx.1x.1xx.us-east-2.compute.amazonaws.com



Terminal Cheat Sheet:
cd /var/lib/jenkins/.m2/repository/com/disney/gqe/SeleniumUtils/0.0.2-14.0.0.0/
cd /var/lib/jenkins/workspace/

mvn install:install-file  -Dfile=/var/lib/jenkins/.m2/repository/com/disney/gqe/SeleniumUtils/0.0.2-14.0.0.0/SeleniumUtils-0.0.2-14.0.0.0.jar  -DgroupId=com.disney.gqe -DartifactId=SeleniumUtils -Dversion=0.0.2-14.0.0.0 -Dpackaging=jar



