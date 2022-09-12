# Project 1
connecting to window
cd Downloads (The .pen file is downloaded to Downloads)
ssh -i <private-key-name>.pem ubuntu@<Public-IP-address>
![image](https://user-images.githubusercontent.com/53397202/189669747-47f82c55-85c8-4e9d-b0ae-7fffdf0daebd.png)
# update a list of packages in package manager
sudo apt update
![image](https://user-images.githubusercontent.com/53397202/189671645-a8134b8e-d497-479f-891c-3ac6c961f93a.png)
#run apache2 package installation
sudo apt install apache2
  ![image](https://user-images.githubusercontent.com/53397202/189672099-3085c642-81c5-454c-a6a6-223c44e7043e.png) (apache 2 installed)
# To verify that apache2 is running as a Service in our OS, use following command
sudo systemctl status apache2
![image](https://user-images.githubusercontent.com/53397202/189672645-432f4f5c-f294-4bb3-8d1e-460cab613264.png)
# Server is running and I want to access it locally
  curl http://localhost:80 or curl http://127.0.0.1:80 (Using these 2 commands to access our apache2 locally)
# Configure security group (SG) of EC2 instance Type: HTTP, Protocol: TCP and port range:80 on inbound rules
Access apache2 on the internet through http://<Public-IP-Address>:80 curl -s http://169.254.169.254/latest/meta-data/public-ipv4
or  http://X.XX.XX.XX:80
![image](https://user-images.githubusercontent.com/53397202/189676341-57db58c5-383a-42a1-9ae3-53bf6395e7c1.png)
# Installing Mysql server on Ubunbutu machine
  sudo apt install mysql-server
 # Log to mysql-server after installation
 use: sudo mysql
 ![image](https://user-images.githubusercontent.com/53397202/189679661-d846f938-757b-4ba7-82a4-7d909b2dd6d3.png)
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1'; (Setting Password)
  To exit: mysql> exit
 ![image](https://user-images.githubusercontent.com/53397202/189680575-61002d17-a972-4261-924e-e1b837d8e871.png)
 To start interactive script: sudo mysql_secure_installation (use PassWord. 1)
 ![image](https://user-images.githubusercontent.com/53397202/189683349-44751bd8-b65e-424a-91e7-fc31f3a7b263.png)
![image](https://user-images.githubusercontent.com/53397202/189684094-31c9ff00-14b5-4c66-a274-09836fbc7750.png)
# To test if you can login to mysql server using your new password
  sudo mysql -p (It ask for the new password)
 ![image](https://user-images.githubusercontent.com/53397202/189684784-558dee68-3b02-4988-a318-132861544fee.png)
# Installation of PHP on your Ubuntu machine
  sudo apt install php libapache2-mod-php php-mysql
  # to confirm if php is installed after installation
  run : php -v (php -version)
  ![image](https://user-images.githubusercontent.com/53397202/189686040-649f8f6b-4e1e-446b-a200-ad8991b2733e.png)

  #### CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE
  #Creating directory projectlamp
  sudo mkdir /var/www/projectlamp
  # Assign of Ownership
  sudo chown -R $USER:$USER /var/www/projectlamp
  # creating and open new configuration file
  sudo vi /etc/apache2/sites-available/projectlamp.conf
  # To access the new file
  sudo ls /etc/apache2/sites-available
  # To enable the virtual host
  sudo a2ensite projectlamp
  ![image](https://user-images.githubusercontent.com/53397202/189688815-faa0c8b3-09b7-44a0-92c7-396521f0dd91.png)
  # To disable the virtual host
  sudo a2dissite 000-default
![image](https://user-images.githubusercontent.com/53397202/189689258-3e664878-c779-4183-875c-1e1dbbedfd24.png)
  # To make sure no error in the configuration
  sudo apache2ctl configtest
  ![image](https://user-images.githubusercontent.com/53397202/189689606-1fee18aa-da1c-4219-8a27-b0ecae7f430a.png)
  # Reload apache 2
  sudo systemctl reload apache2
  # Create site in the web root cos it empty
sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html 
  # run you website again on internet
  ![image](https://user-images.githubusercontent.com/53397202/189690874-2ebcfc10-01bb-4cfe-8b5d-b42b21253a34.png)
# ENABLE PHP ON THE WEBSITE
sudo vim /etc/apache2/mods-enabled/dir.conf
<IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
  # Reload apache 2 again
  sudo systemctl reload apache2
  #Create a new file named index.php inside your custom web root folder:
  <?php
phpinfo();

![image](https://user-images.githubusercontent.com/53397202/189695177-1d44cb56-5f9f-4fdd-8fd0-2e110f04685d.png)
# Remove PHP file
sudo rm /var/www/projectlamp/index.php



