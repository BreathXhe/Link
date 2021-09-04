查看你的远程仓库的路径：git remote -v 
如果只有origin的两行, 说明你未设置 upstream，一般情况下，设置好一次 upstream 后就无需重复设置

执行命令 git remote add upstream https://github.com/BreathXhe/xxx.git

再次执行命令 git remote -v 检查是否成功

将未提交的提交git push origin master

执行命令 git fetch upstream 抓取原仓库的更新

执行命令 git merge upstream/master 合并远程的master分支

执行命令 git push 把本地仓库向github仓库（你fork到自己名下的仓库）推送修改
