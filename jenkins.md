Login to aws -> Instances -> Launch instance -> Amazon Linux AMI... -> Next -> Next -> Next -> Next -> Create a new security group
Name: week2-day6-security-group, Description: jenkins
Type: HTTP, Protocol: TCP, Port Range: 80, Source: 0.0.0.0/0
Type: Custom TCP, Protocol: TCP, Port Range: 8080, Source: 0.0.0.0/0
Type: SSH, Protocol: TCP, Port Range: 22, Source: 130.208.240.8/32 (MyIP)
Review and Launch -> Launch
Create a new key pair -> week2-day6-key-pair -> Download Key Pair -> Launch Instances -> View Instances
Notice the Instance ID (i-09c99c28131db8e8a) and Public DNS (ec2-34-248-245-199.eu-west-1.compute.amazonaws.com)

chmod 400 week2-day6-key-pair.pem

ssh -i week2-day6-key-pair.pem ec2-user@ec2-34-248-245-199.eu-west-1.compute.amazonaws.com

sudo yum install java-1.8.0
sudo yum remove java-1.7.0-openjdk

sudo yum update
sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat-stable/jenkins.repo
sudo rpm --import http://pkg.jenkins-ci.org/redhat-stable/jenkins-ci.org.key
sudo yum install jenkins
sudo service jenkins start
sudo chkconfig jenkins on

sudo yum install -y ecs-init
sudo gpasswd -a jenkins docker
sudo service docker start
sudo chkconfig docker on
sudo yum install git

sudo su -s /bin/bash jenkins
cd /var/lib/jenkins/
ssh-keygen
cat .ssh/id_rsa.pub

cat /var/lib/jenkins/secrets/initialAdminPassword

exit