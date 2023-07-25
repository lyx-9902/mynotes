git使用

1. 克隆项目

    复制  url 

   命令 ：   git clone  + "url"

2  提交代码

   git commit

3  创建新分支 

​    git 

4  切换到新分支上

git checkout  newImage(newImage为你起得分支名字)

git checkout newImage

快捷方式：  创建 + 切换分支

git checkout -b <your-branch-name>

5  合并两个分支

指针在master 上。执行 git merge  bugFix 

即把bugFix 分支 合并到了 master上。

另一种合并： 使提交记录线性化展示。

git rebase master（指针在新分支上。）