# WEB STACK IMPLEMENTATATION (LEMP STACK) 
# Deploying a LEMP Stack Application On AWS Cloud

# Project Goal 

The aim of this implementation is to provide a complete and efficient web development environment. With this implementation I will create a robust and high-performance web server environment by making use of **linux** as the operating system, **Nginx** as the web Server, **MySQL** as the database management system, and **PHP** as the server-side scripting langauge.

# Pre-Requisites
1. AWS account free tier account or any other cloud provider like Azure etc.

2.  Create an EC2 instance in AWS or virtual machine in azure or a virtual machine from any other cloud provider of your choice.

3.  Command line terminal (example, terminal, command prompt or shell, Git Bash).

4. Some Knowlege about SSH, prior knowledge about how to SSH into a virtual/remote host/server.

## Definition of Terms 

**LEMP STACK** is a software bundle used for web development and hosting. it is am alternative to the more commonly known LAMP stack, with the main difference being the replacement of Apache web servefr with Nginx (pronounced "engine-x"). **LEMP** stack consists of **Linux**, **Nginx**, **MySQL** and **PHP**. 

**LINUX :** this serves as the operating system, providing a stable and secure foundation for the stack.

**NGINX :** this is a high performance wed server knwon for its efficiency and scalability. Nginx is designed to handle high traffic loads.

**MySQL :** this is a popular relational database management systems used for storing and managing data. 

**PHP** this is a server-side scripting language used for dynamic content generation and interaction with dadtabases. PHP is widely used for web development and is compactible with different frameworks and content management systems.

**`ADDITIONALLY` :** **LEMP stack** offers a lightweight and efficient alternative to LAMP stack, particularly suitable for high-trafficwebsites and applications.

### Preparing pre-requisites

The  frist thing I have to take in this project is to head on to my AWS account, log in and create an EC2 with Ubuntu operating system that will serve as my virtual/remote servr.

![Alt text](<images/Create EC2.jpg>)

IMPORTANT NOTICE : while creating an EC2 instance remember to select region closest to you in you AWS account and also make sure to Save your private key (.pem file) securely and do not share it with anyone! If you lose it, youn will not be able to connect to your server ever again.

### Remotely Connect (SSH) into your EC2 Instance (Virtual Server)

Once I finished creating and lunching my virtual machine (EC2 instance in AWS), next is to shh into my EC2 instance ie to remotely connect to my my ubuntu server. 

I will open my windows terminal and cd into the directory containg my downloaded private key and run the following command substituting my EC2 IP address, EC2 username and my private key appropriately or I can also use the public DNS to connect to my EC2  :

`ssh -i <Your-private-key.pem> ubuntu@<EC2-Public-IP-address>`

in the case of this project I will be the my public DNS which results in the following command below :

`ssh -i "LEMPstack.pem" ubuntu@ec2-35-178-159-55.eu-west-2.compute.amazonaws.com`

![Alt text](<images/ssh into EC2 1.jpg>)
![Alt text](<images/ssh into EC2 2.jpg>)

## Isntalling the Nginx Web Server

step1- To be able to display webpages to our sites I need to install an Nginx server I'll use the apt package managers to install this package.

Being the first time using `apt` for this session. I will do that with the following commands below:

`sudo apt update`
`sudo apt install nginx`

![Alt text](<images/instal nginx.jpg>)
![Alt text](<images/apt update.jpg>)

*note* : Always watchout to input "**Y**" when prompted while the installation was going on.

At this time I will have to vefrify and confirm if the succesfull and that the Nginx is running as a service, by running this command below:

`sudo systemctl status nginx`

![Alt text](<images/nginx status.jpg>)

*Note*: on seeing the "*active(running)"* written with green colour I know that the **nginex** was installed properly and that it is running as a service.

## Configuring Security Group Inbound Rules on EC2 Instance

As we have been able to ssh into our EC2 server via ssh making use of port 22 which is open by default once an EC2 instance is craeated in AWS,
and alos I have been able sucessfully installed and confirmed that my nginx is active and running, now lets confirm if it can be reached over the internet. 

Before I can be able to have access to my nginx server over the internet I will need to open TCP port 80 (http) by editing inbound rule of my EC2 instance to open inbound connection.

![Alt text](<images/edit inbound rule.jpg>)

 I also need to confirm if I can access the default nginx web server block locally in our Ubuntu shell to see if evrything works properly. This can be achieved by using :

`curl http://localhost:80` 

or 

`curl http:??127.0.0.1:80`

![Alt text](<images/curl http ingnx.jpg>)

