# linux基础----常用命令

------------------



{:toc}

## 命令格式

<b><font color=green>command</font> <font color=red>[-options [parameter]]</font> [file]</b>

| Command   | Operation                                  |                               |
| --------- | ------------------------------------------ | ----------------------------- |
| pwd       | print working dictionary                   | 输出当前目录                  |
| ls        | list                                       | 列出                          |
| cd        | change dictionary                          | 切换目录                      |
| mkdir     | make dictionary                            | 建立一个新的目录              |
| touch     | modify the timestamps in the file metadata | 创建文件                      |
| mv        | move                                       | 移动和重命名                  |
| cp        | copy and paste                             | 拷贝粘贴                      |
| rm        | remove                                     | 删除                          |
| ln        | link                                       | 链接文件                      |
| tar       | tape archive                               | 压缩或者解压文件              |
| cat       | concatenate                                | 查看文本文件内容并输出到屏幕  |
| head/tail | view a text file at several lines          | 查看文件前后n行               |
| less/more | view a text file one page at a time        | 逐页查看                      |
| wc        | word count                                 | 字数统计                      |
| cut       | seperate a file                            | 文本切割                      |
| sort      | output with order                          | 排序                          |
| uniq      | reports or filters out the repeated lines  | 统计重复                      |
| paste     | merge                                      | 合并文件                      |
| tr        | translate/ transform                       | 字符替换                      |
| grep      | search                                     | 查找                          |
| sed       | stream editor                              | 流编辑器 (对文本进行增删改查) |
| chmod     | change mode                                | 更改文件状态                  |
| wget      | retrieves content from web servers         | 下载文件                      |
| scp       | secure copy                                | 远程文件拷贝                  |
| tree      | list dictionary as tree                    | 递归树状列出目录内容          |
| vim       | Vi mode file edition                       | vim程序编辑器                 |

+ 查询所有linux命令及详细参数的网站：http://man.linuxde.net/

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
| ls -s      | list file size                                         | 显示文件大小                   |
| ls --color | colored list [=always/never/auto]                      | 显示颜色                       |
| ls -i      | list file's inode index number                         | 显示目录                       |
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

| Option | Description                                                  |                       |
| ------ | ------------------------------------------------------------ | --------------------- |
| -c     | creates Archive                                              | 创建压缩文件          |
| -x     | extract the archive                                          | 解压缩                |
| -f     | creates archive with given filename                          | 输出结果到文件或设备  |
| -v     | displays verbose Information                                 | 显示处理进度          |
| -j     | filter archive tar file using tbzip (.tbz)                   | 输出重定向给bzip2命令 |
| -z     | zip, tells tar command that creates tar file using gzip (.gz) | 输出重定向给gzip命令  |
| -W     | verify a archive file                                        | 确认压缩文件          |
| -r     | update or add file or directory in already existed .tar file | 重新打包              |

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
$ zcat Y.gff3.gz | cut -f 3| grep -v "#"| sort| uniq -c| sort -nk 1
```

-----------------------

## uniq (reports or filters out the repeated lines)

+ uniq isn’t able to detect the duplicate lines unless they are adjacent to each other. The content in the file must be therefore sorted before using uniq or you can simply use `sort` instead of uniq command. 

| Option | Description |                        |
| ------ | ----------- | ---------------------- |
| -c     | count.      | 统计连续出现重复的行数 |
| -d     | repeated.   | 只显示重复行           |
| -u     | unique      | 只显示非重复行         |

```shell
$ cat example.gtf | cut -f 3 | head 20 | sort | uniq -c
```

-----------------

## paste (merge files)

+ It is used to join files horizontally (parallel merging) by outputting lines consisting of lines from each file specified, separated by tab as delimiter, to the standard output.
+ when no file is specified, or put dash (“-“) instead of file name

| Option | Description                  |                  |
| ------ | ---------------------------- | ---------------- |
| -d     | merge the files by delimiter | 按指定分隔符粘贴 |
| -s     | merge the files sequentially | 按行合并         |

```shell
$ paste -d "|," number state capital
1|Arunachal Pradesh,Itanagar
2|Assam,Dispur
3|Andhra Pradesh,Hyderabad
4|Bihar,Patna
5|Chhattisgrah,Raipur

