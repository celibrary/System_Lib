                                                
# Koha Installation

This post documents adding the open source ILS Koha to my virtual machine.  This required the establishment of a new instance with more memory.

## Set-up of new VM
Review documentation

        1. Go to gcloud account, go to my project.
        2. Create Instance
        3. Change name of instance
        4. Use default Region and Zone
        5. Verify E2 (low cost) selected
        6. Machine needs to be e2-medium (2vcpu, 1 core, 4GB memory)
        7. Go to Networking, check allow HTTP traffic
        8. Go to Network Tag, add koha-staff-8080 then hit enter, next add koha-opac-8081 then enter
        9. Go to OS and Storage and change to Ubuntu 24.04 LTS - ERROR  message that I need the Ubuntu 80x-- fo>
        10. Changed storage from 10 to 20GB
        11. Create instance

### Installing firewalls

        1. Click on hamburger
        2. Click on VPC Network - left side navigation panel
        3. At top of page choose Create a Firewall Rule
        4. Add name - koha-staff-8080
        5. Add description Open prot 8080 for the Koha staff interface
        6. Next to Targets, click on Specified target tags
        7. In target tags, add koha-staff-8080        8. In the source IPv4 ranges change to 0.0.0.0/0 - ERROR message need to enter range, entered 0.0.0.0/0>
        9. Click on Specified protocols and ports
        10. Click on TCP
        11. Enter 8080 in the Ports Box
        12. Click on Create
        13. Repeat/ create a second firewall ule for 8081, koha-opac-8080

## Install Prep
 Prep

`sudo update`
repeat with upgrade, autoremove, and clean

`tmux`
not installed
`sudo apt install tmux`
Will help during long install to not lose progress. Can use `tmux attach`

## Add Koha Repository

will need to sync to remote repositories

`sudo apt install apt-transport-https ca-certificates curl`
`sudo mkdir -p --mode=0755 /etc/apt/keyrings`
`sudo curl -fsSL https://debian.koha-community.org/koha/gpg.asc -o /etc/apt/keyrings/koha.asc`

Become root user:
`sudo su`
All returns OK

```
tee /etc/apt/sources.list.d/koha.sources <<EOF
Types: deb
URIs: https://debian.koha-community.org/koha/
Suites: 25.05
Components: main
Signed-By: /etc/apt/keyrings/koha.asc
EOF
```
Viewed with-
`cat /etc/apt/sources.list.d/koha.sources`
Looks OK
Use `exit` to leave root account.

### Install MariaDB

`sudo apt update`
`sudo apt install mariadb-server`

Returns OK

### Install Koha

`sudo apt update`

Review information on Koha package -
`apt show koha-common`

`tmux`
`sudo apt install koha-common`
As with most of the installs, select Y to continue install

Configuration
Need to always make a copy of important files like config files when prior to editing.

`sudo cp /etc/koha/koha-sites.conf /etc/koha/koha-sites.conf.backup`
ERROR - typo in koha, retyped, OK.

ERROR - nano not installed in new instance -

`sudo apt install nano`
`sudo nano etc/koha/koha-sites.conf.backup`
At the end of Intraport = add 8080.  At the end of OPACport add 8081.
Returns OK

Apache2 Configurations

`sudo a2enmod rewrite cgi headers proxy_http`
`sudo systemctl restart apache2`
Return OK

`sudo cp /etc/apache2/ports.conf /etc/apache2/ports.conf.backup`

At the top under Listen 80, add:

Listen 8080
Listen 8081

Save and close.  Returns OK.

### Create Koha Instance

`sudo koha-create --create-db bibliolib`
`sudo systemctl restart apache2`

`sudo a2dissite 000-default` turns off www document root for Koha.
`sudo a2enmod deflate` turns on network compression.
`sudo a2ensite bibliolib` enables new bibliolib library.

Reload Apache

`sudo systemctl reload apache2`
`sudo systemctl restart apache2`

### Web Installer

`sudo koha-passwd bibliolib`
Recorded Username and Password elsewhere.

Go to URL.  Went through install.  Created Administrator Identity.  Information stored elsewhere.  Created defaults of sample library, patron, etc.  Also created a test patron.

### Public OPAC

I then visited my OPAC using my VM IP with :8081 on the end.  Looks OK.
I then visited my Koha staff interface and added my OPAC url to System Preferences, OPACBaseURL.  Save.

## Reflection

This was the most complicated install, yet.  I am really happy that it seemed to go smoothly.  All problems were straighforward.  Much more could be done in Koha, Omeka, and on my WordPress site, but the basics are there. 





