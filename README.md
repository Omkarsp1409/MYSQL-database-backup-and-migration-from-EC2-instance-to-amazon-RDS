# MYSQL-database-backup-and-migration-from-EC2-instance-to-amazon-RDS
A practical AWS project demonstrating MySQL backup and migration from EC2 to Amazon RDS using mysqldump. Includes database setup, secure configuration, backup generation, restoration, and verification for reliable cloud-based database management.
 MySQL Database Backup & Migration from EC2 to Amazon RDS

This project demonstrates a complete end-to-end workflow for deploying a MySQL database on an Amazon EC2 instance, generating backups using mysqldump, and migrating the database to an Amazon RDS (MariaDB) instance. It highlights essential cloud engineering concepts including database configuration, AWS networking, security groups, backup management, and data migration practices.


---

🚀 Project Overview

The goal of this project is to build a secure, reliable, and scalable cloud-based database environment using AWS services.
Key tasks performed:

Deploy MySQL/MariaDB on an EC2 instance

Create and configure an Amazon RDS (MariaDB) instance

Generate SQL backups using mysqldump

Migrate EC2 database backup to RDS

Verify data integrity after migration

Implement proper inbound/outbound rules via Security Groups



---

🎯 Objectives

Set up and configure MySQL on an EC2 instance

Create a managed and scalable RDS MySQL/MariaDB instance

Migrate data securely using mysqldump

Ensure reliable backup and restore functionality

Improve database security, availability, and performance



---

🏗️ Architecture Diagram

(Upload your architecture image here)
Example:

+------------------------------+
|           VPC                |
|  +------------+   +--------+ |
|  |  EC2       |<->|  RDS   | |
|  | MySQL      |   |MariaDB | |
|  +------------+   +--------+ |
|      Security Groups         |
+------------------------------+


---

🛠️ Technologies Used

Amazon EC2 (Linux Instance)

Amazon RDS (MariaDB)

MySQL / MariaDB Server

mysqldump utility

AWS VPC & Security Groups

SSH / Terminal



---

📦 Implementation Steps

1. Launch EC2 Instance

Use Amazon Linux

Allow inbound rules: SSH (22), MySQL (3306)

Install MySQL/MariaDB:


sudo yum install mariadb105-server -y
sudo systemctl start mariadb
sudo systemctl enable mariadb


---

2. Create Amazon RDS (MariaDB) Instance

Engine: MariaDB

Disable public access (recommended)

Allow EC2 security group in inbound rules

Note down the RDS endpoint



---

3. Create Database & Sample Data on EC2

mysql -u root -p
CREATE DATABASE devopsbatch;
USE devopsbatch;
CREATE TABLE students (id INT PRIMARY KEY, name VARCHAR(50));
INSERT INTO students VALUES (1,'Omkar'), (2,'Aniket');


---

4. Take Backup Using mysqldump

mysqldump -u root -p devopsbatch > ec2_backup.sql


---

5. Restore Backup into RDS

mysql -h <RDS-ENDPOINT> -u admin -p
CREATE DATABASE studentinfo;
EXIT;

mysql -h <RDS-ENDPOINT> -u admin -p studentinfo < ec2_backup.sql


---

6. Verify Migration

USE studentinfo;
SHOW TABLES;
SELECT * FROM students;


---

🔒 Security Best Practices

Avoid using 0.0.0.0/0 — allow only EC2 SG or your IP

Keep RDS private inside VPC

Use strong DB credentials

Enable automated backups in RDS



---

🧪 Testing Done

Verified EC2 MySQL setup

Generated and validated SQL backup file

Successfully restored data on RDS

Checked table structure & data integrity



---

🏁 Conclusion

This project demonstrates a complete and practical database migration workflow on AWS. It enhances database availability, improves reliability, and reduces administrative overhead by using Amazon RDS for managed database operations. The steps implemented here reflect real-world DevOps and cloud engineering practices.


---

📌 Future Enhancements

Automate backup using cron jobs

Enable Multi-AZ for high availability

Use AWS DMS for enterprise-scale migration

Add CloudWatch alerts for database performance



---

👤 Author

Omkar Pagade


---