*note:* the difference from the two commands above is that the first makes use of the DNS name while the second makes use of the IP address, and both actually does the same thing.

Now using the public IP of my EC2 I can now be able to access njinx web server through the internet :

`35.178.159.55:80`

![Alt text](<images/njinx internet access.jpg>)

## *Step 2* : Installing MySQL

Now that I have my **njinx** web server running I need to install my Database management System DBMS to mbe able to store and manage data in a relational database using MySQL. 

Installing my database system using the command below :

`sudo apt install mysql-server`

![Alt text](<images/apt install MySQL.jpg>)

*note* input `Y` when prompted and then press `ENTER`

I will log into MySQL console using the following command :

`sudo mysql`

![Alt text](<images/log in MySQL console.jpg>)

As it is recommended that I run a security script that comes pre-installed wuth MySQL that will remove some insecure default settings and lock down access to your database system.

But then before doing that I need to set **root** user password using mysql_native_password as default authentication method, defining this user's password as `PassWord.1`

I will set this root user password using the command below :

`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`

![Alt text](<images/MySQl root user passwd.jpg>)

After that exit MySQL shell with the commad :

`exit` 

![Alt text](<images/exit MySQl.jpg>)

Using the following command to start the security interactive script : 

`sudo mysql_secure_installation`

![Alt text](<images/secure mysql 1.jpg>)
![Alt text](<images/MySQl root user passwd.jpg>)

To test my settings and know if I am able to log in into MySQL console I will using the following command.

`sudo mysql -p `

![Alt text](<images/test mysql.jpg>)

*notice `-p `flag in this command, which prompted me for the password used after  changing **root** user password*


## *step 3* Installing PHP

Now that I have **Nginx** install to serve content and **MySQL** installed to store and manage data, now I can install **PHP** to process code and generate dynamic content for the web serever. 

 While Apache embeds the PHP interpreter in each request, Nginx requires an external program to handle PHP processing and act as a bridge between the PHP interpreter itself and the web server. This allows for a better overall performance in most PHP-based websites, but it requires additional configuration. I’ll need to install **php-fpm**, which stands for “PHP fastCGI process manager”, and tell Nginx to pass PHP requests to this software for processing. Additionally, you’ll need **php-mysql**, a PHP module that allows PHP to communicate with MySQL-based databases. Core PHP packages will automatically be installed as dependencies.

 To install these 2 packages at once, I will run these commands: 

 `sudo apt install php-fpm php-mysql`

![Alt text](<images/install PHP.jpg>)

## Creating a Web Server Block For our Web Application

When using the Nginx web server, I can create server blocks just like the   virtual hosts in Apache to encapsulate configuration details and host more than one domain on a single server.

In this project we will use **projectlemp** as an example of domain name (server block) . 

Next I will create a directory called projectlemp inside `/var/www/` directory  using the following commands:

`sudo mkdir /var/www/projectlemp`

also for security reasons and as recommended I have to change/assign ownership of the directory(projectlemp) with the $USER environment variable that will refrence my current system user by using the command below:

`sudo chown -R $USER:$USER /var/www/projectlemp`

![Alt text](<images/mkdir chown.jpg>)

Next I will open a new configuartion file in Nginx's sites-avaliable diirectory using the following command :

`sudo nano /etc/nginx/sites-available/projectlemp`

Once the configuration file is open I will go ahead and paste bare-bones confuguration below : 

#/etc/nginx/sites-available/projectLEMP

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

![Alt text](<images/nano projectlemp.jpg>)


To activate my configuration I will have to link it to the config file from Nginx's **sites-enabled**  directory :

`sudo ln -s /etc/nginx/sites-available/projectlemp /etc/nginx/sites-enabled/`

The command above will tell Nginx to use the configuration next time it is reloaded. 

I also used the following command to test my configuration for syntax errors:

`sudo nginx -t`

![Alt text](<images/symbolic link projectlemp.jpg>)

Because the default Nginx server block is configured to listen on port 80 by default,I will have to disbaled it by running the following command :

`sudo unlink /etc/nginx/sites-enabled/default`

After that I will have to reload Nginx to apply the changes by running the command below :

`sudo systemctl reload nginx`

![Alt text](<images/unlink default.jpg>)

So now my newbsites is now active, but the web **/var/www/projectlemp** is still empty. I will have to create an **index.html** file in that location so that I can test that my new server block works as expected :

`sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlemp/index.html`

![Alt text](<images/index.html file.jpg>)

Then after I succesfully created the **index.html** file , I will now go to my browser and try to open my website URL using IP address: 

