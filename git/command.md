# Area

- git clone git@xxx/client.git --progress 操作中刷新状态

# Current

- git reset --hard origin/release 将远端release强制覆盖本地release
- git reset --hard HEAD 将本地release重置成本地最新分支
- git reset --hard develope 将本地release重置成本地develope分支
- git reset --hard commitId 回滚到指定commitId版本
- git reset 撤销add操作

# State

- git log --no-merges --after="00:00:00 2017-4-28" 根据时间查询
- git log --pretty=oneline --author="hexin" --since="2018-4-15" 根据作者和时间查询
- git log --graph --author="chisongqi" --stat 根据作者查询
- git remote show origin 查看remote地址，远程分支，还有本地分支与之相对应关系等信息
- git remote prune origin 与服务器同步删除本地分支
- git remote -v 查看远程库信息
- git remote rm origin 删除关联的origin远程库
- git remote add origin [originlink] 关联新的origin远程库(需要先删除以关联信息)
- git remote set-url origin [originlink] 修改关联的origin远程库

# Common

- git branch -D branch_name 删除本地分支<branch_name>
- git branch -a 查看所有本地分支和远程分支
- git branch -r 只查看远程分支
- git branch --set-upstream release_rights origin/release_rights 关联远程分支<release_rights>
- git branch -vv 查看分支映射关系
- git checkout --ours xxx/A.java // 抛弃甲的版本，保留乙的
- git checkout --theirs xxx/A.java // 抛弃乙的版本，完全采用甲的
- git checkout ver.1.32 迁出指定tag版本
- git checkout dev A.class 从dev分支merge文件A.class到当前分支
- git tag -a ver.7.29.2 -m "ver.7.29.2" 添加tag

# Coloaborate

- git push --tags  # 提交tag
- git push -f origin master  # 强行提交到远程仓库
- git push -u origin master  # 如果当前分支与多个主机存在追踪关系，则可以使用 -u 参数指定一个默认主机，这样后面就可以不加任何参数使用git push
- git push origin --delete [branchname]  # 删除远程分支
- git pull origin <branch_name> --allow-unrelated-histories  # 允许不相关历史强制合并

# Config

- git config --global core.autocrlf false  # 换行符转换
- git config --global gui.encoding utf-8  # 避免 ui 乱码
- git config --global core.quotepath off  # 避免 git status 中文文件名乱码
