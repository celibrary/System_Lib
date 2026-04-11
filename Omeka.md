### Omeka Installation

PHP & MySQL were checked that they were updated
Did not install PHP extensions
`cd /var/www/html`
`sudo apt install imagemagick`

`sudo a2enmod rewrite`
Return OK
`sudo systemctl restart apache2`
Return OK
`sudo wget https://omeka.org/classic/download/`
Return OK
`unzip omeka`
`sudo nano db.ini`
Replaced with database name of omeka, user, and password.  Left directory as omeka-3.2. 
`sudo mysql uroot`
`create user 'omeka'@'localhost' identified by 'password`
`create database Omeka`
`grant all privileges on omeka.* to 'omeka'@'localhost';`
Return OK
`cd /var/www/html/omeka-3.2`
`sudo chmod -R g+w *`
restart
`sudo systemctl restart apache2`
`sudo systemctl restart mysql`

Error when going to my website.
went back and installed php extensions
`sudo apt install mysqli.php`
OK
`sudo apt install exif`
tried
adding `define('FS_METHOD','direct');` didn't help.  Removed.

from searching web, tried to edit (first find!) .htaccess.  Permission denied.
from Candace.
`cd /etc/apache2`
`sudo nano apache2.conf`  fogot tilde was a text editor and needed to use nano
edit /var/www to change 'AllowOverride' to 'All'

returns OK

tried again to edit .htaccess so I could a more informative error message on  Omeka

This time it worked
`sudo nano .htaccess`

Removed #  before  "SetEnv"

This time it worked.
 
