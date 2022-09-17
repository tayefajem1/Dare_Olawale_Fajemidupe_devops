## Project LEMP
#Login to my Ubunbutu machine
ssh -i <private-key-name>.pem ubuntu@<Public-IP-address>
![image](https://user-images.githubusercontent.com/53397202/190856424-7e99942a-13f3-41c8-b63b-a7506bd62a77.png)
#Updated ubuntu server: 
  sudo apt update
 # Nginx installation
  sudo apt install nginx
  ![image](https://user-images.githubusercontent.com/53397202/190856697-6723b939-2370-4ab4-aca3-5e1b353caa11.png)
# start nignx
  sudo systemctl status nginx
  ![image](https://user-images.githubusercontent.com/53397202/190856816-29f1a2c5-cb29-4152-8164-a0d07a6267a1.png)
# To check on local host
 curl http://localhost:80
  ![image](https://user-images.githubusercontent.com/53397202/190856910-2e23bc3a-6794-4560-b6ec-327c5f712d27.png)
# To check if it is running on the internet
 [ http://](http://<Public-IP-Address>:80)
  # installation of mysql
  sudo apt install mysql-server
