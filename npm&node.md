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
