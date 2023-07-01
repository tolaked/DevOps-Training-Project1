# Project1

# STEP 1

- Installing nginx web server
  - run _sudo apt update_ to update server's index package
  - run _sudo apt install apache2_ to install apache2
    ![Step 1](step1.png)

# STEP 2

- Installing MYSQL
  - run _sudo apt install mysql-server_ to install sql server
  - run _sudo mysql_ to login to mysql console
  - run **_ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';_** to set password for the root user using mysql\*native_password as default authentication method.
  - exit MYSQL shell with \_msql > exit
  - run _sudo mysql_secure_installation_ to start the interactive script running and follow prompt to validate password.
  - With the steps above MYSQL server should be installed and secured.
    ![Step 2](step2.png)

# STEP 3

- Installing PHP
  - run _sudo apt install php libapache2-mod-php php-mysql_ to install php, libapache2-mod-php, php-mysql at once.
  - run _php -v_ to confirm php is installed.
    ![Step 3](step3.png)

# STEP 4

- Creating a virtual host for your website using apache

  - run _sudo mkdir /var/www/projectlamp_ to create a directory for projectlamp
  - run _sudo chown -R $USER:$USER /var/www/projectlamp_ to assign ownership of the current system user.
  - run _sudo vi /etc/apache2/sites-available/projectlamp.conf_ to create and open a new configuration file in Apache’s sites-available using vi. This command will create a blank file. Paste the snippet below. Hit escape, type wq to save and exit the file.
  - run _sudo ls /etc/apache2/sites-available_ to view the new file in sites-available directory.
  - run _sudo a2ensite projectlamp_ to use a2ensite to enable virtual host.
  - run _sudo a2dissite 000-default_ to disable apache's default website(optional).
  - run _sudo apache2ctl configtest_ to make sure your configuration file doesn’t contain syntax errors.
  - run _sudo systemctl reload apache2_ reload Apache so these changes take effect.
  - The new website is now active, but the web root /var/www/projectlamp is still empty. Create an index.html file in that location so that we can test that the virtual host works as expected:
  - run _sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html_
  - visit _http://<Public-IP-Address>:80_ in the browser to see the website.

    ```
        <VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
        </VirtualHost>

    ```

  ```

  ```

![Step 4](step4.png)

# STEP 5

-Enabling php on the website

- If we want to serve index.php file as the root file, run _sudo vim /etc/apache2/mods-enabled/dir.conf_ and change the content to the snippet below. Save and close

```
<IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
```

- run _sudo systemctl reload apache2_ to reload apache for the changes to take effect.
- run _vim /var/www/projectlamp/index.php_ to create index.php file in the web root folder. Paste the snippet below in the file.

```
<?php
phpinfo();
```

- save and close the file, refresh the page and you should see the image below.
  ![Step 5](step5.png)
