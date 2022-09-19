# MEAN STACK
# updating in ubuntu machine
sudo apt update
![image](https://user-images.githubusercontent.com/53397202/191009540-4cbb6710-0710-4133-9b6a-a11b35a3c39c.png)
# Upgrade the server
sudo apt upgrade
# Add certificate
sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates
![image](https://user-images.githubusercontent.com/53397202/191010890-ce66e7b0-fbe1-43ea-a677-ce935ee13922.png)
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash 
![image](https://user-images.githubusercontent.com/53397202/191011161-1c3450f7-987e-4701-97b4-1a92403106f3.png)

# Install node.js
sudo apt install -y nodejs
![image](https://user-images.githubusercontent.com/53397202/191011697-1ed27314-ede3-4793-ab77-88553faf120b.png)
# Install MongoDB
MongoDB stores data in flexible, JSON-like documents. Fields in a database can vary from document to document and data structure can be changed over time. For our example application, we are adding book records to MongoDB that contain book name, isbn number, author, and number of pages.
mages/WebConsole.gif
*sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6*
![image](https://user-images.githubusercontent.com/53397202/191012105-c65a696d-50aa-458d-9bad-a3f916405e80.png)
*echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list*
![image](https://user-images.githubusercontent.com/53397202/191012348-4fe87326-1b9d-4d59-b5cb-65f8f331a81d.png)
# Install MongoDB
sudo apt install -y mongodb
![image](https://user-images.githubusercontent.com/53397202/191042498-9556360c-4856-4adb-bc03-83f5691132c5.png)
# Start The server
 sudo service mongodb start
 ![image](https://user-images.githubusercontent.com/53397202/191042964-1cbbc135-8454-4c8e-9730-9df35c3c813a.png)
# Verify that the service is up and running
sudo systemctl status mongodb
![image](https://user-images.githubusercontent.com/53397202/191043324-35420920-d21f-431c-9581-3695c3f476fe.png)
# Install npm – Node package manager.
First install aptitude on the machine: sudo apt-get install aptitude
Use aptitude to install npm: sudo aptutide install -y npm 
sudo aptutide install -y npm
# Install body-parser package
sudo npm install body-parser
![image](https://user-images.githubusercontent.com/53397202/191045589-655f5d24-ac85-43e6-b1d7-85f45a76a3ba.png)
