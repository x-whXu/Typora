# Git bash命令

## 1. 本地git

#### 1.1 基础流程

```git
# 初始化当前目录为git仓库
git init
# 工作区文件添加到暂存区
git add
# 暂存区文件添加到本地仓库
git commit -m 'commit description'
```

#### 1.2 版本管理

```
# 查看文件当前状态
git status
# 查看提交日志
git log
git mylog
# 版本回退
git reset --hard <commit ID>
# 查看删除的提交记录
git reflog
```



## 2. 远程git

#### 2.1 基础流程

```
# 添加远程仓库
git remote add origin <仓库ssh路径>
# 推送本地仓库到远程仓库
git push origin master
git push
```

#### 2.2 远程仓库到本地

```
# clone远程仓库到本地
git clone <仓库url路径>
# 抓取远程分支到本地
git fetch [remote name] [branch name]
# 抓取远程分支到本地，并自动合并
git pull [remote name] [branch name]
```

