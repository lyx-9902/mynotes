# git常用操作

# [git 分支查看与切换](https://www.cnblogs.com/vae860514/p/11009787.html)

git 分支查看与切换

 1.查看所有分支

```
git branch -a
```

2.查看当前使用分支(结果列表中前面标*号的表示当前使用分支)

```
git branch
```

3.切换分支

```
git checkout 分支名
```



## 提交代码



```

1. git clone https://github.com/lys-9902/test2.git  远程克隆仓库
2. cd 进入文件
3. git add .  添加 注意 有 点
4. git commit -m'我是注释'      把文件提交到仓库
5. git push    输入账号密码
```



#### 切换某次历史提交的代码

1.找到提交的hash值

2.git 指令

```
git checkout <提交哈希值>
```

### 回到当前分支最新的版本

切换到需要拉取代码的分支。可以使用以下命令切换到目标分支：

```
git checkout 
```

 从远程仓库拉取最新代码。可以使用以下命令拉取远程分支的最新代码

```
git pull origin 
```

