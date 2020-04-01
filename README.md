# README #

This README would normally document whatever steps are necessary to get your application up and running.

### What is this repository for? ###

* Quick summary
This is the COMET system fork of the School of Ed COURSES DB system
* Version 
  V1.0
* [Learn Markdown](https://bitbucket.org/tutorials/markdowndemo)

### How do I get set up? ###

* Summary of set up

You need to place this code in the root of a web server folder like /var/www/html/

* Configuration

You need to setup the httpd.conf files with the proper codes
You need to add shibboleth codes
You need to set up your certs using openssl and get a UWCert and A InCommon cert


* Dependencies
Needs a working LAMP stack server
Needs Shibboleth SHIBD package

* Database configuration

You will need to install the empty db tables and populate the person table with at least 1 super user and import into the quarters table from the starter .sql file

You will need to config the courses/pub/api dbconfig file with the credentials needed.

* How to run tests
* Deployment instructions

### Contribution guidelines ###

* Writing tests
* Code review
* Other guidelines

### Who do I talk to? ###

* Repo owner or admin
  Michael Scott McGinn waptug@uw.edu
  Tim Hunt thunt@uw.edu

* Other community or team contact
* 
### Notes about this dev-comet.socialwork.uw.edu site.  ###

* the courses-backup folder is the old working system or V1 of the code from Paul I copied this here for reffernece while getting V2 of the code to work.
* 

### In the event of a power outage or server shutdown the following procedure will be required to bring the system back on line

The InCommon-metadata.xml file must be refreshed if any errors related to shibd prevent the system from working.
Try this first to see if it solves the issue.

Loaded the cert and the xml file back into the /var/run/shibboleth folder and restarted: service shibd restart
to refresh the certs and the xml file.
This will need to be done if the power goes out again or shibd errors showup. 

You can download a copy of the metadata from:
 
http://md.incommon.org/InCommon/InCommon-metadata.xml
 
And then manually set the full backingfilepath property in the MetadataProvider configuration element in /etc/shibboleth/shibboleth2.xml to refer to it. Also make sure you have a copy of the metadata signing cert in an appropriate location (also defined in the metadataprovider config element). The cert is available from:
 
http://md.incommon.org/certs/inc-md-cert.pem
 
The Shibboleth logs  will also tell you what went wrong (if anything) with fetching the metadata.
Look in var/log/shibboleth for errors

You will also have to restart httpd with
service httpd restart
and supply the root password for the cert to start the apache server.
See Mike McGinn or Tim Hunt for the password
root Dev.Comet.SSW#2015
linux, sql db, phpMyAdmin and ssl cert password

### In order to edit the db using phpMyAdmin from the admin menu you must ###
* get the current ip address you are connected to the internet with.
* edit /etc/https/conf.d/phpMyAdmin.conf file and change the ip addresses in it with the current ip address
* restart the httpd service with service httpd restart
* supply the ssl password 
* then relaunch phpMyAdmin from the admin menu 
* then login with the phpMyAdmin root and password

### Files to edit the fundingsource dropdown form on Offering Detail Page  ###
* /courses/controllers/offering/index.php  -- main page with all the sections and includes.
* /courses/inc/Form/Offering/MyForm.php
* /courses/views/offering/example-ajax-html.php
* /courses/views/offering/part-administrative.phtml
* /courses/controllers/plan/example.php -- alternate form without ajax.

@ToDo determine why db is not being updated with new value - Fixed 6/2016

Daily backups are run via cron and stored at /sysbackups
The backup dumps the entire server minus some system files.
In order to restore the system to a new vps you will need to install a default install of CentOS V7 and then
unzip the backup file to bring the server up.

The restore process has not been tested......  ran out of budget to finish this.
