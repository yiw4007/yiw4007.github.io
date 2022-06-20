# linux基础----常用命令

------------------

Table of contents:



{:toc}

## 命令格式

<b><font color=green>command</font> <font color=red>[-options [parameter]]</font> [file]</b>

| Command   | Operation                                  |                              |
| --------- | ------------------------------------------ | ---------------------------- |
| pwd       | print working dictionary                   | 输出当前目录                 |
| ls        | list                                       | 列出                         |
| cd        | change dictionary                          | 切换目录                     |
| mkdir     | make dictionary                            | 建立一个新的目录             |
| touch     | modify the timestamps in the file metadata | 创建文件                     |
| mv        | move                                       | 移动和重命名                 |
| cp        | copy and paste                             | 拷贝粘贴                     |
| rm        | remove                                     | 删除                         |
| ln        | link                                       | 链接文件                     |
| tar       | tape archive                               | 压缩或者解压文件             |
| cat       | concatenate                                | 查看文本文件内容并输出到屏幕 |
| head/tail | view a text file at several lines          | 查看文件前后n行              |
| less/more | view a text file one page at a time        | 逐页查看                     |
| wc        | word count                                 | 字数统计                     |
| cut       | seperate a file                            | 文本切割                     |
| sort      | output with order                          | 排序                         |
| uniq      | reports or filters out the repeated lines  | 统计重复                     |
| paste     |                                            |                              |
| tr        |                                            |                              |
| grep      |                                            |                              |
| sed       |                                            |                              |
| awk       |                                            |                              |
| chmod     | change mode                                | 更改文件状态                 |
| wget      |                                            |                              |
| scp       |                                            |                              |
| tree      |                                            |                              |
| vim       |                                            |                              |

--------------------

## pwd (print working dictionary)

