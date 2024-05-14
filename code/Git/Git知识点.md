#code #git
## 1、git和GitHub的关系
---
git和github其实并没有特殊的关系
github只是使用git的开源代码仓库而已。使用git作为工具的代码仓库有很多，除了github之外还有gitlab以及国内的码云gitee等等。

## 2.git
---
### 1、概念
Git是目前世界上最先进的分布式版本控制系统。
Git是分布式版本控制系统，那么它就没有中央服务器的，每个人的电脑就是一个完整的版本库，这样，工作的时候就不需要联网了，因为版本都是在自己的电脑上。
### 2、安装
直接下载安装即可，该选的选上
### 3、Git的基本结构
![[Git工作原理和流程]]
### 4、git设置
---
**设置用户**：`git config --global user.name "xxx"`
**设置邮箱**：`git config --global user.email "xxx@qq.com"`
**查看用户信息**：`git config --list`
git设置用户名和邮箱，ssh设置的邮箱，以及GitHub的用户名邮箱，三者的关系？
	1、**产生ssh密钥对时，`ssh-keygen -t rsa -C "myname@email.com"`，里面输入的email与Git设定的用户名，与GitHub等代码托管网站的用户名毫无关联。**
	**2、git本地用户名和email最好和代码托管网站的一致**，如果本地设定的[user.email](http://user.email/)值是：[personal@126.com](mailto:personal@126.com)，由于在GitHub上的账户的邮件地址也是[personal@126.com](mailto:personal@126.com)，如果从这台电脑push的话，GitHub会认定这次这个push是账户拥有者自己做的，跟直接登录到GitHub，从网站上修改，是相同的，修改人是一样，就是账户拥有者。如果本地设定的[user.email](http://user.email/)值是：[company@company.cn](mailto:company@company.cn)，也能push到GitHub，GitHub会记录这次的修改是另一个人（用户名是company）做的。
### 5、本地仓库
---
版本库又名仓库，英文名repository，可以简单的理解一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改，删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻还可以将文件”还原”。
#### 创建/取消本地仓库
**创建**：也叫初始化本地仓库，cd到需要作为仓库的文件夹下，执行git命令
命令：`git init`
此时目录下会多了一个.git的目录，这个目录是Git来跟踪管理版本的
**取消**：删除仓库文件夹下的.git文件夹
### 6、常用命令
---
#### 查看仓库状态
就是查看目录下所有文件的状态，未被追踪（untracked）的文件，不会被git管理--如追踪修改历史，还原历史版本等
命令：`git status [<选项>...] [--] [<路径名>...]`
红色-untracked files：未被记录的，新增的文件会出现这个状态
红色-changes not staged for commit：modified：修改过，已经登记在案的文件最近又发生了改动，需要新增到暂存区，然后再commit到本地仓库
绿色-changes to be commited：staged：放入了暂存区的状态，接下来需要使用commit将其放入本地仓库

#### 添加到暂存区
**文件只有放入了暂存区，git才开始对其进行各种追踪**
命令：`git add [options] [--] <文件路径>`
新命令：`git stage <文件>`这个命令更直观，就是把文件加入到暂存区
#### 提交到本地仓库
命令：`git commit -m ”提交备注信息"`
#### 撤销
![[Pasted image 20240513093141.png]]
在`git`里，撤销代码的命令主要为`git reset`，但是有`git reset --soft`、`git reset --hard`、`git reset --mixed`3种模式。这三种命令主要是针对已提交仓库之后的代码的回滚，基本后边都是要带上提交日志版本号回滚的。

- `--soft`:该命令表示撤销代码到暂存区之后，`commit`之前，代码在本地不会改变。
- `--mixed`:该命令表示撤销代码到暂存区和`commit`之前，代码在本地不会改变。
- `--hard`:该命令表示回退代码到某个版本下，代码在本地会改变到指定版本下，谨慎操作。

**代码撤销这块，主要想到有下边这几种撤销，`提交暂存区的撤销（add撤销）`、`提交本地仓库撤销（commit撤销）`、`推送远程仓库撤销（git push之后的撤销）`**

**1、从暂存区撤销--add撤销**

当代码通过`git add .`提交到暂存区，如果想要从暂存区撤回来，主要有以下几个方法。

1.1 `git reset <文件名>`或者`git reset HEAD`
1.2 `git restore --staged <fileName>`
1.3 `git reset --mixed`或者`git reset -- <fileName>`
1.4 `git rm --cached 文件名`
以上操作，文件将变成untracked的状态，只针对没有commit过的文件

`--soft`、`--mixed`、`--hard`主要用来基于已commit的代码**版本号**回滚代码的，用在这里有点大材小用。**另外只有`--mixed`可以不用写版本号完成撤销操作**，其他两个不写版本号（除了用HEAD^）都无效果。
文件将变成untracked的状态

**2、commit撤销**

代码经过`git commit -m 备注说明`提交本地仓库之后，想要代码回滚，有以下几种方法来回退不同状态的代码。主要使用`--soft`、`--mixed`模式。

2.1 `git reset --soft HEAD^或者HEAD~1或者版本号`
	只是将代码撤销到暂存区之后，还未添加到本地仓库之前，只能使用`--soft`模式
2.2 `git reset --mixed HEAD^或者HEAD~1或者版本号`
	撤销到暂存区之前(即 `git add .`之前)
**2.3 单纯的修改commit的注释**
	`git commit --amend`进入vim编辑空间，输入i进行编辑，修改最上面的文字，然后保存即可
	当然，如果已推送到远程分支上，虽然也能通过这个命令修改日志内容，但是修改完再提交就是新的日志记录，远程上仍然会有旧的注释。  
	另外，还有假如说我们在本地提交了两次`commit`填写了两次说明，那也仅仅只能修改最后一次。
**3、从远程仓库撤销**
推送到远程仓库和提交本地仓库没有什么区别，仍然使用三种模式`--soft`、`--mixed`、`--hard`进行撤销即可。因为撤销其实不管你用什么模式，都是撤销的我们本地代码，与远程无关，至于你撤销完代码之后，是合并回原分支，还是新拉分支，代码是不会影响远程分支的。

另外，已经推送到远程分支的代码记录，是无法撤销的，只能是撤销回来本地的改完再提交回去，但是无法撤销以前的提交记录。
#### 查看文件内容变化
`git diff <文件名>`
`git diff --cached`和`git diff --stage`
#### 查看文件修改历史
`git log` 显示从最近到最远的日志，只显示提交（commit）的日志
`git blame <file>` 以列表形式查看指定文件的历史修改记录。
#### 回退文件版本
1、`git checkout <文件名>`，修改文件，发现不对，然后将文件回退到stage时的状态
#### 删除
---
1、从暂存库删除

`git rm --cached 文件名`

2、从本地删除

`git rm 文件名`
### 7、分支
---

列出分支
`git branch`
本地git init 之后，没有add之前，git branch 没有数据
创建新分支
`git branch 分支名`
切换分支
`git checkout branchName`
合并分支
`git merge <需要合并到当前分支的分支名>`
删除分支
`git branch -d (branchname)`
### 8、远程仓库
---
#### 创建
`git remote add <remote_name> <remote_url>`：添加一个新的远程仓库。指定一个远程仓库的名称和 URL，将其添加到当前仓库中，也就是建立本地仓库
#### 拉取
`git pull <远程主机名> <远程分支名>:<本地分支名>`

`git fetch 远程别名:本地分支名`
`git merge 远程别名/本地分支名`

git pull === git fetch + git merge
`git fetch`是将远程主机的最新内容拉到本地，用户在检查了以后决定是否合并到工作本机分支中。

而`git pull` 则是将远程主机的最新内容拉下来后直接合并，即：`git pull = git fetch + git merge`，这样可能会产生冲突，需要手动解决。
#### 推送
第一次推送时，要先把远程仓库拉取到本地：git pull
`git push [远程仓库别名] [本地分支名]`
#### 克隆
**git clone** 是一个用于克隆（clone）远程 Git 仓库到本地的命令。

**git clone** 会克隆远程仓库到本地，并在当前目录下创建一个与远程仓库同名的文件夹，并复制远程仓库的所有代码和历史记录

**git clone** 相当于完成了 创建文件夹，`git init` 、`git remote`、 `git pull`的操作

命令：`git clone [url] [别名]`
url：远程仓库的地址
别名：给远程仓库取的别名，会在本地生成以别名命名的文件夹
#### 删除
`git remote rm [别名]`
### 9.链接本地和远程
#### 1、方式一：直接clone
新建文件夹，在文件夹下打开git bash，然后输入 `git clone 远程仓库地址`，会在当前目录下创建与远程仓库同名的文件夹，并把远程仓库内容拉取到该文件夹，包括仓库的内容和历史记录

接下来正常操作就可以
#### 2、方式二：先创建本地文件夹
1、创建与远程仓库同名的文件夹
2、在文件夹下执行`git init`，初始化本地仓库
3、执行`git remote add 别名 远程仓库地址`，与远程仓库建立联系
4、执行 `git pull 别名 本地仓库分支名`，将远程仓库拉取到本地，或者 `git fetch origin`+`git merge origin/main`
### 6.使用ssh访问GitHub
---
#### 概念
SSH是安全外壳协议，它本身和git没什么关系，主要是为了使用它来进行安全验证。密钥本质是为了方便，用来替代用户名口令的认证方式的。

说白了为了证明你是你，为了方便根据账号做权限管理。比如阻止你clone你没有权限的代码，阻止你push代码到没有权限的远程等等。说白了，这是一个安全工具，通过它可以让我们的账号和代码更加安全。

使用SSH，本地生成密钥对，然后把公钥加入到代码托管网站的秘钥允许列表里面，把公钥加入到网站的允许列表这一步是需要密码授权的。这样操作，网站承认这样一个事实：用这个密钥对访问我，等同于提供了密码。密钥对保存在某台机器上，这样从这台机器上访问网站就不需要密码了，因为这台机器上能找到秘钥来替代口令进行认证。
#### 查看现有密钥
`ls -al ~/.ssh`
`~`：表示根目录，Windows下是用户目录C:\Users\jiujie\.ssh
如果您收到 _~/.ssh_ 不存在的错误，则表示默认位置中没有现有的 SSH 密钥对。您可以在下一步中创建新的 SSH 密钥对。
GitHub支持的公钥文件名
- _id_rsa.pub_
- _id_ecdsa.pub_
- _id_ed25519.pub_
#### 生成密钥
使用ssh-keygen工具来生成我们的ras秘钥。ras是一种对称加密算法，它的加密原理是生成一对秘钥，一个是可以分享给别人的公钥，一个是你自己保管的私钥。简单来说持有公钥一方可以验证私钥的正确性，但是不可以破解私钥加密的数据。所以我们会把公钥上传到各个网站，在自己的机器保留私钥。、

GitHub 于 2022 年 3 月 15 日删除了旧的不安全密钥类型，从而提高了安全性。

从该日期起，不再支持 DSA 键 （）。您无法在 GitHub.com 上向个人帐户添加新的 DSA 密钥。`ssh-dss`

2021 年 11 月 2 日之前的 RSA 密钥 （） 可以继续使用任何签名算法。在该日期之后生成的 RSA 密钥必须使用 SHA-2 签名算法。某些较旧的客户端可能需要升级才能使用 SHA-2 签名。

**命令：**`ssh-keygen -t rsa -C "wolfs@******.com"`
**新命令**：`ssh-keygen -t ed25519 -C "your_email@example.com"`
加密方式不同，会生成不同的文件：id_ed25519、id_ed25519.pub、id_rsa、id_rsa.pub
这里的邮箱可以随便，最好能用来表明身份，比如说来自哪一台电脑，这样回头在对应的网站删除公钥的时候，就能知道删除的是来自哪里的公钥

里面的-C参数带的email地址没有什么实际用处。从命令本身来说，-C只是给产生的秘钥对加了一个注释。用notepad++打开id_rsa.pub，可以看到末尾处，有这个email地址，方便以后拿到这个密钥对的时候，根据这个可能能回忆起来当初产生这个密钥对是干嘛的。推荐做法是：每台电脑上产生秘钥对时，加注释信息内容主要跟这台机器相关的内容，并且把秘钥加入到代码托管网站的列表里面的时候，用这个跟某台电脑密切相关的名称。以后如果，不用这台电脑了，从网站上删除这个秘钥很方便。
#### 查看公钥内容
```shell
cat ~/.ssh/id_ed25519.pub | clip
```
以上命令：查看并复制到粘贴板
#### 配置
复制公钥到对应的网站中即可
复制文件`c/Users/Administrator/.ssh/id_rsa.pub`内容，把key添加到：github > settings > SSH and GPG keys > New SSH key > 粘贴保存。
#### 测试连接
`ssh -T git@github.com`
成功：Hi xiabengda! You've successfully authenticated, but GitHub does not provide shell access.

## 3.开发工具集成git环境