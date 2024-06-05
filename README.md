# Install-Ngnix-on-Azurevm

Step 1: Create Azure VM using Linux distribution OS in the Azure Portal
* Configure the VM as per the requirements

Step 2: Login to the Azure VM using SSH 
* Make sure Port 22 (SSH) is enabled in the Azure VM’s network security group**
* Use terminal for Linux/MacOS, Putty for Windows or Azure Cloud Shell*

Step 3: Run the below script to install Nginx

#!/bin/bash
# Update the package list
sudo apt-get update

# Install Nginx
sudo apt-get install -y nginx

# Start and enable Nginx to run at boot
sudo systemctl start nginx
sudo systemctl enable nginx

# Get the hostname of the machine
HOSTNAME=$(hostname)

# Modify the default Nginx welcome page to display hostname
sudo sed -i "s/Welcome to nginx\!/Welcome to \$HOSTNAME/" /var/www/html/index.nginx-debian.html

# Replace placeholder with actual hostname in the html
sudo sed -i "s/\$HOSTNAME/$HOSTNAME/" /var/www/html/index.nginx-debian.html

# Restart Nginx to apply changes
sudo systemctl restart nginx

echo "Nginx has been installed and configured on $HOSTNAME"

Step 4: Test VM’s Public IP address in a web browser 
* If it doesn’t work re-check the ports enabled in network security group