$ paste -s number state capital
1       2       3       4       5
Arunachal Pradesh       Assam   Andhra Pradesh  Bihar   Chhattisgrah
Itanagar        Dispur  Hyderabad       Patna   Raipur

$ seq 20 # 创建20个连续数字，一行一个
$ seq 20 | paste - - # 横着一行两个创建20个连续数字

#Without hypen
$ cut -d " " -f 1 state | paste number
1
2
3
4
5
#With hypen
$ cut -d " " -f 1 state | paste number -
1       Arunachal
2       Assam
3       Andhra
4       Bihar
5       Chhattisgrah
```

---------------------------

## tr (translate)

对文本就行一些操作，比如大小写转换，删除重复字符，类似查找并替换

| Options | Descriptions                                                 |                            |
| ------- | ------------------------------------------------------------ | -------------------------- |
| -c      | complements the set of characters in string .i.e., operations apply to characters not in the given set | 输出除了指定字符以外的字符 |
| -d      | delete characters in the first set from the output           | 删除指定字符               |
| -s      | replaces repeated characters listed in the set1 with single occurrence | 缩减连续重复字符           |

```shell
#convert lower case to upper case
$cat greekfile | tr a-z A-Z
$cat geekfile | tr “[:lower:]” “[:upper:]”

#translate white-space to tabs
$echo "Welcome To GeeksforGeeks" | tr [:space:] '\t'

#translate braces into parenthesis
$tr '{}' '()'   newfile.txt

#squeeze repetition of characters
$echo "Welcome    To    GeeksforGeeks" | tr -s [:space:] ' '
#需要说明的是，有的时候看到的很多个空格(通常是4个)其实是'\t'，在这种情况下用-s参数是没有用的

#delete specified characters
$ echo "Welcome To GeeksforGeeks" | tr -d 'w'

#remove all the digits from the string
$ echo "my ID is 73535" | tr -d [:digit:]
my ID is

#complement the sets 
$ echo "my ID is 73535" | tr -cd [:digit:]
73535
```

-----------------------------

## grep (search)

非常常用的文本搜索工具，配合正则表达式、`less`、`cat`等命令使用

| Option   | Description                                                  |                                       |
| -------- | ------------------------------------------------------------ | ------------------------------------- |
| -w       | get only the pattern as a whole word                         | 精确查找某个关键词                    |
| -c       | count the total number of times that the pattern appears in a file | 统计匹配成功的行                      |
| -v       | versus, match only those lines that do not contain the given word | 反向输出没有匹配的行,相当于过滤的功能 |
| -n       | precede each line of output with the number of the line in the text file where it was obtained | 显示匹配成功的行所在行号              |
| -r       | Look for all files in the current directory                  | 从当前目录中的所有文件中查找          |
| -R       | Look for all files in the current directory and in all of its subdirectories | 从当前目录及下级目录中所有文件查找    |
| -h       | exlclude the file name in the outout data                    | 不在文件名中查找结果                  |
| -e       | match with multiple patterns                                 | 指定多个匹配模式                      |
| -f       | read the pattern from a file                                 | 从指定文件中读取要匹配的模式          |
| -i       | case-insensitive search                                      | 忽略大小写                            |
| -l       | print only names of FILEs with selected lines                | 显示匹配文件                          |
| -- color | display output in colors                                     | 显示颜色增加可读性                    |
| -B N     | display NUMBER lines of before matched context               | 显示匹配成功的前N行                   |
| -A N     | show NUMBER lines of after matched context                   | 显示匹配成功的后N行                   |
| -E       | transform the pattern as Regular Expression                  | 识别pattern中的正则表达式             |

```shell
#grep [option] pattern file
$ less -SN Data/example.gtf | grep -w 'gene'
$ zcat Data/example.gff3.gz | grep -w -e 'gene' -e 'UTR'

#指定文件作为pattern
$ cat file
gene
UTR
start_codon
stop_codon
$ cat Data/example.gtf | grep -w -f file | less -S
```

---------

## sed(stream editor)

+ perform lots of functions on file like searching, find and replace, insertion or deletion without opening them
+ save into a file or you only take a look at what you want to modify

| Option | Description                      |                                         |
| ------ | -------------------------------- | --------------------------------------- |
| -n     | print only the modified lines    | 只显示用sed处理过的内容                 |
| -e     | make multiple selections         | 进行多次修改                            |
| -i     | modified the file without output | 直接修改文件内容，不输出 (真正修改文件) |

```shell
#sed [option] 'script' file
#'[N]s/pattern/new/[flags]'把pattern替换成new，默认替换一次，[flags]指定匹配第几个/g[global], [N]指定第几行

