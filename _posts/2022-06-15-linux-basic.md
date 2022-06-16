

#  linux basic part 1

[生信技能树-linux基础课程及conda精讲](https://www.bilibili.com/video/BV1Yy4y117SX?p=1&vd_source=60b68aa1f5472a5d937a802533f649ab)

> 写在前面

+ 电脑配置
  + 处理器：11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz   2.80 GHz （4个双核CPU）
  + 机带RAM：16GB
+ 为了学习Linux用VMWare在D盘中做了一个虚拟器，安装了Ubuntu linux系统，然而后来买了服务器之后其实并没有怎么用就卸载了，但前期用来学习简单命令和试错还是很好用的，第一次连接服务器前如果不用软件的话也需要linux系统generate一些权限之类的东西
+ 连接远程环境需要配置软件，学会用很重要！！
  + **连接服务器** Xshell/ win+R input cmd (Windows); Termius (MacOS)
  + **传输数据** Xftp/FileZilla (Windows); FileZilla (MacOS)
  + **写各种语言命令** sublime
  + **可视化美化日记排版** Markdown
+ **目前服务器**
  + **wcm**:   $ ssh yiw4007@scu-login02.med.cornell.edu                               *CentOS*
  + **biotrainee**: $ ssh t100334@biotrainee.vip 8861 (pw: pd6445)              *Ubuntu*

------------------------

## 连接远程服务器前的电脑准备

因为两个服务器都给了不一样的Instruction，所以这里记录两种方式：

```shell
#First, check to see if you have ssh keys set up:
ls -ltr ~/.ssh
#If the output shows the files id_rsa and id_rsa.pub,you already have keys in place. 
#Then,Skip the following command and continue to authorizing your key.

#If the output does not show those files, then generate them :
ssh-keygen -t rsa -b 4096
#Follow the instructions on screen. Accept the default location. 

#Authorizing your key
cd ~/.ssh
cat id_rsa.pub >> authorized_keys
```

```shell
#安装ssh服务，默认22端口访问特定IP地址的服务器
sudo apt-get install openssh-server
sudo apt-get install net-tools  #为了可以运行ifconfig命令
ifconfig           
```



----------------------

## 新服务器配置

+ 修改命令行配色 (虽丑但好用) [Ref](https://www.bilibili.com/read/cv16075351)

  ```shell
  echo  'export PS1="\[\033]2;\h:\u \w\007\033[33;1m\]\u \033[35;1m\t\033[0m \[\033[36;1m\]\w\[\033[0m\]\n\[\e[32;1m\]$ \[\e[0m\]"' >> ~/.bashrc
  source  ~/.bashrc  #重启系统常用代码
  ```

+ 查看系统设置 (看看我买了个什么玩意) [Ref1](https://www.bilibili.com/video/BV1XW411d7Bp?p=1&vd_source=60b68aa1f5472a5d937a802533f649ab) [Ref2](https://blog.csdn.net/qq_31555951/article/details/106624010)

  ```shell
  #使用free命令查看内存(show total,used memory,free,shared,available memory)
  free -g
  #查看存储系统信息的文件
  cat /proc/cpuinfo 
  #查看CPU物理个数
  grep ‘physical id’ /proc/cpuinfo | sort -u | wc -l
  #查看CPU核心数
  grep ‘core id’ /proc/cpuinfo | sort -u | wc -l #硬件信息
  #查看CPU线程数
  cat /proc/cpuinfo | grep processor|wc
  grep ‘processor’ /proc/cpuinfo | sort -u | wc -l
  ```
  
  小知识：CPU核心数（core）、线程数（processor/thread）的区别

  CPU的核心数指的是硬件上存在着几个核心，而线程数可以模拟出多个核心数的功能。线程数越多，越有利于同时运行多个程序，因为线程数等同于在某个瞬间CPU能同时并行处理的任务数。一个核心最少对应一个线程，但通过超线程技术，一个核心可以对应两个线程，也就是说它可以同时运行两个线程。
  
  所以买电脑的时候所谓性能好，其中条件之一就是要么有多个高级的（可以同时处理更多事情的）CPU核心
  
  ```shell
  #查看内存 df命令(df = disk free)
  df -h                   #/根目录下的内存对应的是总内存
  #查看服务器硬盘信息
  cat /proc/scsi/scsi
  #如果有高级权限的话可以用sudo fdisk分区挂载等等，mount指挂载的位置
  ```
  
  具体服务器运维管理参考[Ref](https://mp.weixin.qq.com/s/siHnqPQq1in0WK2J2TnAhg), 然而我不配。
  
  还可以查看一下系统
  
  ```shell
  # “uname”  (Unix Name), print detailed information about the machine name, Operating System and Kernel
  uname -a
  ```
  
+ R语言相关环境配置 [Ref](https://mp.weixin.qq.com/s/rR3FMXg3ye36XedolN6yww)

+ 其他服务器配置[Ref](weixin://resourceid/blank)

--------------

> 正则表达式、常用通配符、常用命令

## linux快捷键 (Linux Bash Terminal Keyboard Shortcuts)

[Ref1](https://www.makeuseof.com/linux-bash-terminal-shortcuts/)

[Ref2:10:24](https://www.bilibili.com/video/BV1Yy4y117SX?p=4&vd_source=60b68aa1f5472a5d937a802533f649ab)

| Shortcut           | Action                                                       |                          |
| ------------------ | ------------------------------------------------------------ | ------------------------ |
| Tab                | Autocompletes the command or file/directory name             | 补全                     |
| Tab Tab            | when `Tab`doesn't work, show all choices                     | 查看补全的选项           |
| Crtl+C             | Sends SIGI signal and kills currently executing command      | 终止任务                 |
| Ctrl + Z           | Suspends current command execution and moves it to the background (use `fg` command to come back) | 暂停任务                 |
| Ctrl + S/Q         | Stops/ Resumes command output to the screen                  | 暂停/继续屏幕输出        |
| Ctrl + A/E         | Move to the start/end  of the command line                   | 回到行首/尾              |
| Alt + B / Ctrl+`←` | Moves the cursor one word backward                           | 向后挪动一个单词的光标   |
| Alt + F / Ctrl+`→` | Moves the cursor one word forward                            | 向前挪动一个单词的光标   |
| `↑`/`↓`            | Moves to previous/next command                               | 上/下一条命令            |
| Crtl + `↑`/`↓`     | Read last/next page                                          | 屏幕输出向上/下翻页      |
| Ctrl + l           | Similar to clear command, clears the terminal screen         | 清屏                     |
| Ctrl + R           | Incremental reverse search of bash history                   | 寻找历史命令             |
| Ctrl + W           | Removes the command/argument before the cursor               | 剪切光标前的单词         |
| Crtl + Y           | Paste what you removed                                       | 粘贴命令行剪切的内容     |
| Ctrl + U           | Remove before the cursor until the start of the command      | 剪切光标位置到行首的内容 |
| Ctrl + K           | Remove after the cursor until the end of the command         | 剪切光标位置到行尾地内容 |
| Ctrl + \           | Remove all the blanks before the cursor                      | 删除光标前所有字符       |
| Shift + Insert     | Paste (equals to Crtl+V in windows)                          | 粘贴                     |

命令行窗口中选中即复制，右键粘贴，鼠标滚轮向下按就会出现下拉菜单（像Windows中的右键一样） 

如果不是的话可以在X shell或者系统中设置一下



## 正则表达式 (Regular Expression, regex/ regexp/ RE)

一开始觉得这个也没有那么重要，毕竟我们只是要用别人的命令又不是要编脚本。然后后来实际操作了一两次之后发现作为一个只能用命令行交互的系统，学会查看、查找、筛选输出内容是多么地重要T^T。所以单独在这里会配合grep命令记录一下，实时更新。[Ref 07:35](https://www.bilibili.com/video/BV1Yy4y117SX?p=12&vd_source=60b68aa1f5472a5d937a802533f649ab)  [Ref](https://tldp.org/LDP/abs/html/x17129.html) 

A Regular Expression contains one or more of the following:

- ***A character set***. These are the characters retaining their literal meaning. The simplest type of Regular Expression consists *only* of a character set, with no metacharacters.
- ***An anchor***. These designate (*anchor*) the position in the line of text that the RE is to match. For example, ^, and $ are anchors.
- ***Modifiers***. These expand or narrow (*modify*) the range of text the RE is to match. Modifiers include the asterisk, brackets, and the backslash.

| Expression                              | Symbol    | Meaning                                                      |                                                | Example                         |
| --------------------------------------- | --------- | ------------------------------------------------------------ | ---------------------------------------------- | ------------------------------- |
| asterisk                                | *         | any number of repeats of the character string or RE preceding it, including *zero* instances. | 匹配0次或多次符号前的内容                      | grep 'f*ee'                     |
| dot                                     | .         | matches any one character, except a newline.                 | 换行符以外的任意单个字符                       | grep 'f.ee'                     |
| caret                                   | ^         | matches the **beginning of a line**, but sometimes, depending on context, **negates** the meaning of a set of characters | 行首，在特定情况下也表示否定或除了             | grep '^T' or grep \[^Tt]        |
| dollar sign                             | $         | at the end of an RE matches the end of a line                | 行尾                                           | grep 'ee$'                      |
| brackets       (square brackets)        | []        | enclose a set of characters to match in a single RE          | 匹配任意一个字符                               | grep [xyz]                      |
|                                         |           | matches any one of the characters in the range               | 匹配范围内任意一个                             | [c-n] or        [B-Pk-y]        |
|                                         |           | matches any single lowercase letter or any digit             | 匹配任意小写字母和数字                         | [a-z0-9]                        |
|                                         |           | matches any character *except* those in the range            | 匹配除了这些字符以外的内容                     | \[^b-d]                         |
| backslash                               | \         | [escapes](https://tldp.org/LDP/abs/html/escapingsection.html#ESCP) a special character, which means that character gets interpreted literally (and is therefore no longer *special*). | 转译，至于从什么转成什么那就具体情况具体分析了 | ‘My\ data'                      |
| escaped angle bracket     (chevron)     | \\<...\\> | word boundaries. "\<the\>" matches the word "the," but not the words "them," "there," "other," etc. | 作为一个整体                                   | grep '\\<the\\>' textfile       |
| question mark                           | ?         | zero or one of the previous RE                               | 匹配符号前0次或1次                             | grep ’f\?ee‘                    |
| plus                                    | +         | one or more of the previous RE                               | 匹配符号前1次或多次                            | grep ’fre\\+‘                   |
| vertical bar                            | \|        | matches any of a set of alternate characters.                | 或                                             | ’re(a\|e)d‘         'UTR\|exon' |
| parentheses            (round brackets) | ()        | enclose a group of REs                                       | 强调整体，常与\|连用                           |                                 |
| brace                (curly brackets)   | {}        |                                                              |                                                |                                 |
|                                         |           |                                                              |                                                |                                 |



个人觉得英文解释比中文更好理解，更符合语言习惯，但为了看着方便还是把中文加上。这里需要说明的是RE中指代的都是符号前的内容（也就是RE preceding it）。

不过说个题外话，linux，shell，bash都是常见的我们会提及的概念，但真正理解他们还是在实际操作中才会明白。名词解释这种东西考试考它还是有一定道理的。

------------------------

## 待整理: CUT&RUN 流程化分析

 

[^1]: code一定要注意大小写