感觉常用的就是单独用这个命令，option这种看看就好了。 [Ref](https://phoenixnap.com/kb/pwd-linux)

| Option         | Description                                                  |
| -------------- | ------------------------------------------------------------ |
| -L, --logical  | Instructs `pwd` to output the `$PWD`[environment variable](https://phoenixnap.com/kb/linux-set-environment-variable) contents, including symbolic links. If no option is specified, `pwd`assumes `-L`. |
| -P, --physical | Prints the path to the current directory. All the components are directory names, and symbolic links are resolved. |
| --version      | Outputs the program version.                                 |
| --help         | Displays the help message.                                   |

------------------------

## cd (change dictionary)

习惯用一些符号代替路径

| 常见用法 |                        |
| -------- | ---------------------- |
| cd ./    | 从当前目录进入其他目录 |
| cd ..    | 回到上级目录           |
| cd -     | 返回上一次的工作目录   |
| cd ../.. | 回到上上级目录         |
| cd ~     | 家目录                 |
| cd       | 同上,回到家目录        |
| cd /     | 根目录                 |

-------------------

## ls (list)

在文件特别多的时候学会用参数进行查看

| option     | description                                            |                                |
| :--------- | :----------------------------------------------------- | ------------------------------ |
| ls -a      | list all files including hidden file starting with '.' | 列出全部文件包括隐藏文件       |
| ls -l      | list with long format - show permissions               | 列出目录详细信息               |
| ls -h      | list long format with readable file size               | 将内容转化为人类易读方式       |
| ls -R      | list recursively directory tree                        | 递归目录列出文件               |
| ls -d      | list directories - with ' */'                          | 显示目录本身而非目录下文件     |
| ls -S      | sort by file size                                      | 以文件大小排序                 |
| ls -t      | sort by time & date                                    | 以时间排序                     |
| ls -X      | sort by extension name                                 | 以扩展名排序                   |
| ls -r      | list in reverse order                                  | 反向排序                       |
| ls -s      | list file size                                         |                                |
| ls --color | colored list [=always/never/auto]                      |                                |
| ls -i      | list file's inode index number                         |                                |
| ls -F      | add one char of */=>@\| to enteries                    | 显示目录后的/，显示可执行文件* |
| ls -C      | show colors                                            | 带颜色显示                     |

| Usage      | Description                     |                                 |
| ---------- | ------------------------------- | ------------------------------- |
| ls         | list files in current documents | 列出当前目录下文件              |
| ls ./      | Ibid.                           | 同上                            |
| ls ./*.txt | list all files end with txt     | 列出当前目录下所有txt结尾的文件 |
| ll         | =ls -la                         | 列出当前目录下文件包括隐藏文件  |

------------------------

## mkdir (make dictionary)

| Option | Description                                              |                                              |
| ------ | -------------------------------------------------------- | -------------------------------------------- |
| -v     | displays a message for every directory created (verbose) | 显示创建信息                                 |
| -p     | create parent directories as necessary                   | 创建层级文件夹，不加的话只能在当前目录下创建 |
| -m     | set the file modes, i.e. permissions                     | 为文件夹添加权限                             |

```shell
$ mkdir -p file/data/{vip1,vip2,vip2} 
$ mkdir -v a=rwx file
```

----------------------------

## touch 

一般就是简单的创建一个文件，参数不常用

```shell
$ touch test{1..10}
```

| Option | Description                                                 |                |
| ------ | ----------------------------------------------------------- | -------------- |
| -c     | avoid creating a new file                                   | 避免创建新文件 |
| -r     | change a file's timestamp based on another file's timestamp | 按参考文件     |

-----------------

## mv (move)

```shell
#移动或重命名：mv [Option] source destination
$ mv a.txt geek.txt #重命名文件 rename
$ mv data ~ #移动文件夹到家目录 move dictionary with the inside files to home dictionary
$ mv a.txt data/ #移动 move file
```

+ 其实我觉得与其说是移动的操作，不如说是剪切并粘贴为/到，跟windows中的移动到的操作还是不太一样的

----------------

## cp (copy and paste)

+ 与剪切并粘贴为的命令相对应的就是复制并粘贴为，其实区别就是是否保留原文件

```shell
$ cp readme.txt ./data/
$ cp my_test ./data/
```

-------------------------------

## rm (remove)

| Option | Description                                                  |                        |
| ------ | ------------------------------------------------------------ | ---------------------- |
| -i     | ask the user for confirmation before removing each file      | 删除前询问用户         |
| -f     | removes the file forcefully                                  | 不显示警告信息强制删除 |
| -r     | delete all the files and sub-directories recursively of the parent directory | 递归删除文件夹         |

 `rm -r *`    删除文件夹下所有文件

+ 删除重要文件时尽量使用`-i`参数

-------------------------

## ln (link)

+ 不像在windows中可以在使用软件时导入文件，在命令行界面（command line interface, CLI）需要把要操作的文件复制到具有自己权限的文件夹内操作，因此利用软链接节约文件空间就十分必要

```shell
#ln -s target(absolute address) dictionary
$ ln /home/yiw4007/data ./
```

+ **软链接与硬链接的区别**：软链接指向地址，硬链接指向文件内容

----------------------------------------

## tar (tape archive)

+ 解压缩：tar [options] [archived-file]
+ 压缩：tar [options] [name of archive-file] [file or directory to be archived]

| Option | Description                                                  |      |
| ------ | ------------------------------------------------------------ | ---- |
| -c     | creates Archive                                              |      |
| -x     | extract the archive                                          |      |
| -f     | creates archive with given filename                          |      |
| -v     | displays verbose Information                                 |      |
| -j     | filter archive tar file using tbzip (.tbz)                   |      |
| -z     | zip, tells tar command that creates tar file using gzip (.gz) |      |
| -W     | verify a archive fil                                         |      |
| -r     | update or add file or directory in already existed .tar file |      |

```shell
#Creating an uncompressed tar Archive using option -cvf
$ tar -cvf file.tar *.c
$ tar -cvfz fille.tar.gz *.c
$ tar -cvfj file.tar.tbz example1.cpp example2.cpp example3.cpp

#Extracting files from Archive using option -xvf
$ tar -xvf file.tar
$ tar -zxvf file.tar.gz 
```

+ 其他**压缩**和**解压缩**命令
  + `zip`和`unzip`用于压缩和解压缩*zip文件
  + `gzip`和`gunzip`用于压缩和解压*gz文件
  + `bzip2`和`bunzip2`用于压缩和解压*bz2/ *tbz文件

+ 解压后的文件会放在当前目录下以压缩前文件命名的文件夹内，`-v`参数也是用来显示整个过程的
+ `z`和`j`的顺序不能变，其他参数的顺序不影响（因为其实相当于两个步骤，`tar`相当于打包，`gz/bz`相当于压缩，**先打包再压缩**或者**先解压再拆包**）

----------------------------

## cat (concatenate)

| Option | Description                             |                          |
| ------ | --------------------------------------- | ------------------------ |
| -A     | Show all                                | 列出所有字符，包括制表符 |
| -n     | print the line numbers                  | 打印所有行号             |
| -b     | print the nonblank line numbers         | 仅打印非空白行行号       |
| -s     | suppress repeated empty lines in output | 不输出多行空行           |
| -E     | highlight the end of line               | 在每行结束显示$          |

```shell
#create and input content into a new file
$ cat >test2
#press CTRL+D (hold down Ctrl key and type ‘d‘) to exit

#Standard Output with Redirection Operator
$ cat test >test1 # existing contents of the test1 will be overwritten by the contents of the test file

#Appending Standard Output with Redirection Operator
$ cat test >>test1
#the contents of the test file will be appended at the end of the test1 file.
```

+ `tac` 逆向查看 concatenate in reverse
+ `zcat`查看压缩的文本文件
+ 使用cat写入文件时不能随意删除，删除本行内容可以用`CTRL`+`Bachsapce`组合，但上一行的内容无法用`cat`命令修改，只能重新写入
+ 每次用`>`写入同一文件之前的内容都会被覆盖，如果不想被覆盖可以用`>>`写入

-----------------

## head/ tail

| Option | Description                               |                            |
| ------ | ----------------------------------------- | -------------------------- |
| -n     | show fist/last n lines (default 10 lines) | 查看文件前/后n行，默认10行 |

```shell
$ head -n 2 test.gtf
$ head -2 test.gtf
```

-------------------------

## more/ less

+ 空格键翻页，回车键换行，`q`退出

+ `less`: 更常用，可配合`zless`使用

  | Option | Description                                    |          |
  | ------ | ---------------------------------------------- | -------- |
  | -N     | show output along with line numbers            | 显示行号 |
  | -S     | show by lines (press`←/→`to view all contents) | 单行显示 |

-------------

## wc (word count)

| Option | Description     |                    |
| ------ | --------------- | ------------------ |
| -l     | line            | 统计行数           |
| -w     | word            | 统计字符串数       |
| -m     | character       | 统计字数           |
| -c     | bytes           | 统计字节数         |
| -L     | max line length | 统计最长的行的长度 |

```shell
$ wc /proc/cpuinfo
#lines words characters
```

--------------------

## cut (seperate a file)

| Option | Description                                  |                             |
| ------ | -------------------------------------------- | --------------------------- |
| -d     | use DELIM instead of TAB for field delimiter | 指定分隔符，默认`\t`(`Tab`) |
| -f     | select only fields                           | 输出哪几列 （特定字段）     |

```shell
$ cut -d " " -f 1,2 state.txt --output-delimiter='%'
Andhra%Pradesh
Arunachal%Pradesh
Assam
Bihar
Chhattisgarh

$ less -S Data/example.gtf | cut -f 1,3-5,7
```

-------------------------------

## sort (order)

| Option | Description                                    |                                        |
| ------ | ---------------------------------------------- | -------------------------------------- |
| -n     | compare according to string numerical value    | 按照数值从小到大排序                   |
| -V     | natural sort of (version) numbers within text  | 字符串中含有数值时，按数值从小到大排序 |
| -r     | sort in reverse order                          | 逆向排序                               |
| -k     | sort a table on the basis of any column number | 指定区域排序                           |
| -t     | sort by a specific delimiter                   | 指定分隔符排序                         |
| -u     | sort and remove duplicates                     | 排序并去除重复项                       |

+ 总的来说从`wc`到`sort`的命令都会结合`cat`或`less`命令使用，使用`|`去传递内容

```shell
$ cat example.gtf | cut -f 1 | sort -Vr
$ less -S example.gtf | sort -k 3 | less -S
```

-----------------------

## uniq (reports or filters out the repeated lines)





-------------------------

## chmod (change mode)/chown (change owner)

```shell
-rw-r--r-- 12 linuxize users 12.0K Apr  8 20:51 filename.txt
|[-][-][-]-   [------] [---]
| |  |  |   |      |     | 
| |  |  |   |      |     +-----------> 7. Group
| |  |  |   |      +-----------------> 6. Owner
| |  |  |   +------------------------> 5. how many files in 
| |  |  +----------------------------> 4. Others Permissions
| |  +-------------------------------> 3. Group Permissions
| +----------------------------------> 2. Owner Permissions
+------------------------------------> 1. File Type (directory(d);file(-);link(l))
```

+ r = read:4, w = write:2, x = execute:1

| Number Combo | Owner          | Group                               | Others         |
| ------------ | -------------- | ----------------------------------- | -------------- |
| 777          | All permission | All permission                      | All permission |
| 754          | All permission | Only read and execute，can't modify | Only read      |
| 760          | All permission | Only read and write                 | no permission  |

+ 通常情况下可写就会可读，因为不读的话也没法写，除非加一些信息

```shell
$ chmod +x seq1.sh
$ chmod 777 seq1.sh
```

+ 下载后的脚本默认都是普通文档，需要加可执行的权限，可执行的文件会以绿色显示

```shell
$ sudo chown root seq1.fastq
```

+ 一般来说变更所有者的话都需要管理员权限，所以不常用

------------------

## tree

| Option  | Description                                               |                            |
| ------- | --------------------------------------------------------- | -------------------------- |
| tree -L | Descend only level directories deep                       | 目录显示到几层，后面接数字 |
| tree -p | Print the permission information for each file            | 列出权限标识               |
| tree -u | Display file owner or UID number                          | 列出文件或目录的拥有者名称 |
| tree -g | Display file group owner or GID number                    | 列出文件或目录所属群组名称 |
| tree -s | Print the size in bytes                                   | 列出文件或目录的大小       |
| tree -D | Print the date of last modification or (-c) status change | 列出文件更改的时间         |

```shell
$ tree -L 1 /home/data
```

