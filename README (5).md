<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Connect a Web App with Aurora

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-databases-webapp)

**Author:** anifalaje clinton  
**Email:** clintonanif@gmail.com

---

## Connect a Web App to Amazon Aurora

![Image](http://learn.nextwork.org/content_lavender_curious_centaur/uploads/aws-databases-webapp_1709b26b)

---

## Introducing Today's Project!

### What is Amazon Aurora?

Amazon Aurora is a fully managed, cloud-native relational database service from AWS that's compatible with MySQL and PostgreSQL. It's designed to offer the speed and reliability of high-end commercial databases at a much lower cost.

It is useful because it provides exceptional performance (up to 5x faster than standard MySQL), high availability with data replicated across multiple Availability Zones, and automatic scalability. As a managed service, AWS handles the operational tasks, letting you focus on your applications. In this project, you used Amazon Aurora to store and manage data for your web application running on an EC2 instance.

### How I used Amazon Aurora in this project

In today's project, I used Amazon Aurora to create a MySQL-compatible relational database instance. This database served as the backend for my web application, allowing me to store and manage data that users input through the web interface. I connected the web app, running on an EC2 instance, to the Aurora database and verified that the web app could successfully interact with and update the database.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how fun it would be.

### This project took me...

The project took 2 hours.

---

## Creating a Web App

![Image](http://learn.nextwork.org/content_lavender_curious_centaur/uploads/aws-databases-webapp_b7999168)

To connect to my EC2 instance, I used the key pair created during its launch and connected via SSH.

To help me create my web app, I first installed a basic web app that runs on my EC2 instance.

---

## Connecting my Web App to Aurora

I set up my EC2 instance's connection details to my database by creating a file named dbinfo.inc in the inc sub-folder within the /var/www directory. This file contains the necessary information to connect to my Aurora database.

![Image](http://learn.nextwork.org/content_lavender_curious_centaur/uploads/aws-databases-webapp_1709b25b)

---

## My Web App Upgrade

Next, I upgraded my web app by navigating to the /var/www/html folder, creating a new file named SamplePage.php, and then adding a PHP script to it. This script pulls details from the dbinfo.inc file to display up-to-date changes directly from the website.

![Image](http://learn.nextwork.org/content_lavender_curious_centaur/uploads/aws-databases-webapp_2709b25b)

---

## Testing my Web App

To make sure my web app was working correctly, I first added some new data through the web app in my browser. Then, to verify that this data was actually updating my Aurora database, I connected to my database using the MySQL CLI. I ran several commands, including SHOW DATABASES;, USE sample;, SHOW TABLES;, DESCRIBE EMPLOYEES;, and finally SELECT * FROM EMPLOYEES; to view the actual data in the EMPLOYEES table and confirm the updates.

![Image](http://learn.nextwork.org/content_lavender_curious_centaur/uploads/aws-databases-webapp_1409z22b)

---

---
