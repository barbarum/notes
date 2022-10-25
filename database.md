# Databases

## Mysql

### List of commands

```bash

mysqldump -h mysql -u root -p mall > ~/mall_backup.sql #Dump mysql database
mysql -h mysql -u root -p****** -D mall < ~/mall_backup.sql #Restore mysql database

## Dump mysql database to new database
mysqladmin -h mysql -u root -p****** mall_event_pid_coverage_1022 
mysqldump -h mysql -u root -p****** -v mall | mysql -h mysql -u root -p****** -D mall_event_pid_coverage_1022

mysql -uroot -p****** -sNe "set global explicit_defaults_for_timestamp =1;create database if not exists airflow";

## Start mysql client with UTF-8 character set/解决中文乱码问题
mysql --default-character-set=utf8
```

## PostgreSQL

### List of commands

```bash
psql -h host -d database -U user -W # connect to database@host with the given user.
\c DBNAME # switch to new table
```

## References

1. [Postgres Cheatsheet](https://postgrescheatsheet.com/#/)
