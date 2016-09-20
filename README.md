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

