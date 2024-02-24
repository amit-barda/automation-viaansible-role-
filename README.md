# ansible


As part of my DevOps studies, I was asked to create an ansible role that does the following steps


Update for Linux installation packages

Installing the tree and htop packages (it was allowed to replace, add and change packages as needed)

Installing a webserver in my case Apache/httpd but allowed to change to ngnix, mysql or any software whose installation is done this way ״apt/yum install-what-we-want-to-install״

Copying files from the file folder inside the role (any type of file can be copied) into the servers located in the host file (we can change the file copying location by changing the line in code "dest: /var/www/html" to "dest:/any/path/ we-want

And finally print how many RedHat and how many Debian (Ubuntu) hosts
