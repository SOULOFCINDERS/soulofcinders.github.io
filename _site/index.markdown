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

WSL2的.wslconfig配置
```
[wsl2]
networkingMode=bridged
vmSwitch=WSL_Bridge
dhcp=false
macAddress=5c:bb:f6:9e:ee:55

memory=4GB 
processors=4
```

在WSL内部：
```
sudo gedit /etc/wsl.conf
```

编辑输入：
```
[boot]
systemd=true
[network]
generateResolvConf = false
```

然后：
```
sudo gedit /usr/lib/systemd/network/wsl_external.network
```

编辑输入：
```
[Match]
Name=eth0

[Network]
Description=WSL_external
DHCP=false
Address=192.168.1.10/24 # 这是自定的ip地址
Gateway=192.168.1.1
DNS=192.168.1.30
```

WSL中运行：
```
sudo systemctl enable systemd-networkd
sudo systemctl restart systemd-networkd
ip a
```

查看WSL虚拟网卡ip，在WSL中运行：
```
ip a |grep "global eth0"
```

在Windows中通过<wsl-ip>和<端口>就可以访问WSL2中的应用程序

解决docker desktop在win下启动容器端口占用的问题
这种情况是Hyper-V会保留部分tcp端口，开始到结束范围内的端口不可用：
```
netsh interface ipv4 show excludedportrange protocol=tcp
```
解决方法是暂时关闭NAT服务，并排除你想要的端口(6379)作为保留端口
```
net stop winnat
netsh int ipv4 add excludedportrange protocol=tcp startport=6379 numberofports=1 store=persistent
net start winnat
```