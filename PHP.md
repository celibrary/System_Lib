

# Installing PHP
## First ran
'''
sudo apt update
'''
'''
sudo apt upgrade
'''
terminal successfully updated.
## PHP Install
'''
sudo apt install php libapache2-mod-php
'''
Realized need to run entire command at the same time
'''
sudo apt install php libapache2-mod-php
sudo systemctl restart apache2
'''
'''
php -v
'''
successful
'''
systemctl status apache2
'''
Apache running, but didn't get a return to cutiewindriver.. couldn't figure out how to exit            

'''
cd /var/www/html/
sudo nano info.php
'''
<?php
phpinfo();
?>
'''
Then visited from browser. Had to fix / PHP Version 8.3.6
Then delete to not expose info
sudo rm /var/www/html/info.php
'''
cd /etc/apache2/mods-available/
'''
sudo cp dir.conf dir.conf.bak
'''
sudo dir.conf

'''
apachectl configtest
'''
sudo systemctl reload apache2
'''
systemctl status apache2
'''
cd /var/www/html
'''
sudo nano index.php
'''
copy and pasted code from textbook.
success with new webpage



### Problems
Tried /var/www/html/$
Did not work
Backed up and repeated steps to make sure Apache running.  It is.  I don't need $

Did something wrong when creating PHP file.   Repeated instructions and now I see the correct output of PHP on my webpage. That was because I deleted it.
## Reflection
1) This is the first week I started with opening the terminal, then the markdown file.
2) I am not sure what the difference is between doing an update and doing an upgrade.
3) /var/www.html/$ is our root directory
4) After updating Apache always check that it is running OK that syntax OK.
