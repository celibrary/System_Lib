# Installing WordPress

## Before Installation

Open VM. Run -
 
`sudo apt update`
`sudo apt clean`
`sudo apt autoremove`

## Check Versions of Software

`php --version`
 
Return is 8.3.6
 
`mysql --version`

Return is ver. 8.0.45
These both meet installation requirements.

## Add additional PHP Modules

`sudo apt install php-curl php-xml php-imagick php-mbstring php-zip php-intl`

Return OK

`sudo systemctl restart apache2`

Typed with a space between apache and 2 and got an error message. Corrected error and return OK.

`sudo systemctl restart mysql`

Return OK

## Download and Extract

`cd /var/www/html`
`sudo wget https://wordpress.org/latest.zip`
If you go to the WordPress website and hover over download will give webaddress for install
`sudo unzip latest.zip`
Got an error message.  Retried 4 times and then went to video where I learned we needed to install zip program.

`sudo apt install unzip`
Return OK
`sudo unzip latest.zip` 
Return OK
 
Remove latest.zip file because we no longer need.  WordPress directory is visible via `ls`
In my attempt to unzip earlier I downloaded lastest.zip twice so had to remove both files.

`sudo rm latest.zip`
`sudo rm latest.zip.1`

## Create Database and User

Log in as the MySQL root user -

`sudo mysql -root`

Create a new user for WordPress DB, User: wordpress-

`create user 'wordpress'@'localhost' identified by 'password;`

My password is Word5!moon

Create a new DB 

`create database wordpress;`

Grant privileges -

`grant all privileges on wordpress.* to 'wordpress'@'localhost';`

We are giving privileges to our new database to the user we created.

`show databases;`

Returns are good, Quit -

`\q`

## Configure wordpress with our new user information.

Go to wordpress directory - /var/www/html/wordpress
`ls`
will see a configure file - wp-config-sample-phpwe need to copy this file and alter it.
`sudo cp wp-config-sample.php wp-config.php`

Check that our copy is there using `ls`

Open file -

`sudo nano wp-config.php`

Enter the new database, user, and password we created.  Look for define.
'wordpress'
'wordpress'
'password'

At the end we entered command in case permissions were not working in lab environment.
`define('FS_METHOD','direct');`

Good to change defaults to add barrier to hacking.  They will assume defaults.

Save and close Nano file.

## Finish

Go to my URL.  Change the directory to wordpress.  Will get sign-on page. Completed with the following -
<<<<<<< HEAD



Email: cel@uky.edu




=======
>>>>>>> 7357c2f (WordPress.md)
