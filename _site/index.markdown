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