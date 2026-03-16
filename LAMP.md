
# Set-up MySQL
## First things
	-`sudo apt update`
	-`sudo apt upgrade`
	-'sudo apt autoremove` helps clean out files you don't need
	-`sudo apt clean`

## Install MySQL 
	`sudo apt install mysql-server`
	`mysql  --version' version details
	`systemctl status mysql`  - return is active
	`sudo mysql_secure_installation` Yes, set password to low

### Login to mysql
	`sudo mysql -u root` now see mysql>
	`show databases;` all mysql commands end in ;
	
### Quit mysql, return to Basg shell
	`\q`

### Create mysql user
	`create user 'opacuser'@'localhost' identified by '123horses'
Return of **Query OK** = successfully executed

### Create Database
	`create database opacdb default character set utf8mb4 collate utf8mb4_0900_ai_ci;`
UTF-8 Supports Universal Characters
utf8mb4 supprts range of Unicode
ai = accent insensitive
ci = case insensitive
	`show databases;`
	`grant all privileges on opacdb.* to 'opacuser'@'localhost';`

### Make return more informative
	`\q`
	`nano ~/.bashrc`
At bottom of file add
	`export MYSQL_PS1="[\d]> "`
save and exit
source file
	`source ~/.bashrc`
### To switch to the database
	`use opacdb;`
### Setting up a table
	`create table books (
	id int unsigned not null auto_increment,
	author varchar(150) not null,
	title varchar(150) not null,
	copyright year not null,
	primary key (id)
);`

### Add data to table
	`insert into books (author, title, copyright) values
	('Jennifer Egan', 'The Candy House', '2022');`

Each row/r4ecord in parenthesis, separated by comma

### View table
	`select * from books;`

Everything is working well to this point.

### SQL commands
	-alter
	-describe
	-update
	-delete (will take whole row)
	-insert (add data)

## Install PHP / MQSQL connection

	`sudo apt install php-mysql'
### Restart
	`sudo systemctl restart apache2`
	`sudo systemctl restart mysql`

## Authenticate PHP, Allow Apache to Read (not others)

	`cd /var/www`
	`sudo touch login.php`
	'sudo chmod 640 login.php`
	'sudo chown :www-data login.php'
	`ls -l login.php`
	`sudo nano login.php`
`ls -l` will show owner and group owner,  user owner only read , write

### Add credentials

	`<?php // login.php
	$db_hostname = "localhost";
	$db_database = "opacedb";
	$db_usernam = "opacuser";
	$db_password = "123horses";
	?>`

## Create PHP website file

	`cd /var/www/html`
	`sudo nano opac.php'

large php file.  could not see all of text to copy over on laptop. Copied with mouse. save and exit.

## Go to webapage and view new data ADDED

# Summary
Webpage not working.  Something went wrong between adding credentials and adding the php file.   Very frustrating,not sure how to fix.
POsted in class questions.

"PHP Warning:  Undefined variable $db_username in /var/www/html/opac.php on line 21
PHP Fatal error:  Uncaught mysqli_sql_exception: Access denied for user ''@'localhost' (using password: YES) in /var/www/html/opac.php:21
Stack trace:
#0 /var/www/html/opac.php(21): mysqli->__construct()
#1 {main}
  thrown in /var/www/html/opac.php on line 21


	1) Re-did credential step & PHP login steps
	2) re-did PHP file step.  THis time used copy button in textbook.
	3) ran `sudo php -f /var/www/login.php` - no message
	4) ran `sudo php -f /var/www/html/opac.php` - no message

Everything finally worked.
php text
'<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MySQL Server Example</title>
</head>
<body>

    <h1>A Basic OPAC</h1>
    <p>We can retrieve all the data from our database and book table using a couple of different queries.</p>

    <?php
    // Load MySQL credentials securely
    require_once '/var/www/login.php';

    // Enable detailed MySQL error reporting
    mysqli_report(MYSQLI_REPORT_ERROR | MYSQLI_REPORT_STRICT);

    // Establish database connection
    $conn = new mysqli($db_hostname, $db_username, $db_password, $db_database);

    if ($conn->connect_error) {
        die("Connection failed: " . $conn->connect_error);
    }

    echo "<h2>Query 1: Retrieving Publisher and Author Data</h2>";

    // Query using prepared statement
    $stmt = $conn->prepare("SELECT publisher, author FROM books");
    $stmt->execute();
    $result = $stmt->get_result();

    while ($row = $result->fetch_assoc()) {
        echo "<p>Publisher " . htmlspecialchars($row["publisher"]) .
             " published a book by " . htmlspecialchars($row["author"]) . ".</p>";
    }

    $stmt->close();

    echo "<h2>Query 2: Retrieving Author, Title, and Date Published Data</h2>";

    $stmt2 = $conn->prepare("SELECT author, title, copyright FROM books");
    $stmt2->execute();
    $result2 = $stmt2->get_result();

    while ($row = $result2->fetch_assoc()) {
        echo "<p>A book by " . htmlspecialchars($row["author"]) .
             " titled <em>" . htmlspecialchars($row["title"]) .
             "</em> was released in " . htmlspecialchars($row["copyright"]) . ".</p>";
    }

    $stmt2->close();
    $conn->close();
    ?>

</body>
</html>

` 
 
