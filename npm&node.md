1. 手动安装 npm

```
curl -L https://npmjs.com/install.sh| sh
```

2. 安装 npm 中的 n 模块，并用 n 安装 node

```
npm install -g n
n stable
```

3. node 切换失效的解决办法

   3.1 查看 node 当前安装路径

   ```
   $ which node
   ```

   3.2 n 默认安装路径是 /usr/local，若你的 node 不是在此路径下，n 切换版本就不能把 bin、lib、include、share 复制该路径中，所以我们必须通过 N_PREFIX 变量来修改 n 的默认 node 安装路径。编辑环境配置文件：

   ```
    $ vim ~/.bash_profile
   ```

   3.3 将下面两行代码插入到文件末尾： ( /usr/local 是 node 实际安装位置 )

   ```
    export N_PREFIX=/usr/local
    export PATH=$N_PREFIX/bin:$PATH
   ```

   3.4 保存退出 `:wq`

   3.5 执行 source 使修改生效。

   ```
    $ source ~/.bash_profile
   ```

---

# install pm2

1. 安装 pm2

```
npm install pm2 -g
```

2. 根目录 www 下创建文件，hello.js,内容如下：

```
const http = require('http')
http.createServer(function(req,res) {
res.writeHead(200,{'Content-Type':'text/plain'})
res.end('hello world')
}).listen(8081)

console.log('server test')
```

3. 执行 pm2 start hello.js 你的服务就跑起来了，此时地址栏输入http://118.xxx.xxx.xx:8081（你自己的服务器IP）就会看到hello world

4. pm2 的几个常用命令：

- `pm2 start <projectname>` 启动项目
- `pm2 list` 查看启动的应用
- `pm2 show <projectname>` 查看详细信息
- `pm2 logs` 查看当前信息
- `pm2 stop <projectname>` 停止项目
- `pm2 delete <projectname>` 删除项目

---
