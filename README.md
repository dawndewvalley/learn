# git初次使用记录

## 创建版本库
1. 安装完git后，在开始菜单打开 gitbash;
2. 通过`cd F:/xx/` 进入到你希望的目录，`git init`初始化一个Git仓库。(pwd 可以查看当前所在目录)；
3. 添加文件到Git仓库，首先、要把文件放到git仓库目录下，然后通过`git add fileName` 和`git commit -m 注释`即可

## 版本修改及回退命令
1. `git status` 查看当前仓库的状态；
2. `git diff` 能够查看文件做了什么修改；
3. `git log` 查看修改的历史记录；
    `git reflog` 可以查看你每次修改的 commit id,通过`git reset --head commitId`能回退or前进到对应的文件版本；
4. `git rm file`将 file 工作区删除，然后 `git commit`，即可从版本库中删除file，或者在版本库尚未删除时，使用`git checkout --file`，可以找回该file；
