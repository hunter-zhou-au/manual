# 一台机器绑定两个 github 账号

1. 生成两个 SSH KEY
   `ssh-keygen -t rsa -C "hunter.zhou.au@gmail.com" -f ~/.ssh/huntergitkey_rsa`
   `ssh-keygen -t rsa -C "polokang@gmail.com" -f ~/.ssh/polokang163gitkey_rsa`
2. 把 key 加到 ssh agent 上
   `ssh-add ~/.ssh/huntergitkey_rsa`
   `ssh-add ~/.ssh/polokang163gitkey_rsa`
   可以通过 `ssh-add -l` 来确认结果

3. 进入~/.ssh/ 目录，创建 config 文件,并配置（CMD + SHIFT + G）
   `touch config`

```
#one(self-email@.com)
  Host github.com
  HostName github.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/huntergitkey_rsa
  User one

#two(work-email@xxx.com)
  Host github_work.com
  HostName github.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/polokang163gitkey_rsa
  User two
```

4. 将生成的新 SSH key(huntergitkey_rsa)添加到要关联的 Github 帐号中(https://github.com/settings/keys)

5. 进入工程目录，配置 git 账号

```
git init
git config user.email "hunter-zhou-au@gmail.com"
git config user.name "hunter-zhou-au"
```
