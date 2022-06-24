

# 生物信息学环境配置

{:toc}

## 生物信息学常见数据格式

| File format | Information                                                  |
| ----------- | ------------------------------------------------------------ |
| fasta       | text-based format to represent nucleotide or protein sequences |
| fastq       | store both sequence and associated quality values            |
| gff/gtf     | tab-delimited text file that holds information any and every feature that can be applied to a nucleic acid or protein sequence |
| bam         | A BAM file (.bam) is the binary version of a SAM file. A SAM file (.sam) is a tab-delimited text file that contains sequence alignment data[^1]. |
| bai         |                                                              |
| bw          |                                                              |
| narrowPeak  |                                                              |
| broadPeak   |                                                              |
| bed         |                                                              |

----------------

### Fasta

+ 基于文本表示核酸序列或多肽序列
  + **id行**：以 '>' 符号开头，有时会包含注释信息
  + **序列行**：一个字母表示一个碱基/氨基酸

### Fastq[^2]

+ 存储生物序列以及相应的质量评价的文本格式（fasta+qual=fastq）
  + **id行**：以@开头，记录必要信息
  + **序列行**：一个字母表示一个碱基/氨基酸
  + **附加信息行**：没有注释的话会以“+”显示，有的话会和第一行是一样的
  + **碱基质量行**：PHRED值 （根据ASCII表，用1个字符表示1个碱基的好坏）

 ### gff/gtf

+ 记录序列中转录起始位点、基因、外显子、内含子等组成元件在染色体中的位置信息。目前gff到第三版，gtf到第二版gtf，即gff3，gtf2。
+ 可以**用cufflinks里的gffread命令互相转换格式**
+ Sequence ID/seqname
  + The name of the sequence where the feature is located.

+ Source
  - Describes the algorithm or the procedure that generated this feature. e.g. Augustus, RepeatMasker, Genescane or Genebank. (.) is used if it's unknown.
