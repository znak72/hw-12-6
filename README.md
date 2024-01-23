# Домашнее задание к занятию «Репликация и масштабирование. Часть 1»

---

### Задание 1
Выполните конфигурацию master-slave репликации, примером можно пользоваться из лекции.

*Приложите скриншоты конфигурации, выполнения работы: состояния и режимы работы серверов.*
![1](https://github.com/znak72/hw-12-6/blob/main/001.png)
---

### Задание 2

Выполните конфигурацию master-slave репликации, примером можно пользоваться из лекции.

*Приложите скриншоты конфигурации, выполнения работы: состояния и режимы работы серверов.*

#### На всех:
```
wget https://dev.mysql.com/get/mysql80-community-release-el7-6.noarch.rpm
```
```
rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
```
```
rpm -Uvh mysql80-community-release-el7-6.noarch.rpm
```
```
yum -y install mysql-server mysql-client
```
```
mysqld --initialize
```
```
chown -R mysql: /var/lib/mysql
```
```
mkdir -p /var/log/mysql
```
```
chown -R mysql: /var/log/mysql
```
#### Добавить в /etc/my.cnf :
```
bind-address=0.0.0.0
server-id=(1..n)
log_bin=/var/log/mysql/mybin.log
```
#### Посмотреть пароль присвоенный при инициализации бд:
```
cat /var/log/mysqld.log
```
#### Сменить пароль:
```
mysql -p
```
```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY '12345';
```
```sql
FLUSH PRIVILEGES;
```
#### На мастере:
```sql
CREATE USER 'replication'@'%' IDENTIFIED WITH mysql_native_password BY 'Repl11Pass!';
GRANT REPLICATION SLAVE ON *.* TO 'replication'@'%';
```
```sql
SHOW MASTER STATUS;
```
![12-6-2-1](https://github.com/znak72/hw-12-6/blob/main/12-6-2-1.png)
#### На слэйве:
```sql
CHANGE MASTER TO MASTER_HOST='192.168.*.*', MASTER_USER='replication', MASTER_PASSWORD='Repl11Pass!', MASTER_LOG_FILE = 'mybin.000001', MASTER_LOG_POS = (число из колонки position из статуса мастера);
```
```sql
START SLAVE;
```
```sql
SHOW SLAVE STATUS\G;
```
![12-6-2-2](https://github.com/znak72/hw-12-6/blob/main/12-6-2-2.png)
#### На мастере: 
```sql
create database hw_12_6_Golikov;
```
#### На слэйве:
```sql
show databases;
```
![12-6-2-3](https://github.com/znak72/hw-12-6/blob/main/12-6-2-3.png)
---

