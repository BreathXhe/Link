### 查看远程仓库的路径
``` git remote -v ```
>如果只有origin的两行, 说明未设置 upstream，一般情况下，设置好一次 upstream 后就无需重复设置

### 添加上游仓库
``` git remote add upstream https://github.com/BreathXhe/xxx.git```

### 检查是否添加成功
``` git remote -v ```

### 推送本地修改
``` git push origin master ```

### 拉取源仓库的更新
``` git fetch upstream ```

### 合并远程的master分支
``` git merge upstream/master ```

### 推送合并的内容
``` git push ```
