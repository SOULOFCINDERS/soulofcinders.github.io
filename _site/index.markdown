### git的使用

```
查看状态
git status

git log --oneline  显示现在的分支

git reset --hard HEAD~1  回退一个版本

git commit -m "initial commit" 仓库初始化

个人信息初始化，每次换机子都要加入这些信息
git config --global user.email  "841135647@qq.com"
git config --global user.name  "SOULOFCINDER"
git config --list 

生成ssh密钥
ssh-keygen -t ed25519 -C "841135647@qq.com"

切换http到ssh
git config --global url.git@github.com:.insteadOf https://github.com/

复制上一台机子的id_rsa密钥，并赋予可执行权限
chmod 600 id_rsa

切换分支到main和feature
git checkout main
git checkout feature

拉取当前分支最新代码
git pull

提交当前版本的三段代码
git add .    暂存当前更改
git commit -m "test"   test是本次提交的操作名
git push  提交你的当前版本，仓库会更新

怎么把一个本地工程推送到远程新建的git仓库
git init
git remote add origin https://github.com/SOULOFCINDERS/myMIT6.824.git
git branch -M main
git add .
git commit -m "initial commit"
git push -u origin main
```


### debian大版本升级

首先

```
apt-get update
apt-get upgrade
```

打开配置文件

```
nano /etc/apt/sources.list
```

将版本代号改为你想升级到的版本，如sid

```
deb http://mirrors.ustc.edu.cn/debian sid main contrib non-free
deb-src http://mirrors.ustc.edu.cn/debian sid main contrib non-free
```

然后

```
apt-get update
```

```
apt-get dist-upgrade
```

如果这个过程出问题，系统会坏掉，建议重装

### WSL2技巧
停止WSL2到win的NAT转换，这可能会导致WSL2没有网络，但是同时可以解决docker端口占用的问题
```
net stop winnat
docker start container_name
net start winnat
```