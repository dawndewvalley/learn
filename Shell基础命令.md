使用git bash过程中发现，自己对shell的一些基础的文件操作命令不熟。故找了些资料学习下：
# 磁盘管理
1. `cd dirName` 切换到dirName目录下； `cd ..`返回上一级，注意有空格
2. `df -h` 查看文件系统的磁盘使用情况 ,-h是为了让输出结果容易阅读
3. `du -h` 查看当前目录或文件的大小
3. `mkdir [-p] dirName` -p确保目录名称存在，不存在就建一个，比如`mkdir -p BBB/Test`若没有 -p参数，那么当BBB目录不存在时将产生错误；
4. `ls` 查看当前目录下的文件及 子目录
5. `pwd` 查看当前目录的绝对路径 

# 文件管理
1. `cat fileName` 将 fileName文件的内容，加上行号打印出来。 `cat -n textfile1 > textfile 2`将textfile1上的内容加上行号输入到textfile2中；
2. `find path -option`在指定目录下查找文件，如果使用该命令时，不设置任何参数，则find命令将在当前目录下查找子目录与文件。并且将查找到的子目录和文件全部进行显示。 
3. `mv [options] source dest`用来给文件改名 `mv 文件名 文件名`，或移动文件到目录`mv 文件名 目录名` 
4. `rm [options] name` 删除一个文件或目录  `rm -r *`删除当前目录下所有文件及子目录
5. `touch fileName` 用于修改文件或目录的时间属性，若文件不存在，则新建。 `ls -l fileName`可以查看档案的时间记录
6. `cp [options] source dest`用于复制文件或目录 ， -r 参数表示若给出的源文件是一个目录文件，则将复制该目录下所有的子目录和文件
