# 常用命令

- docker images 列出所有镜像
- docker image rm [image id] 删除镜像
- docker container ls -a 列出所有容器
- docker start [C.id] 启动 container
- docker exec -it [C.id] bash 进入容器(exit 退出)
- docker container stop [C.id] 停止一个容器
- docker container rm [C.id] 删除一个容器
- docker system prune -a 清理所有无用镜像

---

# 1. 容器技术和 Docker 简介

# 2. Docker 环境的各种搭建方法

1. 下载 VirtalBox 6.0.8 https://www.virtualbox.org/wiki/Downloads
2. 下载 Vagrant https://www.vagrantup.com/downloads.html
3. vagrant 使用
   - 命令行进入文件夹 centos7
   - 初始化 vagrantfile 文件 centos7 `vagrant init centos/7`
   - 下载 vagrant centos7 到 virtualbox,并启动机器 `vagrant up`
   - 登录到 centos7 系统 `vagrant ssh`
   - 更新 centos7 相关文件到最新版本 `[vagrant@localhost ~]$ sudo yum update`
   - 退出 centos7 `[vagrant@localhost ~]$ exit`
   - vagrant 其他常用命令：
   - 查看当前运行的机器状态 `vagrant status`
   - 停止 vagrant 机器 `vagrant halt`
   - 删除 vagrant 机器 `vagrant destroy`
   - 可以通过 vagrant boxes https://app.vagrantup.com/boxes/search 查找想要的不同操作系统的 vagrantfile.
4. centos 安装 docker https://docs.docker.com/install/linux/docker-ce/centos/
   - Install required packages. `sudo yum install -y yum-utils \device-mapper-persistent-data \lvm2`
   - set up the stable repository `sudo yum-config-manager \ --add-repo \ https://download.docker.com/linux/centos/docker-ce.repo`
   - install docker-ce `sudo yum install docker-ce docker-ce-cli containerd.io`
   - Start Docker `sudo systemctl start docker`
   - Verify that Docker CE is installed correctly by running the hello-world image. `sudo docker run hello-world`
5. 通过 vagrandfile 直接安装 centos7, only type `vagrant up`. 文件地址：
6. 通过 docker-machine 安装 centos7 虚拟机
   - `docker-machine create demo`

# 3. Docker 的镜像和容器

# 4. Docker 的网络

# 5. Docker 的持续化存储和数据共享

# 6. Docker Compose 多容器部署

7. 容器编排 Docker Swarm
8. Docker Cloud 和 Docker 企业版
9. 容器编排 Kubernetes
10. 容器的运维和监控
11. Docker + DevOps 实战 — 过程和工具
12. 总结
