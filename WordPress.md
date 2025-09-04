# Project: Deploying a LAMP Stack and WordPress on an Ubuntu Server VM
## Project overview
Wordpress is an open source Content Management System (CMS) written in PHP, using the MySQL database management system, allowing users to build dynamic web and blogs.
Content Management System (CMS) is a software that stores data such as text, photos, music, documents, etc and is made available on the website.
Wordpress was released in 2003 and announced as open source in 2009.
This is a personal hands-on project that demonstrates the process of building a complete web server from scratch using the LAMP (Linux, Apache, MySQL/MariaDB, PHP) architecture on an Ubuntu Server 22.04 virtual machine. The final objective is to successfully deploy and host a functional WordPress website.
This project showcases fundamental and core skills for a System Engineer, including:
-   Linux System Administration.
-   Setting up and managing a virtualized environment.
-   Installing and configuring network services (Web Server, Database).
-   Implementing basic security measures (Firewall, Database Hardening).
-   Deploying a real-world web application.
## 2. Technology Stack

-   **Operating System:** Ubuntu Server 22.04 LTS
-   **Virtualization:** Oracle VM VirtualBox
-   **Web Server:** Apache2
-   **Database:** MariaDB
-   **Scripting Language:** PHP 8.1
-   **Application:** WordPress
-   **Firewall:** UFW (Uncomplicated Firewall)
-   **Client:** Windows 11 & Command Prompt (for SSH)

## 3. Deployment Steps
### 3.1: Setting Up the Ubuntu Server VM
- A new virtual machine was created in VirtualBox.
- The network was configured in **Bridged Adapter** mode to allow the VM to get an IP address from the local network.
- Installed Ubuntu Server 22.04 and the OpenSSH server for remote management.
![VM](https://github.com/hoangmanhdungg/Mini-Project/blob/main/Images/Screenshot%202025-09-04%20150449.png?raw=true)
### 3.2: Installing and Configuring Apache2 Web Server
- Executed command:
```
sudo apt-get install apache2
```
- **Result:** Successfully accessed the default Apache2 landing page from the host machine's browser.'
![Default Apache Page](https://github.com/hoangmanhdungg/Mini-Project/blob/main/Images/Screenshot%202025-09-04%20005613.png?raw=true)

### 3.3: Installing and Securing MariaDB Database
- Executed command:
```
sudo apt install mariadb-server -y
```
- Run the interactive security script to set the root password and apply security best practices.
```
sudo mysql_secure_installation
```
- **Result:** Completed the security script, hardening the database installation.
![DTB](https://github.com/hoangmanhdungg/Mini-Project/blob/main/Images/Screenshot%202025-09-04%20010430.png?raw=true)

### 3.4: Installing PHP
- Install PHP along with essential modules required by WordPress for database connectivity, image processing, and more.
```
sudo apt install php libapache2-mod-php php-mysql php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip -y
```
- To verify the installation, a temporary info.php file was created and accessed.
```
Create the test file
sudo nano /var/www/html/info.php

(File content: <?php phpinfo(); ?>)

Clean up after verification
sudo rm /var/www/html/info.php
```
- **Result:** The PHP Info page loaded correctly, confirming that Apache is processing PHP files.
![DTB](https://github.com/hoangmanhdungg/Mini-Project/blob/main/Images/Screenshot%202025-09-04%20010812.png?raw=true)

### 3.5: Deploying Wordpress
- Log into MariaDB
```
sudo mysql -u root -p
```
- Create the database
```
CREATE DATABASE wordpress_db;
```
- Create user
```
CREATE USER 'wordpress_user'@'localhost' IDENTIFIED BY 'Your_Strong_Password';
```
- Grant permissions to users on the database:
```
GRANT ALL PRIVILEGES ON wordpress_db.* TO 'wordpress_user'@'localhost';
```
- Downloaded and extracted the WordPress source code, then moved it to the webroot.
```
cd /tmp
curl -O https://wordpress.org/latest.tar.gz
tar -xzvf latest.tar.gz
sudo cp -R /tmp/wordpress/* /var/www/html/
```
- Assigned the correct file ownership to the web server user.
```
sudo chown -R www-data:www-data /var/www/html/
```
- The final installation steps were completed through the user-friendly web interface.
![alt text](images/05-wordpress-setup-screen.png)
![alt text](images/05-wordpress-setup-screen.png)

## 4. Final Result
The project was successfully completed, resulting in a fully functional WordPress website running on a self-hosted LAMP stack, accessible from the local network.
![alt text](images/06-wordpress-final-site.png)










