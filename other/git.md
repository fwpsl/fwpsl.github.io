**git操作**：
```
    在本地新建一个分支： git branch [newBranch]
    切换到你的新分支: git checkout [newBranch]
    创建并切换到新分支： git checkout -b [newBranch]
    将新分支发布在github上： git push origin newBranch
    在本地删除一个分支： git branch -d newBranch
    git co -b  feature/fwpsl
    git push origin  feature/fwpsl
    在github远程端删除一个分支： git push origin :newBranch   (分支名前的冒号代表删除)
    git checkout -- <file> 指令从先从缓存区中拉取版本还原，如果没有 再到版本库中拉取还原。
    git branch --set-upstream-to=origin/feature/<远程分支> <本地分支> 分支跟踪
    git config --add core.filemode false
    git log --pretty=oneline：将只会显示提交的commit id号和对应的注释
    回退：
    ​	git reset --hard commit_id 或则是 git reset --hard HEAD^  回退版本
    ​	# hard选项，表示彻底将工作区、暂存区和版本库记录恢复到指定的版本库
    ​	使用“git push -f”提交更改
    反做：
    ​	使用“git revert -n 版本号”命令
```

