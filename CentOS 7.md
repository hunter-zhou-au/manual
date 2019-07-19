### 环境

- CentOS 7.6.1810 64 位
- 5.5.60-MariaDB
- openjdk version "1.8.0_212"
- apache-tomcat-8.5.39
- Yum version: 3.4.3
- 19.1.1 from /usr/lib/python2.7/site-packages/pip (python 2.7)
- Python 2.7.5

### List

- Java
- Tomcat8
- mariadb
- mongodb 3.4

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

---

##### 安装 mongodb 3.4

1. 配置 MongoDB 的 yum 源(创建 yum 源文件)

   > vim/etc/yum.repos.d/mongodb-org-3.4.repo

2. 添加以下内容：

```
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

3. 安装 MongoDB

   > yum -y install mongodb-org

4. 常用命令

- `mongod` 查看 mongodb 信息：(可以看到 mongodb 端口号，以及存储数据文件夹/data/db)
- `whereis mongod` 查看 mongo 安装位置
- `systemctl start mongod.service` 启动 MongDB
- `systemctl stop mongod.service` 停止 MongDB
- `systemctl restart mongod.service` 重启 mongodb
- `systemctl status mongod.service` 查看 Mongdb 状态
- `systemctl enable mongod.service` 设置开机启动
- `mongo` 进入 mongo
- `show dbs` 查看数据库

5. 设置 mongodb 远程访问：

- 修改配置文件：`vim /etc/mongod.conf` 进入配置文件中，将 bindIp 注释掉。并且重启 mongdb。

- 开启防火墙端口 `firewall-cmd --permanent --zone=public --add-port=27017/tcp`
- 使规则生效 `firewall-cmd –reload`
- 查看开放的所有端口号 `firewall-cmd --list-ports`
- 远程 HTTP 访问： http://ip:27017

##### 安装 forever 用来替代 node 启动（Express 项目)

1. 安装
   > npm install forever -g
2. 常用命令

- `forever –help`
- `forever start app.js`
- `forever stop app.js`
- `forever start -l forever.log -o out.log -e err.log app.js`