`http://<Public-IP-Address>:80`
![Alt text](<images/website result.jpg>)

## Serving content using PHP with Nginx

At this piont my LEMP stack is now completely set up . 

I can test it to validate that **Nginx** can correctly hand **.php** files off to your PHP processor.

And to do this I will have to create a test PHP file in my document root by creating and opening a file called **info.php**
within my document root in my text editor using the following the command :

`nano /var/ww/projectlemp/info.php`

Once I create and open the **info.php** file I will input the following valid PHP code that will return information about my server

![Alt text](<images/ls info.php.jpg>)
![Alt text](<images/nano info.php.jpg>)

I can now go to my web browser to access this page by visiting the public domain name or public IP address of my server followed by /info.php :

`http://<server_domain_or_IP>/info.php`

![Alt text](<images/502 Bad gateway.jpg>)

I encountered the error above because the version of PHP that installed in my server is **php7.4** while I have version  to the one I have in my **root** configuration file (projectlemp), so I had to go to my back and edit my **root** configuration file as shown below :

![Alt text](<images/PHP version correction .jpg>)

After the correction, I now can access my PHP page :

![Alt text](<images/php webpage result.jpg>)

So as one of Devops best practice, after checking the relevant information about PHP server through that page, it is recommended that I remove the file I created as it contain sensitve information about your PHP environment and your Ubuntu server. 

To do that I will use the following commands :

`sudo rm /var/www/projectlemp/info.php`

![Alt text](<images/rm php.info.jpg>)

## *step 6* Connecting PHP with MySQL and Fetching Content :
 
 At this stage I will create a test database(DB) with simple "To do list" and configure access to it, so the **Nginx** websites would be able to querry data from the DB and display it.

*note* At the time of this writing, the native MySQL PHP library `mysqlnd` doesn't support caching_sha2_authentication, the default authentication method for MySQL8. We;ll need to create a new user with the mysql_native_password anthentication method in order to be able tom connect the MySQL database from PHP.

I will create database named **projectLEMP_database** and user named **first_user**

I will first , connect to MySQL console using the root account using the following command :

`sudo mysql -p`

*note* notice the inclusion of **`-p`** in this command which prompted me to input password and that is because I have previously changed the **root password**

![Alt text](<images/mysql log in.jpg>)

Since I am now logged into MySQL console, I will go ahead to create a new databse with the follwing command :

`CREATE DATABASE projectLEMP_database;`

since I have created my new Database I will also go ahead to create a new user with the following command :

`CREATE USER 'first_user'@'%' IDENTIFIED WITH mysql_native_password BY 'moNey.2023';`

Then I will also go ahead to grant this user (first user) permission over the **projectLEMP_database** with the follwing command: 

`GRANT ALL ON projectLEMP_database.* TO 'first_user'@'%';`

after all that I will exit MySQL shell with the follwing command :

`exit`

![Alt text](<images/database&database user.jpg>)

To test if the user has the proper permissions, I can do that by logging in to the MySQL console again , this time using the custom user credentials as follows :

`mysql -u first_user -p`

*note* the -p flag will prompt for password used when creating the **first_user** user

After logging into the MySQL console, I will confirm that I have access to the **projectLEMP** database using the following command :

`SHOW DATABASE;`

![Alt text](<images/login nad show databases.jpg>)

Creating a test table and named it todo_list. I will the follwing statement from my MySQL console :
`CREATE TABLE projectLEMP_database.todo_list (item_id INT AUTO_INCREMENT,content VARCHAR(255),PRIMARY KEY(item_id));`
![Alt text](<images/Create database table .jpg>)

Since I have succefully created my tabel, I will then add some few content in the test table by running and repeating the following statment while changing the content inside the bracket each time :

`INSERT INTO projectLEMP_database.todo_list (content) VALUES ("Get up from bed");`

![Alt text](<images/my todo list.jpg>)


After I have finshed inserting some content into the test tabel, I can now go further to confirm that data was successfully saved to my table by running the following command :

`SELECT * FROM projectLEMP_database.todo_list;`

![Alt text](<images/Result of my todo.list.jpg>)

Next is to create a PHP script that will connect to MySQL and querry for content.

I will create the new PHP file in my custom web root directory and input the PHP script inside the file using the command below :

`nano /vary/www/projectlemp/todo_list.php`

![Alt text](<images/nano edit todo.php.jpg>)

After I have editted and saved the file I will now head on to my browser access this page by visiting the domain name or public IP address that I configured for my website followed by 

`/todo_list.php` 

![Alt text](<images/database webpage result.jpg>)



