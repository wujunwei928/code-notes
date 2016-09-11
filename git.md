```bash
    $ git config --global user.name "Your Name"
    $ git config --global user.email "email@example.com"
```

1. 初始化一个Git仓库，使用git init命令。


1. 查看工作区的状态: git status


1. 查看修改内容: git diff <file>(查看某个文件修改)  或  git diff(查看所有修改)


1. 添加文件到Git仓库，分两步：
    * 第一步，添加: git add <file1> <file2> <file3>  或 git add . (添加所有)
    * 第二步，提交: git commit -m '提交时的说明'


1. 查看提交日志: git log  或  git log --pretty=oneline


1. 查看git历史命令: git reflog


1. 回到过去: git reset --hard HEAD^   或   git reset --hard commit_id(之前某个版本的commit_id, git log可以看) 


1. 重返未来: 如果回到过去某个版本后, 想再回来, 先用git reflog查看历史命令, 找到想要返回的commit_id, 然后用git reset 返回未来


1. 工作区 和 暂存区: 修改一个文件, git add 之前, 在工作区, git add之后, 保存到暂存区, git add命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行git commit就可以一次性把暂存区的所有修改提交到分支。
一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的：
$ git status
nothing to commit (working directory clean)


1. git diff HEAD -- readme.txt 命令可以查看工作区和版本库里面最新版本的区别


1. Git每次修改，如果不add到暂存区，那就不会加入到commit中


1. 撤销修改
    * 当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。
    * 当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作。
    * 已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。


1. 删除文件
    命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。


1. 远程仓库
    ssh-keygen -t rsa -C "youremail@example.com"
    你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。
    如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。


1. 创建和合并分支
    * 查看分支：git branch

    * 创建分支：git branch <name>

    * 切换分支：git checkout <name>

    * 创建+切换分支：git checkout -b <name>

    * 合并某分支到当前分支：git merge <name>

    * 删除分支：git branch -d <name>


1. 解决冲突
    当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
    用 git log --graph 命令可以看到分支合并图。
    或用这样查看 git log --graph --pretty=oneline --abbrev-commit 


1. 分支管理策略
    Git分支十分强大，在团队开发中应该充分应用。
    合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，
    能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。
    $ git log --graph --pretty=oneline --abbrev-commit


1. bug分支
    修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
    当手头工作没有完成时，先把工作现场 git stash 一下，然后去修复bug，
    修复后，再 git stash pop，回到工作现场。
    * 保存工作现场: git stash
    * 工作现场列表: git stash list
      stash@{0}: WIP on dev: fb446fc rm d.txt
      stash@{1}: WIP on dev: fb446fc rm d.txt
    * 工作现场详情: git stash show stash@{0}   其中 stash@{0} 是现场ID 
    * 一是用 git stash apply 恢复，但是恢复后，stash内容并不删除，你需要用 git stash drop 来删除；
    * git stash pop  恢复工作现场的同时把stash内容也删了,  等于 git stash apply + git stash drop


1. Feature分支
    开发一个新feature，最好新建一个分支；
    如果要丢弃一个没有被合并过的分支，可以通过 git branch -D <name> 强行删除。


1. 多人协作


1. 标签管理
    * git tag <name>用于新建一个标签，默认为HEAD，也可以指定一个commit id；
    * git tag -a <tagname> -m "blablabla..." 可以指定标签信息；
    * git tag -s <tagname> -m "blablabla..." 可以用PGP签名标签；
    * git tag 可以查看所有标签。
    * git push origin <tagname> 可以推送一个本地标签；
    * git push origin --tags 可以推送全部未推送过的本地标签；
    * git tag -d <tagname> 可以删除一个本地标签；
    * git push origin :refs/tags/<tagname> 可以删除一个远程标签。


1. 忽略特殊文件
    * 忽略某些文件时，需要编写.gitignore；
    * .gitignore文件本身要放到版本库里，并且可以对.gitignore做版本管理！
    * 不需要从头写.gitignore文件，GitHub已经为我们准备了各种配置文件，只需要组合一下就可以使用了。https://github.com/github/gitignore


1. git配置
    * git 配置有三种级别  --system(系统级别), --global(用户级别), --local(仓库级别, 可以省略)
    * 配置git别名:  
      git config [ --system | --global | --local ] alias.st status
      下面就可以用 git st 代替 git status 使用了
    * git配置文件,  用户全局配置在  ~/.gitconfig, 代码仓库配置在 .git/config
      可以在文件中查看用户的 名称, 邮箱, 别名 等配置


1. 搭建git服务器(ubuntu为例)
    * 安装git: sudo apt-get install git
    * 创建一个git用户，用来运行git服务: sudo adduser git
    * 创建证书登录
      收集所有需要登录的用户的公钥，就是他们自己的id_rsa.pub文件，
      把所有公钥导入到/home/git/.ssh/authorized_keys文件里，一行一个。
    * 初始化git仓库
    * 未完待续......


1. 关于git的ssh-key: 解决本地多个ssh-key的问题
    本地配置了两个ssh-key，一个用来连接公司server，一个用来连接github，
    分别用的不同的用户名和邮箱地址，
    默认的配置情况下肯定会出现permission denied的错误，如何解决这个冲突呢？

>```bash
># 1: 为github配置新的key ，取名为github
>$ ssh-keygen -t rsa -C "xxx@gmail.com" -f ~/.ssh/github
>$ ls ~/.ssh
>github github.pub id_rsa id_rsa.pub known_hosts
>#其中默认的id_rsa是公司server用的
>
># 2: 复制 github.pub 中的内容, 在github账号中设置
>
># 3: 需要配置一下 将类似以下内容复制进去保存
>$ sudo vi ~/.ssh/config
>host github
>user git
>hostname github.com
>port 22
>identityfile ~/.ssh/github
>
># 4: 测试是否生效
>$ ssh -T github
># 如出现下列信息, 证明配置成功
># Hi xxx! You've successfully authenticated, but GitHub does not provide shell access.
>
># 5: 修改~/.ssh/config后, 命令行下从github网站clone代码的方法稍有不同
>git clone git@github.com:wujunwei928/big-data-study.git   # 修改前clone方法
>git clone github:wujunwei928/big-data-study.git           # 修改后clone方法
>
>```



1. windows下，glone出的代码，换行符改变，导致shell脚本报错，需要git配置设置换行符



### 参考资料
[廖雪峰的官方网站 - git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)




































