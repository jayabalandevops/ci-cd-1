# CI-CD-1 project 1 [sri ram](http://google.com)
# Web Application in CI-CD

This is a simple web application using java and jsp.
This is used in the demonstration of development of java web applications. 
  
  Below are the steps required to get this working on a base linux system.
  
  - Install RHEL8 in aws
  - Install and Configure java, maven, jenkins, tomcat
  - Start tomcat and jenkins
  - Install and Configure Web Server as a second instance
  - Start Web Server
   
## 1. Provision and Install RHEL8 in aws
  
  Provision an instance with RHEL8

    yum -y install java-1.8* maven git

   
## 2. Install and Configure tomcat
    
 Install tomcat
       
    yum -y install wget
    wget http://apachemirror.wuchna.com/tomcat/tomcat-8/v8.5.49/bin/apache-tomcat-8.5.49.tar.gz
    tar xzvf apache-tomcat-8.5.49.tar.gz
    mkdir /opt/servers
    chown -R devuser:devuser /opt/servers
    mv apache-tomcat-8.5.49 /opt/servers/tomcat8
    vi .bash_profile
       JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.232.b09-2.el8_1.x86_64
       export JAVA_HOME
       CATALINA_HOME=/opt/servers/tomcat8
       export CATALINA_HOME
       PATH=$JAVA_HOME/bin:$PATH:$CATALINA_HOME/bin
       export PATH
     :wq
     

## 3. Start tomcat Service
  - Start the tomcat service
    
        vi /opt/servers/tomcat8/conf/tomcat-users.xml
          edit the user with the following roles 
          manager-gui, manager-jmx, manager-status, manager-script roles
        :wq
        
        catalina.sh start

    
## 4. Install and Configure Jenkins Server

Install Jenkins

    wget http://mirrors.jenkins.io/war-stable/latest/jenkins.war
    mv jenkins.war /opt/servers/tomcat8/webapps
    browse with url - localhost:8080/jenkins
    copy paste the initialadminpassword from the file .jenkins/secrets/initialadminpassword file
    and select the default plugins to install and create a new user
    

- In global configuration tool, add JAVA_HOME and Maven path
- Install additional plugins 
- Test the free-style-job with hello-world text.


## 5. Git clone the Web App

Git clone the simple web app, in local machine using gitbash.

    git clone https://github.com/jayabalandevops/jjn.git
    modify the index.jsp
    cd jjn
    git add .
    git commit -m "modified index.jsp" 
    git push -u origin master

## 6. Launch another instance and install java and tomcat for Web Server

Start web server

    catalina.sh start

    
## 7. Jenkins Job

Create a new free style job

    choose maven project, say ok.
    configure the job
    select git as SCM and provide the github https URL
    
    
## 6. Test

Open a browser and go to URL

    http://ip:8080/jjn/index.jsp
