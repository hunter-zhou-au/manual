### CentOS 如何查看端口是被哪个应用/进程占用

- `ps -ef|grep node` 会列出所有 node 程序的进程
- `netstat -lnp|grep 3002` 查看 3002 端口是否被占用
