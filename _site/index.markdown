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

复制上一台机子的id_rsa密钥，并赋予可执行权限
chmod 600 id_rsa

拉取当前分支最新代码
git pull

提交当前版本的三段代码
git add .    暂存当前更改
git commit -m "test"   test是本次提交的操作名
git push  提交你的当前版本，仓库会更新
```



