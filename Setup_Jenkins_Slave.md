# Configure Jenkins Slave on AWS

# Prerequisites:

1. Jenkins Master (Running)
2. Launce an EC2 Slave Node with
   - Security group with port 8080 
   - Install java v1.8.x and Set the JAVA_HOME path 


# Setup Jenkins Slave 

1. Create user 
#
    useradd slave-01

2. Create SSH keys
#
    sudo su - jenkins-slave-01
    ssh-keygen -t rsa -N "" -f /home/slave-01/.ssh/id_rsa
    
    Note: The private and public keys will be created at these locations `/home/jenkins-slave-01/.ssh/id_rsa` and `/home/jenkins-slave-01/.ssh/id_rsa.pub`
    
    cd .ssh
    cat id_rsa.pub > authorized_keys
    chmod 700 authorized_keys


# Configuration on Master

Below commands copy Slave node's public key[id_rsa.pub] to Master Node's known_hosts file
#
    mkdir -p /var/lib/jenkins/.ssh
    cd /var/lib/jenkins/.ssh
    ssh-keyscan -H SLAVE-NODE-PRIVATE-IP >>/var/lib/jenkins/.ssh/known_hosts
    chown jenkins:jenkins known_hosts
    chmod 700 known_hosts

# Next step is to Configuring Slave on Jenkins using Manage Jenkins
#
    Manage Jenkins > Manage Nodes > New Node

    Name : Slave
    Description : Jenkins Slave 01
    # of Executors : 5
    Remote root directory : /home/slave-01
    Labels : Test
    Usage : Use this node as much as possible
    Launch method : Launch agent via SSH
    host : add private ip address of the server
    credentials : add 
        Domain:
        Kind:
        Username:
        Private Key: Enter directly
To Copy private key from Slave server
#
    sudo su -slave-01
    more /.ssh/id_rsa 
