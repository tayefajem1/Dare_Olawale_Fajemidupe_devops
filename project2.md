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
# Login to mysql-server
  ![image](https://user-images.githubusercontent.com/53397202/190857686-145e6b85-ba35-4ddb-8014-cc8dc81041ad.png)
# Set password before locking the database
  ![image](https://user-images.githubusercontent.com/53397202/190857874-1e90d858-f029-4ba5-8f12-09b4e4b9089c.png)
# Start interactive script
  sudo mysql_secure_installation
  ![image](https://user-images.githubusercontent.com/53397202/190857939-ac5b4620-8ae5-4397-a654-6e3e761b5f22.png)
# Enter pasword for userroot: The password we set for when the mysql is to be secured
  PassWord.1
  # Install php
  sudo apt install php-fpm php-mysql
  ![image](https://user-images.githubusercontent.com/53397202/190861086-f16403f4-89db-4971-bacd-8173f638cb82.png)
### Configuration of nginx  to use php
  # creating root directory for the domain
  sudo mkdir /var/www/projectLEMP
  # Assigning of ownership $USER
  sudo chown -R $USER:$USER /var/www/projectLEMP
  
 ## Open new configuration file in nginx
  sudo nano /etc/nginx/sites-available/projectLEMP
 #/etc/nginx/sites-available/projectLEMP
Paste:
server {
    listen 80;
    server_name projectLEMP www.projectLEMP;
    root /var/www/projectLEMP;

    index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
     }

    location ~ /\.ht {
        deny all;
    }

} 
  # Activate your configuration by linking to the config file from Nginx’s sites-enabled directory:This will tell Nginx to use the configuration next time it is reloaded. You can test your configuration for syntax errors by typing:
  sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/
  sudo nginx -t
 ![image](https://user-images.githubusercontent.com/53397202/190862000-24524f33-f93d-4c7b-9638-4fa283083ad6.png)
 # We also need to disable default Nginx host that is currently configured to listen on port 80, for this run:
  sudo unlink /etc/nginx/sites-enabled/default
  # To relaod
  sudo systemctl reload nginx
  ## Your new website is now active, but the web root /var/www/projectLEMP is still empty. Create an index.html file in that location so that we can test that your new server block works as expected:
 sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html
  ![image](https://user-images.githubusercontent.com/53397202/190863179-493aecf6-3870-4262-ae35-8a45e6c2560b.png)
 # Testing php
 sudo nano /var/www/projectLEMP/info.php
  paste:
  <?php
phpinfo();
http://18.217.25.146/info.php
![image](https://user-images.githubusercontent.com/53397202/190863482-b3312250-acc2-4547-857c-37db46ae549b.png)

![image](https://user-images.githubusercontent.com/53397202/190863797-51cfe637-b599-45af-b8d6-814a55df0e34.png)
# Remove PHP Page when you are done
sudo rm /var/www/your_domain/info.php
# Login to mysql Database and create new database
CREATE DATABASE `example_database`;
The name of the database  `example_database'
![image](https://user-images.githubusercontent.com/53397202/190865137-f12d3ff5-de6b-455c-a21f-0e1ed9fdcb5e.png)
# To create new user on the database: create a new user and grant him full privileges on the database you have just created.
CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'xxxxxxxxx.';
GRANT ALL ON example_database.* TO 'example_user'@'%';
![image](https://user-images.githubusercontent.com/53397202/190865476-d6e82334-1942-4186-954c-347ce9aef30c.png)
![image](https://user-images.githubusercontent.com/53397202/190865552-ec31a6ed-caac-49d7-a77a-57a2e37725c6.png)
# Create TO-DO-LIST (Create new table
![image](https://user-images.githubusercontent.com/53397202/190865943-91d8676f-42c8-4486-bb8e-69da81d2a8a8.png)

CREATE TABLE example_database.todo_list (   
 item_id INT AUTO_INCREMENT,
content VARCHAR(255),
PRIMARY KEY(item_id)
);
Insert values into the table created: INSERT INTO example_database.todo_list (content) VALUES ("My first important item");
Query your table: SELECT * FROM example_database.todo_list;
exit
# create a PHP script that will connect to MySQL and query for your content. Create a new PHP file in your custom web root directory using your preferred editor. We’ll use vi for that:

nano /var/www/projectLEMP/todo_list.php



 
