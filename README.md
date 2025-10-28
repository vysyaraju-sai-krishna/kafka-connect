# kafka-connect
Debezium mysql connector with mysql for kafka connect handson 

I have installed debezium-connector-mysql-3.3.1.Final-plugin.tar.gz  locally . 
And then extracted tar file . 
Send extracted file through scp from my local  windows to cp-demo .

I have stored this directory in /usr/share/java

[root@saikrishna cp-demo]# docker exec -it connect bash
[appuser@dcfc5fc154d8 ~]$ ls /usr/
bin  games  include  lib  lib64  libexec  local  logs  sbin  share  src  tmp
[appuser@dcfc5fc154d8 ~]$ ls /usr/share/java
acl                   ce-kafka-rest-extensions  confluent-common          confluent-hub-client        confluent-rebalancer  confluent-telemetry  debezium-connector-mysql  kafka-rest-bin  kafka-serde-tools        rest-utils
ce-kafka-http-server  ce-kafka-rest-servlet     confluent-control-center  confluent-metadata-service  confluent-security    cp-base-new          kafka                     kafka-rest-lib  monitoring-interceptors  schema-registry
[appuser@dcfc5fc154d8 ~]$

Command to see all the connectors present 



[root@saikrishna ~]# curl -k -u connectAdmin:connectAdmin https://localhost:8083/connector-plugins | jq

I have created tables in mysql docker container which is present in cp-demo in this way .

[root@saikrishna cp-demo]# docker exec -it mysql mysql -u root -p # to enter into mysql docker container .
Enter password:vsaikrish@143
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 10
Server version: 9.4.0 MySQL Community Server - GPL

Copyright (c) 2000, 2025, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| db1                |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.006 sec)

mysql> use db1;
Database changed
mysql> CREATE TABLE students (
    ->   id INT AUTO_INCREMENT PRIMARY KEY,
    ->   name VARCHAR(100),
    ->   age INT,
    ->   city VARCHAR(50)
    -> );
Query OK, 0 rows affected (0.056 sec)

mysql> INSERT INTO students (name, age, city)
    -> VALUES
    ->   ('Sai', 22, 'Hyderabad'),
    ->   ('Krishna', 23, 'Chennai'),
    ->   ('Anu', 21, 'Bangalore');
Query OK, 3 rows affected (0.028 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM students;
+----+---------+------+-----------+
| id | name    | age  | city      |
+----+---------+------+-----------+
|  1 | Sai     |   22 | Hyderabad |
|  2 | Krishna |   23 | Chennai   |
|  3 | Anu     |   21 | Bangalore |
+----+---------+------+-----------+
3 rows in set (0.001 sec)

mysql> exit





I have added this debezium mysql configuration file  through control center directly in connect .


While launching it asked me a username and password for oAuth Bearer, at that i have given directly 
superUser as username and superUser as password 


