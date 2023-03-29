# 常用命令

## 常用命令

​​一般流程

```bash
#添加readme文件
echo "# gitLearn" >> README.md
#初始化本地git
git init
#添加 README.md文件
git add README.md
#提交commit
git commit -m "first commit"
#重命名当前分支为 main
git branch -M main
#添加远程仓库地址, 替换成自己的
git remote add origin https://github.com/kokodayou2000/gitLearn.git
#推送
git push -u origin main
```

查看

```bash
#查看远程分支
git branch -r
 
#查看本地分支
git branch
```

推送

```bash
#将服务器的修改合并到本地后上传
git stash git pull --rebase origin master git stash pop
#强制上传,本地覆盖服务器
git push origin master -f
```

拉取

```bash
#拉取远程分支
git checkout -b 本地分支 origin/远程分支
 
#拉取远程分支
git pull origin 远程分支　

#建立分支
git branch --set-upstream-to origin/远程分支名  本地分支名

#拉取分支
git pull
 
#遇到本地冲突，先删除本地分支，再重新拉取远程分支
git branch -D 本地分支名称
```

分支

```bash
#创建分支
git branch newBranch
#切换分支
git checkout newBranch
#合并分支
#比如你想合并一个修改好bug的程序，修好bug的分支叫 fixBug 主分支 main，你现在应该在main分支上
git merge fixBug
```

合并

```bash
git merge
#当你在main分支上，你想要将bugFix合并进来 git merge bugFix即可
```

变基









