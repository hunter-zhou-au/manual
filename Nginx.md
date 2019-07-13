# 安装

1. 添加 CentOS 7 EPEL 仓库
   `sudo yum install epel-release`

2. 安装 Nginx
   `sudo yum install nginx`

3. 启动 Nginx
   `sudo systemctl start nginx`

4. 启动防火墙（启动防火墙后，则远程连接不上数据库了）sudo systemctl start firewalld.service

5. 允许 HTTP 和 HTTPS 传输

```
sudo firewall-cmd --permanent --zone=public --add-service=http
sudo firewall-cmd --permanent --zone=public --add-service=https
sudo firewall-cmd --reload
```

6. 在浏览器中输入服务器 ip 地址，看到类似 Welcome to nginx 字样，则表示安装成功

# 操作

1. 停止 nginx
   `nginx -s stop`

2. 重启 nginx
   `nginx -s reload`

3. 启动 nginx
   `nginx`

# 配置 SSL（ /etc/nginx/nginx.conf)

1. 将已获取到的 1_www.domain.com_bundle.crt 证书文件和 2_www.domain.com.key 私钥文件从本地目录拷贝到 Nginx 服务器的 /usr/local/nginx/conf 目录下。(若无 /usr/local/nginx/conf 目录，可通过 mkdir /usr/local/nginx/conf 命令行创建。)
2. 修改 /etc/nginx/nginx.conf 文件(https://cloud.tencent.com/document/product/400/35244)

- 配置腾讯 SSL 安全认证

```
server {
    listen 443;
    server_name www.domain.com; #填写绑定证书的域名
    ssl on;
    root /var/www/www.domain.com; #网站主页路径。此路径仅供参考，具体请您按照实际目录操作。
    index index.html index.htm;
    ssl_certificate  1_www.domain.com_bundle.crt; #证书文件名称
    ssl_certificate_key 2_www.domain.com.key; #私钥文件名称
    ssl_session_timeout 5m;
    ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers on;
    location / {
    index index.html index.htm;
    }
}
server {
    listen 80;
    server_name www.domain.com; #填写绑定证书的域名
    rewrite ^(.*)$ https://$host$1 permanent; #把http的域名请求转成https
}
```

- 配置阿里云域名 SSL 安全认证

```
server {
	listen 443;
	server_name www.ozselection.com;
	ssl on;
	root /usr/share/nginx/www;
	index index.html index.htm;
	ssl_certificate   /usr/local/nginx/conf/2465609_www.ozselection.com.pem;
	ssl_certificate_key  /usr/local/nginx/conf/2465609_www.ozselection.com.key;
	ssl_session_timeout 5m;
	ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
	ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
	ssl_prefer_server_ciphers on;

	location / {
		root /usr/share/nginx/www;
		index index.html index.htm;
		}
}
```

3. 重启 nginx -s reload

# 常用命令

```
nginx -s reload  ：修改配置后重新加载生效
nginx -s stop  :快速停止nginx
nginx -c /path/to/nginx.conf：启动nginx
nginx -t : 验证nginx文件配置
ps aux | grep nginx ： 查看nginx路径

netstat -apn | grep 4040  查询端口号所占用的程序
kill -9 26105   杀死进程

rm -rf /var/log/httpd/access   将会删除/var/log/httpd/access目录以及其下所有文件、文件夹

rm -f /var/log/httpd/access.log   将会强制删除/var/log/httpd/access.log这个文件

unzip all.zip 解压缩

ssh haibor@1.2.3.4 Mac 连接linux
```
