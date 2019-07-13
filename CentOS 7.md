### 环境

- CentOS 7.6.1810 64 位
- 5.5.60-MariaDB
- openjdk version "1.8.0_212"
- apache-tomcat-8.5.39
- Yum version: 3.4.3
- 19.1.1 from /usr/lib/python2.7/site-packages/pip (python 2.7)
- Python 2.7.5

### 步骤：

1. Install Java

- `yum install java-1.8.0-openjdk.x86_64`

2. Install Tomcat 8

- Download from https://archive.apache.org/dist/tomcat/tomcat-8/v8.5.39/bin/apache-tomcat-8.5.39.tar.gz

- Uplaod to /usr/local by [FileZilla's sftp]

- into /usr/local folder for unzip
  `tar -zxvf apache-tomcat-8.5.39.tar.gz -C /usr/local`

- modify the folder name to tomcat8

3. Install mariadb(mysql)

- `yum install mariadb mariadb-server mariadb-libs mariadb-devel -y`

4. install mariadb secure

- startup mariadb `systemctl start mariadb`
- check status `systemctl status mariadb`
- set mariadb startup at machine opening `systemctl enable mariadb`
- install secure `mysql_secure_installation`
- all steps enter `y`
- check if can enter db `mysql -u root -p version`

5. configure charset to utf-8

- `vi /etc/my.cnf` add following under [mysqld] tag

  `init_connect='SET collation_connection = utf8_general_ci' init_connect='SET NAMES utf8' character-set-server=utf8 collation-server=utf8_general_ci skip-character-set-client-handshake`

- `vi /etc/my.cnf.d/client.cnf` add following under [client]

  `default-character-set=utf8`

- `vi /etc/my.cnf.d/mysql-clients.cnf` add following under [mysql]

  `default-character-set=utf8`

- check charset

  `show variables like "%character%";show variables like "%collation%";`

6. create user and set privileges

- `create user starex@localhost identified by 'zhk39...';`
- `grant all on *.* to username@localhost identified by 'zhk39...';`
- `grant all privileges on *.* to username@'%' identified by 'zhk39...';`
- `flush privileges;`

7. other commands

- `UPDATE mysql.user SET password=PASSWORD('zhk39...') WHERE User='starex';`

- `rm -rf apache-tomcat-8.5.39`

- `wget https://www.python.org/ftp/python/3.7.3/Python-3.7.3.tgz`
