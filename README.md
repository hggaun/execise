# execise
创建版本库    git init 在某一个目录下进行
创建文件      touch 文件名
添加文件到仓库   git add 文件名
提交文件到仓库   git commit -m "修改解释内容"
检查是否有未提交的修改  未放入的待提交的修改等    git status
查看历史记录     git log   简显  git log pretty=oneline
回到某一个版本    git reset --hard HEAD^(当前版本)/某一个版本秘钥
读取文件内容     cat 文件名
丢弃工作区修改    git checkout --文件名
暂存区的修改撤销到工作区     git reset HEAD 文件名
移出文件          rm 文件名    若想撤销删除操作  git checkout --文件名   (版本库中存在该文件)  若想把版本库中的文件也删除   git rm 文件名
