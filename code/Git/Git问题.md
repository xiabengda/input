## 什么是Git？
## 测试git本地设置用户名与GitHub不一致
## 如何修改commit注释？
git commit -amend
## 添加到暂存库后，commit之前如何撤销？
git reset 文件名
git restore --staged 文件名
git reset --mixed/git reset -- 文件名
## commit之后如何撤销？
git reset --soft/--mixed/--hard 版本号
## 推送到远程仓库后，如何撤销？
经推送到远程分支的代码记录，是无法撤销的，只能是撤销回来本地的改完再提交回去，但是无法撤销以前的提交记录。