$echo howtogonk | sed 's/gonk/geek/'
howtogeek
$cat readme.txt | sed '1a welcome to Biotrainee'
$cat coleridge.txt| sed -n '1,4p'

#删除空行#
$cat readme.txt | sed '/^$/d'
$grep -v '/^$/d'
#另外一种指定第几行的方法
$cat readme.txt |sed '/www/ s/ee/EE/p' #将含有www的那一行/ee/替换成/EE/

#'[N]y/inchars/outchars/'实现字符一对一转换
cat readme.txt | sed 'y/abcd/ABCD'
```

+ script 的一些说明：

| address   |                                    | command |                           |
| --------- | ---------------------------------- | ------- | ------------------------- |
| 2         | row 2                              | a       | append a row after        |
| 2,4       | row 2 to row 4                     | i       | insert a row before       |
| 2,$       | row 2 to the end                   | d       | delete rows               |
| 2~3       | from row 2, every 3 row to the end | c       | change content of the row |
| 2,+4      | from row 2 to line 2+4             | s       | substitute                |
| /pattern/ | the row match the pattern          | y       | transform                 |
| [!]       | the row doesn't match              | p       | print                     |



----------------

## wget (web servers get)

| Option       | Description                          |                                      |
| ------------ | ------------------------------------ | ------------------------------------ |
| -b           | backgroung                           | 转入后台下载                         |
| -P           | save the file to a specific location | 指定存储文件夹(否则会存到默认文件夹) |
| --limit-rate | limit the download speed             | 限制下载速度                         |
| -c           | continue (resume the download)       | 断点续传                             |
| -i           | download multiple files at once      | 下载多个链接                         |
| -Q           | limit size of file                   | 限制文件大小                         |
| -r           | recursive                            | 递归下载所有文件夹                   |

```shell
#wget [option] URL 
#以不同的文件名保存
$wget -O wordpress.zip http://www.centos.bz/download.php?id=1080

#查看任务进程
$ tail -f wget-log

#下载多个链接
$ cat > linux-distros.txt
http://mirrors.edge.kernel.org/archlinux/iso/2018.06.01/archlinux-2018.06.01-x86_64.iso
https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-9.4.0-amd64-netinst.iso
https://download.fedoraproject.org/pub/fedora/linux/releases/28/Server/x86_64/iso/Fedora-Server-dvd-x86_64-28-1.1.iso
$ wget -i linux-distros.txt

#通过FTP下载
$ wget --ftp-user=FTP_USERNAME --ftp-password=FTP_PASSWORD ftp://ftp.example.com/filename.tar.gz

#测试下载链接,且连接正确
$ wget –spider URL 
Spider mode enabled. Check if remote file exists. 
HTTP request sent, awaiting response… 200 OK 
Length: unspecified [text/html] 
Remote file exists and could contain further links, 
but recursion is disabled — not retrieving. 
```

-----------------

## scp (secure copy)

```shell
#scp [option] file_source file_target 
#本地复制到远程
$scp /home/space/music/1.mp3 root@www.runoob.com:/home/root/others/music 
#远程复制到本地
$scp -r www.runoob.com:/home/root/others/ /home/space/music/
```

| Option | Description                                       |                                              |
| ------ | ------------------------------------------------- | -------------------------------------------- |
| -q     | repress the progress meter and non-error messages | 不显示传输进度条                             |
| -r     | copy files recursively                            | 递归复制整个目录                             |
| -P     | defines the SSH port of the remote host           | 指定数据传输用到的端口号                     |
| -C     | compresses data to speed up file transfer         | 允许压缩                                     |
| -p     | safeguards files from being modified or accessed  | 保留原文件的修改时间，访问时间和访问权限     |
| -v     | show detail (verbose)                             | 详细方式显示输出, 会显示出整个过程的调试信息 |
| -l     | limit                                             | 限制传输宽带                                 |

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

