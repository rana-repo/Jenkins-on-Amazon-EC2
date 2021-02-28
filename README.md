# Jenkins Installation& Configuration on AWS EC2 instance
*******************************************************************

Installation 

1. Lanuch AWS EC2 instance.
# Install java and set path
	  sudo su -
	  yum install java-1.8*
	  java -version
# Steps to set java path permanently
    ls -la
    vi .bash_profile
    JAVA_HOME=/usr/lib/jvm/java-11-amazon-corretto.x86_64/
    PATH=$PATH:$JAVA_HOME:$HOME/bin
# Download jenkins on to EC2 instance.
    yum install wget -y 
    sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat/jenkins.repo
    sudo rpm --import https://pkg.jenkins.io/redhat/jenkins.io.key
	
# Install jenkin
	yum install jenkins -y
# Start jenkins service
	  service jenkins start
	

# Configuration

1. Open default port 8080 in security group. Set Inbound rule and Open port 8080 to all tcp traffic.
2. Login to Jenkins console
#
	<Public-IP>:8080
	Username : admin
	Password location: /var/lib/jenkins/secrets/initialAdminPassword
3. Skip plugins installation (Can be done later)
4. Change admin password
	  admin > configurate > Password
5. Configure java path under jenkins configuration
  	Manage Jenkins > Global Tool Configuration > JDK > Add JAVA_PATH
	