+ Feature Type
  - Describes what the feature is (mRNA, domain, exon, etc.).
  - These terms are constrained to the [Sequence Ontology terms](http://www.sequenceontology.org/).
+ Feature Start
  + Start from 1 (which bed file starts from 0)
+ Feature End
+ Score
  - Typically E-values for sequence similarity and P-values for predictions.  (.) is used if it's empty.
+ Strand
  + "+": positive strand
  + "-": negative strand
  + ".": no specific statement needed
  + "?": unkown
+ Phase/frame
  - Indicates where the feature begins with reference to the reading frame. The phase is one of the integers 0, 1, or 2, indicating the number of bases that should be removed from the beginning of this feature to reach the first base of the next codon.
+ Atributes
  - A semicolon-separated list of tag-value pairs, providing additional information about each feature. Some of these tags are predefined, e.g. ID, Name, Alias, Parent . You can see the full list [here](https://github.com/The-Sequence-Ontology/Specifications/blob/master/gff3.md).
  - gtf file has to include: **gene_id value** and **transcript_id value**

### bam





--------------------------

## 其他一些生物学知识补充

+ Ambiguous base 模糊碱基

  'R': ['A','G'], 'Y': ['C','T','U'], 'M': ['A','C'], 'K': ['G','T'], 'S': ['C','G'], 'W': ['A','T'], 'H': ['A','C','T'], 'B': ['C','G','T'], 'V': ['A','C','G'], 'D': ['A','G','T'],'N': ['A','C','G','T']





-------------

## 环境设置及软件安装



### Conda安装

+ 我们说的Conda全称是[ANACONDA](http://www.anaconda.com/)，是一个所有语言的包、依赖和环境管理器。另外有一个类似于conda的工具叫Mamba
+ MiniConda是工作台

```shell
#官网安装下载
$ wget -c https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh

#国内镜像安装:北京外国语大学下载
$ wget -c https://mirrors.bfsu.edu.cn/anaconda/miniconda/Miniconda3-latest-Linux-x86_64.sh

#Mac下载
$curl -O  https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
$curl -O https://mirrors.bfsu.edu.cn/anaconda/miniconda/Miniconda3-latest-Linux-x86_64.sh

#安装：运行.sh脚本
$ bash Miniconda3-latest-Linux-x86_64.sh
#运行过程中打错字要用Ctrl+Backspace删除

#默认在base环境是显示的，也可以不显示
$conda config --set auto_activate_base false
$source ~/.bashrc #更改设置后需要重启一下

#更新Conda
$conda update conda

#卸载Conda:直接删除安装目录
$rm -rf ~/miniconda
```

-----------------

### Conda配置频道和环境

+ [国内Conda镜像](https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/): 查看完整列表中有所有已维护的Conda频道

+ 官方频道

  ```shell
  $conda config --add channels bioconda
  $conda config --add channelsconda-forge
  $conda config --set show_channel_urls yes
  ```

+ 清华镜像频道

  ```shell
  $conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  $conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
  $conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
  $conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda/
  $conda config --set show_channel_urls yes
  ```

+ 北外镜像频道

  ```shell
  $conda config --add channels https://mirrors.bfsu.edu.cn/anaconda/pkgs/free/
  $conda config --add channels https://mirrors.bfsu.edu.cn/anaconda/pkgs/main/
  $conda config --add channels https://mirrors.bfsu.edu.cn/anaconda/cloud/conda-forge/
  $conda config --add channels https://mirrors.bfsu.edu.cn/anaconda/cloud/bioconda/
  $conda config --set show_channel_urls yes
  ```

  其他镜像：[南京大学](https://mirrors.nju.edu.cn/anaconda/) [上海交通大学](https://mirrors.sjtu.edu.cn/anaconda/)

+ 不要重复添加频道，后添加的优先级高

+ 添加镜像看服务器的位置，而不是使用者位置

+ 有的时候defaults频道会影响下载和安装，不需要的话可以删掉,`$vim ~/.condarc` 进行删除

  ```shell
  # 查看已添加的频道：
  $ cat ~/.condarc
  $ conda config --get channels
  $ conda config --show channels
  ```

+ base环境里最好不要装任何包，用不同的环境做不同的project，否则一旦冲突排查问题会很难或者都需要重装。但需要在所有环境用的软件还是要装在base环境里，比如mamba

  ```shell
  #创建独立环境,-n指定名称,同时可以指定语言及版本
  $ conda create -n rnaseq
  $ conda create -n pyt2 python=2.7
  #启动环境
  $ conda activate rnaseq
  #退出环境
  $ conda deactivate
  #查看环境列表
  $ conda env list 
  $ conda info --env
  #复制环境
  $ conda create -n pyt2 --clone Python2
  #删除环境
  $ conda remove -n rnaseq --all #删除环境中所有内容
  ```

--------------------

### Conda软件安装

+ 查询可以在Conda中安装的软件或包
  + 网站查询：[anaconda](http://anaconda.org/search) [bioconda](https://bioconda.github.io)
  + 命令行查询：`$ conda search fastqc` 用命令行查询的话要保证输入的软件名称是对的
  + 关键词查询： 搜索引擎 搜索 fastqc conda

+ **安装时记住要在特定环境中安装！**如果环境中没有的依赖软件，Conda会自动安装

```shell
$conda install fastqc
#如果不指定版本会默认安装最新版
$conda install fastqc=0.11.7
#跳过确认步骤,且多个软件可以同时安装
$conda install -y fastqc=0.11.7 miltiqc

#配合正则表达式查看已有软件
$conda list fast*
#查看指定的环境的软件,默认当前环境
$conda list -n rnaseq
#安装软件到特定位置,注意指定位置的话conda不会生成文件夹，需要自己创建
$mkdir -p ~/smatools
$conda install -p ~/samtools samtools
#删除软件
$conda remove -n rnaseq -y fastqc

#升级软件
$conda update fastqc
#降级软件=>安装特定版本的软件
```

+ 安装好的软件直接用`[软件名] -h`可以查看帮助文档的话则说明安装成功，不可以的话退出环境重进或者重启conda也是可以的

```shell
#软件/环境迁移
$ conda list [name] #查看某个软件的版本
#导出环境
$ conda env export -n rnaseq > rnaseq.yml
#导出环境中安装的包列表
$ conda list -n rnaseq --export > conda_rnaseq_list.txt
#根据导出的yml文件创造环境
$ conda env create -f rnaseq.yml
$ conda env update -f rnaseq.yml    #更新环境
#安装导出的信息
$ conda create -n rna -file conda_rnaseq_list.txt
#本地安装
$ wget -c URL 
$ conda --use-local link
#查看安装包装在哪
$ conda which python
```

+ `conda clean`清理环境

  | Option | Description |                        |
  | ------ | ----------- | ---------------------- |
  | -i     | index-cache | 清除目录（镜像之类的） |
  | -a     | all         | 清除所有缓存           |
  | -p     | packages    | 清除安装包的缓存       |
  | -t     | tarballs    | 清除下载的压缩包缓存   |

+ 为当前环境设置特殊频道

  `$ conda config --env --add channels genomedk`

+ 报错查询

  | Situation                  | Reason                                                       | Solution                                                     |
  | -------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | HTTP 000 Connection failed | No internet or poor internat connection                      | verify the internet connection<br>try the mission again<br>delete the default channel in ~/.condarc<br>try mamba |
  | Solving environment        | the portal of https(443) was stopped by security. http(80) is better | change the mirror `https` to `http`                          |
  | mismatch of tar archive    | the download was incomplete                                  | download package again                                       |

-----------------------

### Mamba

+ [mamba](https://github.com/mamba-org/mamba) 只是在conda的基础上加速了一些，以及新增了一些功能

```shell
$conda activate base
$conda install mamba

#除启动环境外，所有的软件操作都可以用mamba代替
$mamba search fastqc
$mamba repoquery search fastqc #新增的更快地搜索
$mamba install fastqc

#查看软件之间的依赖关系
$mamba repoquery depends -t samtools
$mamba repoquery whoneeds -t python

```

----------

[^1]:   https://software.broadinstitute.org/software/igv/BAM           
[^2]: https://support.illumina.com/bulletins/2016/04/fastq-files-explained.html
