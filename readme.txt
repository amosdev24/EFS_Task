#!/bin/bash
# Update the system packages
sudo yum update -y

# Install Apache for Amazon Linux
sudo yum install httpd -y

# Install EFS and NFS utilities for Amazon Linux
sudo yum -y install amazon-efs-utils
sudo yum -y install nfs-utils

# Create the directory for the website content
sudo mkdir -p /var/www/html/

# Create a simple HTML file
echo "<h1> I'm you're, Jesus. Ill be with you always</h1>" | sudo tee /var/www/html/index.html

# Mount the EFS file system (replace the fs ID with your own)
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-01a846d0717dbeee9.efs.us-east-1.amazonaws.com:/ /var/www/html

echo "<h1> Your Code or Project Details Here!!</h1>" | sudo tee /var/www/html/index.html

# Start Apache service
sudo systemctl start httpd

# Enable Apache to start on boot
sudo systemctl enable httpd

# Check the status of the Apache service
sudo systemctl status httpd
