# git初次使用记录

## 创建仓库
1. 安装完git后，在开始菜单打开 gitbash;
2. 通过`cd F:/xx/` 进入到你希望的目录，`git init`初始化一个Git仓库。(pwd 可以查看当前所在目录)；
3. 添加文件到Git仓库，首先、要把文件放到git仓库目录下，然后通过`git add fileName` 和`git commit -m 注释`即可

## Git基本命令
1. `git add fileName` 可以将文件添加到缓存，`git add.`添加当前目录的所有文件
2. `git status` 查看当前仓库的状态；
3. `git diff` 能够查看文件做了什么修改；
4. `git log` 查看修改的历史记录；
    `git reflog` 可以查看你每次修改的 commit id,通过`git reset --head commitId`能回退or前进到对应的文件版本；
5. `git rm file`将 file 工作区删除，然后 `git commit`，即可从版本库中删除file，或者在版本库尚未删除时，使用`git checkout --file`，可以找回该file；
6. `git commit` 将缓存区内容添加到仓库中。Git为你的每一个提交都记录你的名字和邮箱地址，所以会提示你配置用户名和邮箱 `git config --global user.name 'dawndewvalley'` `git config --global user.email test@xx.com`. 当然如果绝对 `git add`提交缓存太繁琐了，你可以使用 `-a`跳过该选项：`git commit -am "跳过add"`；
7. `git rm file`将条目从缓存区中及硬盘中移除，如果想要在工作目录保留该文件：`git rm -cached file`；
8. `git mv file newfileName` 重命名磁盘上的文件

## 工作区和暂存区
你的Git仓库地址就是一个工作区，工作区的隐藏文件夹`.git`是Git的版本库。版本库中存了很多东西，最重要的就是称为 `stage`  或`index`的暂存区，还有Git为我们自动创建的第一个分支`master`，及指向`master`的一个指针叫`HEAD`.<br/>
`git add` 实际就是把文件修改添加到暂存区；<br/>
`git commit` 就是把暂存区中所有内容提交到当前分支；</br>
Git比其他版本控制系统设计得更优秀的是因为**Git跟踪并管理的是修改，而非文件**。

## 远程仓库
1. 创建SSH key:
先看用户主目录下是否有`.ssh`目录，若无，在git bash中输入`ssh-keygen -t rsa -C"email@xx.com"`。然后复制生成的`id_rsa.pub`中的文本；
2. 登录GitHub，在Setting中添加 ssh key,即1中复制的文本；
3. 在github中新建一个repo：learn;
4. 将本地的git库，与远程库关联：`git remote add origin git@github.com:dawndewvalley/learn.git`
5. 将本地库的所有内容推送给远程库`git push -u origin master`;
6. 解除本地库与远程库的关联：`git remote rm origin`;
7. 拉取一个Git仓库到本地 `git clone [url]`。 Git会按照你提供URL所提示的项目名称创建你的本地项目目录。
8. `git pull ` 获取最新的远程仓库分支。 

## 分支操作
master称为主分支，一开始master分支是一条线，Git用master指向最新的提交，再用HEAD指向master，就能确定当前分支，及当前分支的提交点。 当我们创建一个新的分支，例如dev，Git新建了一个指针dev，指向master相同的提交，再把HEAD指向dev,就表示当前分支在dev上。现在对工作区的修改和提交就是针对dev分支了，比如最新提交一次后，dev指针向前移动一步，而master指针不变。
```
//创建dev分支，并切换到dev
$ git checkout -b dev    // 相当于两条命令 $ git branch dev; $ git checkout dev

//查看当前分支，会列出所有分支，并用`*`标注当前分支
$ git branch 

//当完成 dev 分支的操作后，切换到master
$ git checkout master
 
//将dev 分支合并到 master 上。
$ git merge dev //git merge 用于合并指定分支到当前分支

//合并后，就能删除 dev 分支
$ git branch -d dev
```
通常合并分支时，Git会用fast forward模式，但是这种模式下，删除分支后，就会丢掉分支信息。如果禁用该模式后，Git就会在merge时生成一个新的commit，这样，从分支历史就能看到分支信息。即在合并分支时使用：
```
git merge --no-ff-m "merge with no-ff" dev
```
我们工作中对于分支的处理，master仅作为发布正式版用，工作时用 dev分支，然后每个人自己有一个分支，并即时将代码提交到dev分支上。

## 多人协作
当你从远程仓库克隆时，实际上Git自动把本地的master分支和远程的master分支对应起来了。并且远程仓库的默认名称是 origin. <br/>
`git remote`查看远程库的信息；<br/>
`git push origin master` 推送主分支<br/>
`git push origin dev` 推送工作分支<br/>
当他人从远程库clone时，默认情况下只能看到本地master分支，而想要在dev分支上开发，就必须创建远程origin的dev分支到本地：
```
git checkout -b dev origin/dev //这样才建立了工作分支
```
多人合作时，通常 先试图用`git push origin branchName`推送自己的修改，若推送失败表明远程分支比你本地更新，需要使用`git pull`合并。	

## FAQ

- 在GitHub添加SSH key时 提示 key is already use.<br/>

>表明所添加的SSH key已被其他账户使用，解决方法有两种，一是找到账户删除key,而是重新生成key. 重新生成key：在shell中使用命令`ssh-keygen -t rsa -b 4096 -C"email@xx.com"`;

- `git add`文件取消<br/>

>git使用过程中，发现不想提交的文件add进入index后，想回退取消，可以使用命令`git reset HEAD fileName`
