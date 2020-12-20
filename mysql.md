# Mysql

## List of commands

```bash

mysqldump -h mysql -u root -p mall > ~/mall_backup.sql #Dump mysql database
mysql -h mysql -u root -p123456 -D mall < ~/mall_backup.sql #Restore mysql database

## Dump mysql database to new database
mysqladmin -h mysql -u root -p123456 mall_event_pid_coverage_1022 
mysqldump -h mysql -u root -p123456 -v mall | mysql -h mysql -u root -p123456 -D mall_event_pid_coverage_1022

mysql -uroot -p123456 -sNe "set global explicit_defaults_for_timestamp =1;create database if not exists airflow";
```
