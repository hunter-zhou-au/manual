# 在 CentOS 7 上搭建 Shadowsocks

1. shadowsocks 服务端安装

```
yum install python-setuptools && easy_install pip
pip install shadowsocks
```

2. 配置服务器端 `vi /etc/shadowsocks.json`

```
{
    "server":"0.0.0.0",
    "server_port":8388,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password":"Opal1003",
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open": false
}
```

也可配置多个账号（但是我没测试）

```
{
    "server":"0.0.0.0",
    "port_password":{
     "8381":"xxxxxxx",
     "8382":"xxxxxxx",
     "8383":"xxxxxxx",
     "8384":"xxxxxxx"
     },
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open": false
}

字段	        说明
server	        ss服务监听地址
server_port	ss服务监听端口
local_address	本地的监听地址
local_port	本地的监听端口
password	密码
timeout	        超时时间，单位秒
method	        加密方法，默认是aes-256-cfb
fast_open	使用TCP_FASTOPEN, true / false
workers	        workers数，只支持Unix/Linux系统

```

3. 将 shadowsocks 加入系统服务 `vi /etc/systemd/system/shadowsocks.service`

```
[Unit]
Description=Shadowsocks
[Service]
TimeoutStartSec=0
ExecStart=/usr/bin/ssserver -c /etc/shadowsocks.json
[Install]
WantedBy=multi-user.target
```

- 设置开机自启命令 `systemctl enable shadowsocks`

- 启动命令 `systemctl start shadowsocks`

- 查看状态命令 `systemctl status shadowsocks`

4. shadowsocks 客户端安装

- Windows  
  https://github.com/shadowsocks/shadowsocks-windows/releases

- Mac OS X  
  https://github.com/shadowsocks/ShadowsocksX-NG/releases

- Android (可 PlayStore 直接下载 `shadowsocks` )
  https://play.google.com/store/apps/details?id=com.github.shadowsocks  
  https://github.com/shadowsocks/shadowsocks-android/releases

- Linux  
  https://github.com/shadowsocks/shadowsocks-qt5/wiki/Installation  
  https://github.com/shadowsocks/shadowsocks-qt5/releases

- IOS  
  https://itunes.apple.com/app/apple-store/id1070901416?pt=2305194&ct=shadowsocks.org&mt=8  
  https://github.com/shadowsocks/shadowsocks-iOS/releases

5. 可选装 serverspeeder [参考]https://github.com/91yun/serverspeeder
