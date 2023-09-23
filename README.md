# jenkins-ansible-tomcat-deployment

Here is a summarized and rephrased version of your Git readme note:

**Setting Up Jenkins on AWS:**

1. Access your AWS console to set up a Jenkins server.

2. Ensure port security is configured for port 8080.

**Installing Jenkins:**

- Use the provided script to install Jenkins on your server. The script is as follows:

```bash
#!/bin/bash
# Install Jenkins on RHEL 7/8, CentOS 7/8, or Amazon Linux OS (T2 Medium)
# Execute this script as user-data when launching your EC2 VM.

# Update the system
sudo yum update -y
sudo timedatectl set-timezone America/New_York
sudo hostnamectl set-hostname jenkins
sudo yum install wget -y
sudo wget -O /etc/yum.repos.d/jenkins.repo \
  https://pkg.jenkins.io/redhat/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat/jenkins.io-2023.key
sudo yum upgrade -y

# Install required dependencies
sudo yum install java-11-openjdk -y
sudo yum install git wget jenkins -y
sudo systemctl daemon-reload

# Start Jenkins
sudo systemctl enable jenkins
sudo systemctl start jenkins

# Check Jenkins status
sudo systemctl status jenkins
sudo su - ec2-user
echo "Jenkins installation completed."
systemctl status jenkins
```

- Confirm that Jenkins is running with the command: `systemctl status jenkins`.

- Obtain the server's IP address using `curl ifconfig.me`.

- Retrieve the Jenkins initial admin password with `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.

**Jenkins Configuration:**

- Access the Jenkins GUI and enter the initial admin password.

- Fill in the required details and install recommended plugins.

- Navigate to "Manage Jenkins" and click on "Plugins."

- Install the following plugins: Maven Integration (for building applications), Deploy to Container (for package deployment), Jacoco (code coverage), Audit Trail (log auditing), and Email Extension (for email notifications).

- Set up SMS notification using your email.

- Install the Ansible plugin for deploying Tomcat applications.

- Install the Docker plugin for building Tomcat servers.

**Credential Configuration:**

- In "Manage Jenkins," configure credentials by adding access keys, secret keys, and IDs for Ansible to deploy Tomcats within the Jenkins slave.

**Continuous Integration Testing:**

- In the system settings, install Maven, Ansible, and SonarQube for continuous integration testing and email notifications.