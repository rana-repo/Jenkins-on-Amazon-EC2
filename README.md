# Jenkins Installation& Configuration on AWS EC2 instance
*******************************************************************

# Installation 

1. Lanuch AWS EC2 instance.
2. Install java and set path
#
	  sudo su -
	  yum install java-1.8*
	  java -version
3. Steps to set java path permanently
#
	whereis java or find / -name javac
	ls -la
	vi .bash_profile
	JAVA_HOME=/usr/lib/jvm/java-11-amazon-corretto.x86_64/
	PATH=$PATH:$JAVA_HOME:$HOME/bin
4. Download Jenkins on to EC2 Instance using yum.
  #  
    yum install wget -y 
    sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat/jenkins.repo
    sudo rpm --import https://pkg.jenkins.io/redhat/jenkins.io.key
	
5. Install Jenkin
#
	yum install jenkins -y
6. Start Jenkins Service
#
	service jenkins start
7. Setup Jenkins to start at boot
#
	systemctl enable jenkins
	

# Configuration

1. Open default port 8080 in security group. Set Inbound rule and Open port 8080 to all tcp traffic.
2. Login to Jenkins console
#
	<Public-IP>:8080
	Username : admin
	Password location: /var/lib/jenkins/secrets/initialAdminPassword 
	(Remove this file once you create admin credentials)
3. Skip plugins installation (Can be done later)
4. Change admin password
  #
	  admin > configurate > Password
5. Configure java path under jenkins configuration
  #
	Manage Jenkins > Global Tool Configuration > JDK > Add JAVA_PATH
	
