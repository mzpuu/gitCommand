# 核心操作
* 初始化仓库,.git目录默认隐藏,可以通过命令ls -ah显示
git init

* 把文件添加到版本库，可以一次添加多个文件，git add . 代表把所有文件全部提交
git add 文件名 文件名

* 把文件提交到当前分支
git commit -m '本次提交的说明'

* 把项目提交到(远程)仓储
git push


# 分支管理
* 查看远程分支
git branch -a

* 查看本地分支
git branch

* 创建并切换分支 （加-b表示创建并切换）
git checkout -b 分支名

* 切换回分支
git checkout 分支名

* 从主分支里创建新分支
git checkout master -b 新分支名

* 合并某分支到当前分支
git merge 分支名

* 删除分支
git branch -d 分支名
git branch -D 分支名 (强行删除分支)


# 解决冲突
* 情景一 提交或拉取时冲突
  - git stash
  - git pull
  - git stash pop

* 情景二 如果你想完全地覆盖本地的代码，只保留服务器端代码，则直接回退到上一个版本，再进行pull
git reset --hard HEAD^
git pull origin master
*** 注：origin master表示git的主分支

* 情景三 分支合并时冲突(当我们git merge 分支名 时)
  - git status (查看发生冲突的文件)
  - 然后手动合并冲突
  - git add .  (添加更改后的文件)
  - git commit -m 'xj' (提交)


# 查看ssh密钥
* 进入.ssh目录
cd ~/.ssh

* 查看id_rsa.pub文件
cat id_rsa.pub

# 克隆远程项目
git clone 远程源地址

# 回退某个操作
* 查看命令历史
git reflog
* 根据commitID撤销某个操作
git reset --hard 某个commitId


# 和远程分支建立关联
git branch --set-upstream-to=origin/远程分支的名字 本地分支名


# 删除文件
* 删除版本库中的文件
git rm filename
* 恢复工作区中误删的文件
git checkout -- filename
*** 注：git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。


# 远程仓储
* 创建sshkey密钥
ssh-keygen -t rsa -C "youremail@example.com"
* 在远程仓库中添加ssh公钥
* 关联远程库
git remote add origin git@server-name:path/repo-name.git
* 第一次推送master分支的所有内容,此后只需要使用git push origin master即可推送最新修改
git push -u origin master


# 多人协作
* 查看远程仓储的详细信息
git remote -v
* 推送本地分支到远程仓库,
  - 如果发生冲突，用git pull试图合并，如果发生冲突则解决冲突，再进行推送
  - 如果git pull后提示no tracking information(没有追踪信息)，则进行第四项，建立关联，之后pull，有冲突再合并
git push origin 本地分支名
* 在本地创建和远程分支对应的分支
git checkout -b 本地分支 origin/远程分支名
* 建立本地分支和远程分支的关联
git branch --set-upstream 本地分支名 origin/远程分支名

# 补充
* git fetch和git pull的区别
与git pull相比git fetch相当于是从远程获取最新版本到本地，但不会自动merge。如果需要有选择的合并git fetch是更好的选择。效果相同时git pull将更为快捷。

* 查看仓库当前的状态
git status

* 查看提交日志
git log

* 回退版本,在git中用HEAD表示当前版本,HEAD^表示上一个版本,HEAD^^表示上上个版本
  - git reset --hard HEAD^ 或
  - git reset --hard 3628164 (数字代表log里commit后面的id,只需要填前几位就可以)

* 窗口关闭后回退版本(git reflog用来记录你的每一次命令)
git reflog

* 工作区和暂存区
工作区就是你建立的能看见的目录,.git即为git的版本库,Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。
用git add把文件添加进去，实际上就是把文件修改添加到暂存区；
用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支

* 撤销修改
  - 直接丢弃工作区的修改，用命令git checkout -- file
  - 修改添加到了暂存区，想丢弃修改，分两步，第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作
