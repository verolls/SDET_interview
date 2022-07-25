# 目录操作命令
## ls
作用：显示目录下的内容  
使用格式：`ls [选项] [文件名或目录名]`  
选项：

```bash
-a：显示所有文件(包括隐藏文件)
-d：显示目录信息
-h：人性化显示，按照我们习惯的单位显示文件大小
-i：显示文件的inode
-l：长格式显示
```

举例：

```bash
[veroll@localhost ~]$ ls -lai
total 16
51300144 drwx------. 4 veroll veroll 103 Jul 11 04:12 .
33592566 drwxr-xr-x. 3 root   root    20 Jul 11 03:57 ..
51300145 -rw-r--r--. 1 veroll veroll  18 Mar 31  2020 .bash_logout
51300146 -rw-r--r--. 1 veroll veroll 193 Mar 31  2020 .bash_profile
51300147 -rw-r--r--. 1 veroll veroll 231 Mar 31  2020 .bashrc
16793039 drwxrwxr-x. 3 veroll veroll  18 Jul 11 03:58 .cache
51084930 drwxrwxr-x. 3 veroll veroll  18 Jul 11 03:58 .config
51300154 -rw-rw-r--. 1 veroll veroll  13 Jul 11 04:13 demo
```
- 第一列：文件inode
- 第二列：权限
- 第三列：引用计数。文件的引用计数代表该文件的硬链接个数，目录的引用计数代表该目录有多少个一级子目录。
- 第四列：所有者，也就是这个文件属于哪个用户。默认所有者是文件的建立用户。
- 第五列：所属组。默认所属组是文件建立用户的有效组，一般就是建立用户的所在组。
- 第六列：大小。默认单位是字节。
- 第七列：文件修改时间。文件状态或文件数据被修改都会更改这个时间。
- 第八列：文件名

## cd
作用：切换所在目录  
使用格式：`cd [路径]`  
符号：

```bash
~：切换至当前用户的家目录
-：切换至上次所在目录
.：表示当前目录
..：表示上级目录
```

举例：

```bash
[veroll@localhost ~]$ cd /
[veroll@localhost /]$ cd ~
[veroll@localhost ~]$ cd ../../lib
[veroll@localhost lib]$ cd ./kernel/
[veroll@localhost kernel]$ cd -
/lib
[veroll@localhost lib]$
```

## pwd
作用：查询所在工作目录  
使用格式：`pwd`  
举例：  

```bash
[veroll@localhost lib]$ pwd
/lib
```
## mkdir
作用：创建空目录  
使用格式：`mkdir [选项] 目录名`  
选项：  

```bash
-p：递归建立所需目录。即创建多级目录时需要加上-p选项。
```

举例：

```bash
[veroll@localhost ~]$ mkdir menu1

# 创建一个多层级目录
[veroll@localhost ~]$ mkdir -p menu2/name

# 同时创建多个目录
[veroll@localhost ~]$ mkdir menu3 menu4
```

## rmdir
作用：能且只能删除空目录(一旦目录中有内容，该命令就会报错，无论删除文件还是命令，通常使用`rm`命令)  
使用格式：`rmdir [选项] 目录名`  
选项：  

```bash
-p：递归建立所需目录。即创建多级目录时需要加上-p选项。
```

# 文件操作命令
## touch
作用：创建空文件或修改文件的时间戳  
使用格式：`touch 文件名`  
举例：

```bash
[veroll@localhost ~]$ ls -l
total 4
-rw-rw-r--. 1 veroll veroll 13 Jul 11 04:13 demo
[veroll@localhost ~]$ touch demo
[veroll@localhost ~]$ ls -l
total 4
-rw-rw-r--. 1 veroll veroll 13 Jul 11 04:40 demo

# 批量创建100个文件
[veroll@localhost test_100]$ touch test{001..100}.txt
[veroll@localhost test_100]$ ls
test001.txt  test018.txt  test035.txt  test052.txt  test069.txt  test086.txt
test002.txt  test019.txt  test036.txt  test053.txt  test070.txt  test087.txt
test003.txt  test020.txt  test037.txt  test054.txt  test071.txt  test088.txt
test004.txt  test021.txt  test038.txt  test055.txt  test072.txt  test089.txt
test005.txt  test022.txt  test039.txt  test056.txt  test073.txt  test090.txt
test006.txt  test023.txt  test040.txt  test057.txt  test074.txt  test091.txt
test007.txt  test024.txt  test041.txt  test058.txt  test075.txt  test092.txt
test008.txt  test025.txt  test042.txt  test059.txt  test076.txt  test093.txt
test009.txt  test026.txt  test043.txt  test060.txt  test077.txt  test094.txt
test010.txt  test027.txt  test044.txt  test061.txt  test078.txt  test095.txt
test011.txt  test028.txt  test045.txt  test062.txt  test079.txt  test096.txt
test012.txt  test029.txt  test046.txt  test063.txt  test080.txt  test097.txt
test013.txt  test030.txt  test047.txt  test064.txt  test081.txt  test098.txt
test014.txt  test031.txt  test048.txt  test065.txt  test082.txt  test099.txt
test015.txt  test032.txt  test049.txt  test066.txt  test083.txt  test100.txt
test016.txt  test033.txt  test050.txt  test067.txt  test084.txt
test017.txt  test034.txt  test051.txt  test068.txt  test085.txt

```
## stat
作用：显示文件或文件系统的详细信息  
使用格式：`stat 文件名`  
举例：

```bash
[veroll@localhost ~]$ stat demo
  File: ‘demo’
  Size: 13              Blocks: 8          IO Block: 4096   regular file
Device: fd00h/64768d    Inode: 51300154    Links: 1
Access: (0664/-rw-rw-r--)  Uid: ( 1000/  veroll)   Gid: ( 1000/  veroll)
Context: unconfined_u:object_r:user_home_t:s0
Access: 2022-07-11 04:40:04.581812152 -0400
Modify: 2022-07-11 04:40:04.581812152 -0400
Change: 2022-07-11 04:40:04.581812152 -0400
 Birth: -
```

stat翻译：

```bash
[veroll@localhost ~]$ stat demo
  File: 文件
  Size: 大小            Blocks: 块         IO Block: IO块   regular file(普通文件)
Device: 设备   Inode: 索引节点    Links: 硬链接数
Access: 权限  Uid:用户ID    Gid: 组ID
Context: 环境
Access: 文件访问时间
Modify: 数据修改时间
Change: 状态修改时间
 Birth: 创建时间
```

## cat
作用：合并文件并打印输出到标准输出，即查看文件内容。  
使用格式：`cat [选项] 文件名`  
选项：

```bash
-A：相当于-vET选项的整合，用于列出所有隐藏符号
-v ：列出特殊字符
-E：列出每行结尾的回车符
-T：把Tab建用^T显示出来
-n：显示行号
```

举例：

```bash
[veroll@localhost ~]$ cat -An demo
     1  Hello World!$
     2  Hello$
     3  World!$
     4  W$
```

## more
作用：分屏显示文件内容  
使用格式：`more 文件名`  
举例：  
使用该命令后会打开一个交互界面，可以识别一些交互命令。常用的交互命令有：

```bash
空格键：向下翻页
b：向上翻页
回车键：向下滚动一行
/字符串：搜索指定字符串
q：推出交互界面模式
```

## less
作用：分行显示命令  
使用格式：`less 文件名`

## head
作用：显示文件开头的内容  
使用格式：`head [选项] 文件名`  
选项：

```bash
-n 行数：从文件头开始，显示指定行数
-v：显示文件名
```

举例：

```bash
[veroll@localhost ~]$ head -vn2 demo
==> demo <==
Hello World!
Hello
```

## tail
作用：显示文件结尾的内容  
使用格式：`tail [选项] 文件名`  
选项：

```bash
-n 行数：从文件结尾开始，显示指定行数
-f：监听文件的新增内容，即实时查看文件内容
```

举例：

```bash
# 查看文件最后两行内容
[veroll@localhost ~]$ tail -n2 demo
World!
W
```

## vim
基本上 vim 共分为三种模式，分别是**命令模式（Command mode）**，**输入模式（Insert mode）**和**底线命令模式（Last line mode）**。 这三种模式的作用分别是：  
### 命令模式(也称为一般模式)
用户刚刚启动 vi/vim，便进入了命令模式。

此状态下敲击键盘动作会被Vim识别为命令，而非输入字符。比如我们此时按下i，并不会输入一个字符，i被当作了一个命令。  

以下是常用的几个命令：
- i ：切换到输入模式，以输入字符。
- : ：切换到底线命令模式，以在最底一行输入命令。
- h 或 向左箭头键(←)：光标向左移动一个字符
- j 或 向下箭头键(↓)	：光标向下移动一个字符
- k 或 向上箭头键(↑)：光标向上移动一个字符
- l 或 向右箭头键(→)：光标向右移动一个字符
- G：移动到这个档案的最后一行
- nG：n 为数字。移动到这个档案的第 n 行。例如 20G 则会移动到这个档案的第 20 行
- gg：移动到这个档案的第一行，相当于 1G  
- /word：向光标之下寻找一个名称为 word 的字符串。
- dd：删除游标所在的那一整行
- yy：复制游标所在的那一行
- p, P：p 为将已复制的数据在光标下一行贴上，P 则为贴在游标上一行

若想要编辑文本：启动Vim，进入了命令模式，按下i，切换到输入模式。

命令模式只有一些最基本的命令，因此仍要依靠底线命令模式输入更多命令。
### 输入模式(也称为编辑模式)
在命令模式下按下i就进入了输入模式。

按ESC键可随时退出输入模式。

### 底线命令模式(也称为指令行模式)
在命令模式下按下:（英文冒号）就进入了底线命令模式。

底线命令模式可以输入单个或多个字符的命令，可用的命令非常多。

在底线命令模式中，基本的命令有：

- :w：将编辑的数据写入硬盘档案中
- :wq：储存后离开，若为 :wq! 则为强制储存后离开 
- :q：离开 vi 
- :q!：若曾修改过档案，又不想储存，使用 ! 为强制离开不储存档案。

按ESC键可随时退出底线命令模式。

### 三种模式的转换示意图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210127135222902.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L21haG9vbjQxMQ==,size_16,color_FFFFFF,t_70)

## ln
作用：在文件之间建立链接  
使用格式：`ln [选项] 源文件 目标文件`  
选项：  

```bash
-s：建立软链接文件。如果不加`-s`选项，则建立硬链接文件。
-f：如果目标文件已存在，则强制删除目标文件后再建立链接文件。
```

举例：
- 创建硬链接
```bash
[veroll@localhost ~]$ ln demo demo_hard
[veroll@localhost ~]$ ls -li
total 8
51084931 -rw-rw-r--. 2 veroll veroll 28 Jul 11 04:59 demo
51084931 -rw-rw-r--. 2 veroll veroll 28 Jul 11 04:59 demo_hard
```
- 创建软链接

```bash
[veroll@localhost ~]$ ln -s demo demo_soft
[veroll@localhost ~]$ ls -li
total 8
51084931 -rw-rw-r--. 2 veroll veroll 28 Jul 11 04:59 demo
51084931 -rw-rw-r--. 2 veroll veroll 28 Jul 11 04:59 demo_hard
51084929 lrwxrwxrwx. 1 veroll veroll  4 Jul 11 05:12 demo_soft -> demo
```


# 目录和文件都能操作的命令
## rm
作用：删除文件或删除目录  
使用格式：`rm [选项] 文件或目录`  
选项：  

```bash
-f：强制删除
-i：交互删除，在删除前会询问用户
-r：递归删除，删除非空目录时使用-r
```
举例：

```bash
# 强制删除目录及目录内的文件
[veroll@localhost ~]$ rm -rf ./tmp/
```


## cp
作用：复制文件或目录  
使用格式：`cp [选项] 源文件或目录 目标文件或目录`  
选项：  

```bash
-a：相当于-dpr选项的集合
-d：如果源文件为软链接(对硬链接无效)，则复制出的目标文件也为软链接
-p：复制后目标文件保留源文件的属性(包括所有者、所属组、权限、修改时间)
-r：递归复制，复制非空目录时使用该选项
-i：交互复制，如果目标文件已经存在，则会询问是否覆盖
```

举例：

```bash
# 复制一个文件夹
[veroll@localhost ~]$ cp -r test_100/ ./output/
```

## mv
作用：移动文件或目录，给文件或目录改名  
使用格式：`mv [选项] 源文件或目录 目标文件或目录`  
选项：   

```bash
-f：强制覆盖，如果目标文件已经存在，则不询问，直接强制覆盖
-i：交互移动，如果目标文件已经存在，则询问用户是否覆盖
-v：显示详细信息
```

举例：

```bash
# 如何同时移动多个文件
[veroll@localhost test_100]$ mv test003.txt test004.txt ../output/
```

# 用户权限管理命令
## chmod
作用：修改文件或目录的权限模式  
使用格式：`chmod [选项] 权限模式 文件或目录`  
选项：  
```bash
-R：递归设置权限，也就是给子目录中的所有文件设定权限
```

举例：

```bash
# 给一个文件设置最高权限
[veroll@localhost ~]$ chmod 777 demo
[veroll@localhost ~]$ ls -l
total 8
-rwxrwxrwx. 2 veroll veroll 28 Jul 11 04:59 demo
```

```bash
[veroll@localhost ~]$ chmod -R 777 test
[veroll@localhost ~]$ ls -l
total 8
drwxrwxrwx. 2 veroll veroll  6 Jul 11 22:29 test
```

## chown
作用：修改文件或目录的所有者和所属组  
使用格式：`chown [选项] 所有者:所属组 文件或目录`  
选项：  
```bash
-R：递归设置权限，也就是给子目录中的所有文件设定权限
```

注意：普通用户不能修改文件的所有者，哪怕自己是这个文件的所有者也不行；普通用户可以修改所有者是自己的文件的权限。

## chgrp
作用：修改文件或目录的所属组  
使用格式：`chown [选项] 所属组 文件或目录`  
选项：

```bash
-R：递归设置权限，也就是给子目录中的所有文件设定权限
```




# Bash常用命令
## echo
作用：输出  
使用格式：`echo [选项] [输出内容]`  
选项：  
 
```bash
-e：支持反斜线控制的字符转换
-n：内容输出后不换行
```

举例：

```bash
# 取消换行
[veroll@MiWiFi-CR8809-srv ~]$ echo -n "Hello World"
Hello World[veroll@MiWiFi-CR8809-srv ~]$

# 输出中使用控制字符制表符
[veroll@MiWiFi-CR8809-srv ~]$ echo -e "Hello\tWorld"
Hello   World

```


## history
作用：查看历史命令  
使用格式：`history [选项] [历史命令保存文件]`  
选项：  

```bash
-c：清空历史命令
-w：把缓存中的历史命令写入历史命令保存文件。如果不指定保存文件，则放入默认历史命令保存文件~/.bash_history
```

举例：

```bash
# 把缓存的历史命令直接写入~/.bash_history
[veroll@MiWiFi-CR8809-srv ~]$ history -w

# 清空历史命令
[veroll@MiWiFi-CR8809-srv ~]$ history -c
```

## alias
作用：查看或设置命令的别名  
使用格式：`alias [别名=原命令]`  
举例：  

```bash
# 查询系统中已经定义好的别名
[veroll@MiWiFi-CR8809-srv ~]$ alias
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'
alias grep='grep --color=auto'
alias l.='ls -d .* --color=auto'
alias ll='ls -l --color=auto'
alias ls='ls --color=auto'
alias vi='vim'
alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'

# 设定vim命令的别名是vi
# 注意：这样设置的别名在系统重启后会失效，为了让别名永久生效，需要把别名写入环境变量配置文件~/.bashrc中
[root@MiWiFi-CR8809-srv ~]# alias vi='vim'

```

## 重定向符号: >
作用：已覆盖的方式，把命令的正确输出输出到指定的文件或设备当中    
使用格式：`命令 > 文件`

## 重定向符号: >>
作用：已追加的方式，把命令的正确输出输出到指定的文件或设备当中     
使用格式：`命令 >> 文件`

## wc
作用：统计数目  
使用格式：`wc [选项] [文件名]`  
选项：  

```bash
-c：统计字节数
-w：统计单词数
-l：统计行数
```
举例：

```bash
# 统计历史命令文件的行数
[veroll@MiWiFi-CR8809-srv ~]$ wc -l .bash_history
203 .bash_history
```

## 管道符|
作用：管道符前命令的输出作为管道符后命令的操作对象  
使用格式：`命令1 | 命令2`  
举例：  

```bash
# 在/etc/目录下的文件中搜索文件名中包含yum的文件
[veroll@localhost ~]$ ls -la /etc/ | grep 'yum'
drwxr-xr-x.  6 root root      100 Jul 11 03:54 yum
-rw-r--r--.  1 root root      970 Oct  1  2020 yum.conf
drwxr-xr-x.  2 root root      220 Oct  1  2020 yum.repos.d

# 统计正在连接的网络连接数量
[veroll@localhost ~]$ netstat -an | grep 'ESTABLISHED' | wc -l
5
```

# 搜索命令
## whereis
作用：搜索二进制命令、源文件和帮助文档  
使用格式：`whereis [命令]`  
举例：

```bash
[veroll@MiWiFi-CR8809-srv ~]$ whereis grep
grep: /usr/bin/grep /usr/share/man/man1/grep.1.gz /usr/share/man/man1p/grep.1p.gz
[veroll@MiWiFi-CR8809-srv ~]$ whereis sed
sed: /usr/bin/sed /usr/share/man/man1/sed.1.gz /usr/share/man/man1p/sed.1p.gz
[veroll@MiWiFi-CR8809-srv ~]$ whereis awk
awk: /usr/bin/awk /usr/libexec/awk /usr/share/awk /usr/share/man/man1/awk.1.gz /usr/share/man/man1p/awk.1p.gz
```

## which
作用：搜索二进制命令  
使用格式：`which [命令]`  
举例：

```bash
[veroll@MiWiFi-CR8809-srv ~]$ which grep
alias grep='grep --color=auto'
        /usr/bin/grep
[veroll@MiWiFi-CR8809-srv ~]$ which sed
/usr/bin/sed
[veroll@MiWiFi-CR8809-srv ~]$ which awk
/usr/bin/awk
```

注意：which与whereis命令的不同为：whereis可以在查找二进制命令的同时，查找到帮助文档的位置；which命令在查找到二进制命令的同时，如果这个命令有别名，则还可以找到别名命令

## find
作用：在目录中搜索文件  
使用格式：`find 搜索路径 [选项] 搜索内容`  
选项：

```bash
-name：按照文件名搜索
-iname：按照文件名搜索，不区分大小写
-inum：按照inode号搜索

-size [+|-]大小[cwbkMG]：按照指定大小搜索文件。
						 +的意思是搜索比指定大小还要大的文件；
						 -的意思是搜索比指定大小还要小的文件。
						 b是默认单位，如果单位为b或者不写单位，按照512Byte搜索
						 c是按照字节搜索
						 w是按照双字节(中文)搜索
						 k是按照KB搜索
						 M是按照MB搜索
						 G是按照GB搜索

-atime [+|-]时间：按照文件访问时间搜索
-mtime [+|-]时间：按照文件数据修改时间搜索
-ctime [+|-]时间：按照文件状态修改时间搜索

-perm [-|+]权限模式：若不写-和+,表示查找文件权限刚好等于权限模式的文件；
					+的意思是查找文件权限包含权限模式的任意一个权限的文件
					-的意思是查找文件权限全部包含权限模式的文件

-uid 用户ID：查找所有者是指定用户ID的文件
-gid 组ID：查找所属组是指定组ID的文件
-user 用户名：查找所有者是指定用户名的文件
-group 组名：查找所属组是指定用户组名的文件
-nouser：查找没有所有者的文件

-type d：查找目录
-type f：查找普通文件
-type l：查找软链接文件

-a：逻辑与
-o：逻辑或
-not：逻辑非
```
举例：

```bash
# 在当前目录下搜索文件大小小于2KB，且文件类型是普通文件，且文件名称是d开头的共有四个字符的文件
[veroll@localhost ~]$ find . -size -2k -a -type f -a -name d???
./demo
```

## 三剑客之grep
作用：在文件中提取和匹配符合条件的字符串行。  
使用格式：`grep [选项] '搜索内容' 文件名`  
选项：
```bash
-v：显示未匹配到的行
-i：忽略大小写
-n：显示匹配的行号
-c：统计匹配的行数
-o：仅显示匹配到的字符串，而非整行
-E：使用 ERE，相当于 egrep(扩展正则)
```

举例：

```bash
[veroll@localhost ~]$ cat test
root root hello root
new
new
root
root
leo
kate
hogwart
string
leon

# 显示含有 root 的行，并显示行号
[veroll@localhost ~]$ grep -n 'root' test
1:root root hello root
4:root
5:root

# 查找以 s 开头的行
[veroll@localhost ~]$ grep -n '^s' test
9:string

# 查找以 n 结尾的行
[veroll@localhost ~]$ grep -n 'n$' test
10:leon

# 查找以s开头的行或以n结尾的行(注意：扩展正则中才能使用|符号)
[veroll@localhost ~]$ grep -nE '^s|n$' test
9:string
10:leon

# 查找o字符恰好出现两次的行(注意：扩展正则中才能使用{}符号)
[veroll@localhost ~]$ grep -nE 'o{2}' test
1:root root hello root
4:root
5:root

# 查询命令历史日志中more出现的次数
[veroll@MiWiFi-CR8809-srv ~]$ cat .bash_history | grep -o 'netstat' | wc -l
18

```


## 三剑客之sed

作用：用来将数据进行选取、替换、删除、新增。sed 是流编辑器，一次处理一行内容。  
使用格式：`sed [选项] '[动作]' 文件名`    
选项：

```bash
-e：允许对输入数据应用多条sed命令编辑
-f 脚本文件名：从sed脚本中读入sed操作
-i：用sed的修改结果直接修改读取数据的文件（危险操作）
-h：显示帮助
-n：一般sed命令会把所有数据都输出到屏幕，如果加入此选项，则只会把经过sed命令处理的行输出到屏幕
-r：在sed中支持扩展正则表达式
-V：显示版本信息
```
动作：
```bash
a \：追加， 在当前行后添加一行或多行，添加多行时，除最后一行外，每行末尾都需要用'\'代表数据未完结
c \：行替换，用c后面的字符串替换原数据行，替换多行时，除最后一行外，每行末尾都需要用'\'代表数据未完结
d ：删除，删除指定行
i \：插入，在当前行前插入一行或多行，插入多行时，除最后一行外，每行末尾都需要用'\'代表数据未完结
p：打印；sed -n '/root/p'：只打印包含 root 的行；/***/中的内容表示正则匹配语法脚本
s ：替换，sed -e '3s/old/new/g'：将第三行中的old 替换为 new，g 代表全局替换；'/'可以换成 '#'，'@'等
```


举例：

```bash
[veroll@localhost ~]$ cat student
ID      Name    PHP     Linux   MySQL   Average
1       Sally   82      95      86      87.66
2       Jerry   74      96      87      85.66
3       Tom     99      83      93      91.66

# 在第二行后插入数据
[veroll@localhost ~]$ sed '2a hello world' student
ID      Name    PHP     Linux   MySQL   Average
1       Sally   82      95      86      87.66
hello world
2       Jerry   74      96      87      85.66
3       Tom     99      83      93      91.66

# 在第二行前插入数据
[veroll@localhost ~]$ sed '2i hello world' student
ID      Name    PHP     Linux   MySQL   Average
hello world
1       Sally   82      95      86      87.66
2       Jerry   74      96      87      85.66
3       Tom     99      83      93      91.66

# 替换第二行的数据
[veroll@localhost ~]$ sed '2c hello world' student
ID      Name    PHP     Linux   MySQL   Average
hello world
2       Jerry   74      96      87      85.66
3       Tom     99      83      93      91.66

# 删除第二行到第四行的数据
[veroll@localhost ~]$ sed '2,4d' student
ID      Name    PHP     Linux   MySQL   Average

# 只打印出第二行的数据
[veroll@localhost ~]$ sed -n '2p' student
1       Sally   82      95      86      87.66

# 在第三行中，将字符串"Jerry"替换为"JJJJJ"
[veroll@localhost ~]$ sed '3s/Jerry/JJJJJ/g' student
ID      Name    PHP     Linux   MySQL   Average
1       Sally   82      95      86      87.66
2       JJJJJ   74      96      87      85.66
3       Tom     99      83      93      91.66
```

## 三剑客之awk

作用：把文件逐行读入，以空格为默认分割符，将每行切片，切开的部分再进行后续处理  

使用格式：`awk [选项] '/正则表达式/ 动作' [文件]`  
- pattern：正则表达式
- action：对匹配到的内容执行的命令（默认为输入每行内容）

常用选项及参数：  
- -F: 设置输入域分隔符。e.g. `-F :` 即设定冒号为域的分隔符。若不填写，默认空格为域分隔符。
- FILENAME：awk 浏览的文件名
- BEGIN：处理文本前要执行的操作
- END：处理文本后要执行的动作
- FS：设置输入域分割符，等价于命令行 -F 参数
- NF：浏览记录的域的个数（列数）
- NR：已读的记录数（行数）
- OFS：输出域分割符
- ORS：输入记录分割符
- RS：控制记录分割符
- $0：整条记录
- $n：表示当前行的第n个域(从1开始计数)

应用：  
有一个`passwd`文件如下所示，使用`awk`命令对其进行操作

```bash
[veroll@MiWiFi-CR8809-srv ~]$ cat passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin

```

搜索 passwd 文件中，包含 root 关键字的所有行，并将其整行打印

```bash
[veroll@MiWiFi-CR8809-srv ~]$ awk -F : '/root/{print $0}' passwd
root:x:0:0:root:/root:/bin/bash
```

搜索 passwd 文件中，包含 root 关键字的所有行，并打印第七个域

```bash
[veroll@MiWiFi-CR8809-srv ~]$ awk -F : '/root/{print $7}' passwd
/bin/bash
```

搜索 passwd 文件中，第三个域的值等于0的所有行，并将其整行打印
```bash
[veroll@MiWiFi-CR8809-srv ~]$ awk -F : '$3==0{print $0}' passwd
root:x:0:0:root:/root:/bin/bash
```

搜索passwd文件中，第七个域的值以login结尾的所有行，并将其整行打印(请使用正则表达式)
```bash
[veroll@MiWiFi-CR8809-srv ~]$ awk -F : '$7~/login$/{print $0}' passwd
bin:x:1:1:bin:/bin:/sbin/nologin

```

搜索passwd文件中，第五个域的值不是以b开头的所有行，并将其整行打印(请使用正则表达式)
```bash
[veroll@MiWiFi-CR8809-srv ~]$ awk -F : '$5!~/^b/{print $0}' passwd
root:x:0:0:root:/root:/bin/bash
```


打印 passwd 文件第2行的信息

```bash
[veroll@MiWiFi-CR8809-srv ~]$ awk -F : 'NR==2{print $0}' passwd
bin:x:1:1:bin:/bin:/sbin/nologin
```

使用 BEGIN 加入标题

```bash
[veroll@MiWiFi-CR8809-srv ~]$ awk -F : 'BEGIN {print "开始"} {print $1 $2}' passwd | head -2
开始
rootx
```

自定义行分割符

```bash
[veroll@MiWiFi-CR8809-srv ~]$ echo "111 222|333 444|555 666" | awk 'BEGIN{RS="|"}{print $0}'
111 222
333 444
555 666
```




# 压缩和解压缩命令
## zip
作用：压缩文件或目录  
使用格式：`zip [选项] 压缩包名 源文件或源目录`  
选项：  

```bash
-r：压缩目录
```
举例：

```bash
[veroll@localhost ~]$ zip test.zip test
  adding: test (deflated 24%)
[veroll@localhost ~]$ ls
demo  demo_hard  demo_soft  student  test  test.zip
```

## unzip
作用：解压.zip文件  
使用格式：`unzip [选项] 压缩包名`  
选项：  

```bash
-d：指定解压缩位置
```
举例：

```bash
[veroll@localhost ~]$ unzip -d ./output/ test.zip
Archive:  test.zip
  inflating: ./output/test
[veroll@localhost ~]$ ls ./output/
test
```

## tar
作用：打包与解打包  
使用格式：`tar [选项] [压缩包] [源文件或目录]`  
选项：  

```bash
-z：压缩和解压缩.tar.gz格式
-j：压缩和解压缩.tar.bz2格式
-c：打包
-t：测试，就是不解打包，只是查看包中有哪些文件
-x：解打包
-v：显示解打包文件过程
-f：指定压缩包的文件名。压缩包的扩展名是用来给管理员识别格式的，所以一定要正确指定扩展名

-C 目录：指定解打包位置
```

举例：

```bash
# 打包文件为.tar文件
[veroll@localhost ~]$ tar -cvf test.tar test
test

# 打包文件为.tar.gz文件
[veroll@localhost ~]$ tar -zcvf test.tar.gz test
test

# 打包文件为.tar.bz2文件
[veroll@localhost ~]$ tar -jcvf test.tar.bz2 test
test

# 只查看.tar文件包中有哪些文件，不解打包
[veroll@localhost ~]$ tar -tvf test.tar
-rw-rw-r-- veroll/veroll    68 2022-07-12 02:07 test

# 只查看.tar.gz文件包中有哪些文件，不解打包
[veroll@localhost ~]$ tar -ztvf test.tar.gz
-rw-rw-r-- veroll/veroll    68 2022-07-12 02:07 test

# 只查看.tar.bz2文件包中有哪些文件，不解打包
[veroll@localhost ~]$ tar -jtvf test.tar.bz2
-rw-rw-r-- veroll/veroll    68 2022-07-12 02:07 test

# 解打包.tar文件到指定位置
[veroll@localhost ~]$ tar -xvf test.tar -C ./tmp
test

# 解打包.tar.gz文件到指定位置
[veroll@localhost ~]$ tar -zxvf test.tar.gz -C ./tmp
test

# 解打包.tar.bz2文件到指定位置
[veroll@localhost ~]$ tar -jxvf test.tar.bz2 -C ./tmp/
test

# 将多个文件压缩到一个 tar.gz 文件
[veroll@localhost test_100]$ tar -zcvf test.tar.gz test{001..100}.txt
```

# 硬盘管理命令
## df
作用：统计空间大小，统计的剩余空间是准确的  
使用格式：`df [选项]`  
选项：  

```bash
-a：显示特殊文件系统，这些文件系统几乎都是保存在内存中的。如/proc，因为是挂载在内存中，所以占用量都是0
-h：单位不再只用KB，而是换算成习惯单位
-T：多出了文件系统类型一列
```
举例：

```bash
[veroll@localhost ~]$ df -ahT
Filesystem              Type        Size  Used Avail Use% Mounted on
sysfs                   sysfs          0     0     0    - /sys
proc                    proc           0     0     0    - /proc
devtmpfs                devtmpfs    1.9G     0  1.9G   0% /dev
securityfs              securityfs     0     0     0    - /sys/kernel/security
tmpfs                   tmpfs       1.9G     0  1.9G   0% /dev/shm
devpts                  devpts         0     0     0    - /dev/pts
tmpfs                   tmpfs       1.9G   12M  1.9G   1% /run
tmpfs                   tmpfs       1.9G     0  1.9G   0% /sys/fs/cgroup
cgroup                  cgroup         0     0     0    - /sys/fs/cgroup/systemd
pstore                  pstore         0     0     0    - /sys/fs/pstore
cgroup                  cgroup         0     0     0    - /sys/fs/cgroup/pids
cgroup                  cgroup         0     0     0    - /sys/fs/cgroup/devices
cgroup                  cgroup         0     0     0    - /sys/fs/cgroup/perf_event
cgroup                  cgroup         0     0     0    - /sys/fs/cgroup/freezer
cgroup                  cgroup         0     0     0    - /sys/fs/cgroup/cpu,cpuacct
cgroup                  cgroup         0     0     0    - /sys/fs/cgroup/cpuset
cgroup                  cgroup         0     0     0    - /sys/fs/cgroup/net_cls,net_pr
cgroup                  cgroup         0     0     0    - /sys/fs/cgroup/hugetlb
cgroup                  cgroup         0     0     0    - /sys/fs/cgroup/blkio
cgroup                  cgroup         0     0     0    - /sys/fs/cgroup/memory
configfs                configfs       0     0     0    - /sys/kernel/config
/dev/mapper/centos-root xfs          17G  1.5G   16G   9% /
selinuxfs               selinuxfs      0     0     0    - /sys/fs/selinux
systemd-1               autofs         0     0     0    - /proc/sys/fs/binfmt_misc
debugfs                 debugfs        0     0     0    - /sys/kernel/debug
hugetlbfs               hugetlbfs      0     0     0    - /dev/hugepages
mqueue                  mqueue         0     0     0    - /dev/mqueue
fusectl                 fusectl        0     0     0    - /sys/fs/fuse/connections
/dev/sda1               xfs        1014M  154M  861M  16% /boot
tmpfs                   tmpfs       378M     0  378M   0% /run/user/1000

```


## du
作用：统计文件大小，统计的文件大小是准确的  
使用格式：`du [选项] [目录或文件名]`  
选项：  

```bash
-a：显示每个子文件的磁盘占用量默认只统计子目录的磁盘占用量
-h：使用习惯单位显示磁盘占用量，如KB，MB或GB等
-s：统计总占用量，而不列出子目录和子文件的占用量
```
举例：

```bash
[veroll@localhost ~]$ du -h
4.0K    ./.cache/abrt
4.0K    ./.cache
0       ./.config/abrt
0       ./.config
8.0K    ./output/test_100
12K     ./output
8.0K    ./test_100
0       ./menu3
0       ./menu4
112K    .
```


# 关机和重启命令
## shutdown
作用：关机和重启  
使用格式：`shutdown [选项] 时间 [警告信息]`  
选项：  

```bash
-c：取消已经执行的shutdown命令
-h：关机
-r：重启
```

## reboot
作用：重启
使用格式：`reboot`

## halt
作用：关机
使用格式：`halt`

## poweroff
作用：关机
使用格式：`poweroff`

# 网络命令
## ifconfig
作用：查看IP地址的信息  
使用格式：`ifconfig`  
举例：  

```bash
[veroll@MiWiFi-CR8809-srv ~]$ ifconfig
ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
	   #标志									  最大传输单元
        inet 192.168.2.172  netmask 255.255.255.0  broadcast 192.168.2.255
        #IP地址			   子网掩码			      广播地址
        inet6 fe80::cfb1:5ae6:69d1:a014  prefixlen 64  scopeid 0x20<link>
        #IPv6地址
        ether 00:0c:29:8e:40:cc  txqueuelen 1000  (Ethernet)
        #MAC地址
        RX packets 27507  bytes 2441324 (2.3 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        #接受的数据包情况
        TX packets 27366  bytes 2726982 (2.6 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
        #发送的数据包情况

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
#本地回环网卡
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 5355  bytes 720490 (703.6 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 5355  bytes 720490 (703.6 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

## ping
作用：向主机发送ICMP请求  
使用格式：`ping [选项] IP`  
选项：  

```bash
-b：后面加入广播地址，用于对整个网段进行探测
-c 次数：用于指定ping的次数
-s 字节：指定探测包的大小
```

举例：
```bash
# 探测192.168.2.0/24网段中有多少可以通信的主机
[veroll@MiWiFi-CR8809-srv ~]$ ping -b -c 2 192.168.2.255
WARNING: pinging broadcast address
PING 192.168.2.255 (192.168.2.255) 56(84) bytes of data.
64 bytes from 192.168.2.41: icmp_seq=1 ttl=64 time=56.1 ms
64 bytes from 192.168.2.5: icmp_seq=1 ttl=64 time=74.1 ms (DUP!)
64 bytes from 192.168.2.5: icmp_seq=2 ttl=64 time=86.8 ms

--- 192.168.2.255 ping statistics ---
2 packets transmitted, 2 received, +1 duplicates, 0% packet loss, time 1011ms
rtt min/avg/max/mdev = 56.127/72.376/86.855/12.606 ms
```

## netstat
作用：查看网络状态  
使用格式：`netstat [选项]`  
选项：  

```bash
-a：列出所有网络状态，包括socket程序
-c 秒数：指定每隔几秒刷新一次网络状态
-n：使用IP地址和端口号显示，不使用域名与服务名
-p：显示PID和程序名
-t：显示使用TCP协议端口的连接状况
-u：显示使用UDP协议端口的连接状况
-l：仅显示监听状态的连接
-r：显示路由表
```

举例：

```bash
# 查看本机开启的端口。(因为使用了-l选项，所以只能看到监听状态的连接，而不能看到已经建立连接状态的连接)
[veroll@MiWiFi-CR8809-srv ~]$ netstat -tuln
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp        0      0 0.0.0.0:111             0.0.0.0:*               LISTEN
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN
tcp6       0      0 :::111                  :::*                    LISTEN
tcp6       0      0 :::22                   :::*                    LISTEN
tcp6       0      0 ::1:25                  :::*                    LISTEN
udp        0      0 0.0.0.0:68              0.0.0.0:*
udp        0      0 0.0.0.0:111             0.0.0.0:*
udp        0      0 127.0.0.1:323           0.0.0.0:*
udp        0      0 0.0.0.0:899             0.0.0.0:*
udp6       0      0 :::111                  :::*
udp6       0      0 ::1:323                 :::*
udp6       0      0 :::899                  :::*

上述参数解释：  
Proto：网络连接的协议，一般是TCP协议或UDP协议  
Recv-Q：表示接收到的数据，已经在本地的缓存中，但是还没有被进程取走
Send-Q：表示从本机发送，对方还没有收到的数据，依然在本地的缓冲中，一般是不具备ACK标志的数据包
Local Address：本机的IP地址和端口号
Foreign Address：远程主机的IP地址和端口号
State：状态。常用的状态有:
	LISTEN:监听状态，只有TCP协议需要监听，UDP协议不需要监听
	ESTABLISHED：已经建立连接的状态。如果使用-l选项，则看不到已经建立连接的状态
	SYN_SENT：SYN发起包，就是主动发起连接的数据包
	SYN_RECV：接收到主动连接的数据包
	FIN_WAIT1：正在中断的连接
	FIN_WAIT2：已经中断的连接，但是正在等待对方主机进行确认
	TIME_WAIT：连接已经中断，但是Socket依然在网络中等待结束
	CLOSED：Socket没有被使用
	在这些状态中，我们最常用的就是LISTEN和ESTABLISHED状态，前者代表正在监听，后者代表已经建立连接
```

```bash
# 查看本机有哪些程序开启了端口/查看哪个程序占用了哪个端口。(如果使用-p选项，则可以看到是哪个程序占用了端口，并且可以知道这个程序的PID)
# 注意：使用-p查看程序PID时，需要切换至管理员用户才能查看
[root@MiWiFi-CR8809-srv veroll]# netstat -tulnp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 0.0.0.0:111             0.0.0.0:*               LISTEN      735/rpcbind
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1151/sshd
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      1352/master
tcp6       0      0 :::111                  :::*                    LISTEN      735/rpcbind
tcp6       0      0 :::22                   :::*                    LISTEN      1151/sshd
tcp6       0      0 ::1:25                  :::*                    LISTEN      1352/master
udp        0      0 0.0.0.0:68              0.0.0.0:*                           958/dhclient
udp        0      0 0.0.0.0:111             0.0.0.0:*                           735/rpcbind
udp        0      0 127.0.0.1:323           0.0.0.0:*                           745/chronyd
udp        0      0 0.0.0.0:899             0.0.0.0:*                           735/rpcbind
udp6       0      0 :::111                  :::*                                735/rpcbind
udp6       0      0 ::1:323                 :::*                                745/chronyd
udp6       0      0 :::899                  :::*                                735/rpcbind
```

```bash
# 查看所有连接
# 使用选项-an可以查看所有连接，包括LISTEN、ESTABLISH、Socket程序连接等。从Active UNIX domain sockets开始，后续的内容就是Socket程序产生的连接，之前的内容就是网络服务产生的连接。
[veroll@MiWiFi-CR8809-srv ~]$ netstat -an
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp        0      0 0.0.0.0:111             0.0.0.0:*               LISTEN
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN
tcp        0      0 192.168.2.172:22        192.168.2.224:7748      ESTABLISHED
tcp        0     48 192.168.2.172:22        192.168.2.224:7727      ESTABLISHED
tcp6       0      0 :::111                  :::*                    LISTEN
tcp6       0      0 :::22                   :::*                    LISTEN
tcp6       0      0 ::1:25                  :::*                    LISTEN
udp        0      0 0.0.0.0:68              0.0.0.0:*
udp        0      0 0.0.0.0:111             0.0.0.0:*
udp        0      0 127.0.0.1:323           0.0.0.0:*
udp        0      0 0.0.0.0:899             0.0.0.0:*
udp6       0      0 :::111                  :::*
udp6       0      0 ::1:323                 :::*
udp6       0      0 :::899                  :::*
raw6       0      0 :::58                   :::*                    7
Active UNIX domain sockets (servers and established)
Proto RefCnt Flags       Type       State         I-Node   Path
unix  3      [ ]         DGRAM                    33       /run/systemd/notify
unix  2      [ ]         DGRAM                    35       /run/systemd/cgroups-agent
unix  2      [ ACC ]     STREAM     LISTENING     44       /run/systemd/journal/stdout
unix  5      [ ]         DGRAM                    47       /run/systemd/journal/socket
unix  19     [ ]         DGRAM                    49       /dev/log
......省略后续内容......
```

```bash
# 查看某个端口(例如22端口)是否被占用，若被占用，需查询到占用该端口的PID
[root@MiWiFi-CR8809-srv veroll]# netstat -anp | grep '.*:22'
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1151/sshd
tcp        0      0 192.168.2.172:22        192.168.2.224:7748      ESTABLISHED 6080/sshd: veroll [
tcp        0     48 192.168.2.172:22        192.168.2.224:7727      ESTABLISHED 6076/sshd: veroll [
tcp6       0      0 :::22                   :::*                    LISTEN      1151/sshd
```


# 进程操作命令
## ps
作用：静态显示系统中的进程  
使用格式：`ps [选项]`  
选项：  

```bash
a：显示一个终端的所有进程，除了会话引线
u：显示进程的归属用户及内存的使用情况
x：显示没有控制终端的进程
-A：显示所有进程
-l：长格式显示，显示更加详细的信息
-e：显示所有进程，和-A作用一致
-f: 显示一个更为完整的输出
```
举例：

```bash
# 查看系统中所有的进程，使用BSD操作系统格式
[veroll@MiWiFi-CR8809-srv ~]$ ps aux
USER        PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root          1  0.0  0.1 193692  6756 ?        Ss   Jul12   0:03 /usr/lib/systemd/systemd --switched-root --sy
root          2  0.0  0.0      0     0 ?        S    Jul12   0:00 [kthreadd]
root          4  0.0  0.0      0     0 ?        S<   Jul12   0:00 [kworker/0:0H]
root          6  0.0  0.0      0     0 ?        S    Jul12   0:00 [ksoftirqd/0]

上述参数解释：
USER：该进程是由哪个用户产生的
PID：进程的ID号
%CPU：该进程占用CPU资源的百分比，占用越高，进程越耗费资源
%MEM：该进程占用物理内存的百分比，占用越高，进程越耗费资源
VSZ：该进程占用虚拟内存的大小，单位KB
RSS：该进程占用实际物理内存的大小，单位KB
TTY：该进程是在哪个终端中运行的。其中tty1-tty7代表本地控制台终端(可以通过alt+F1-F7切换不同的终端)，tty1-tty6是本地的字符界面终端，tty7是图形终端。pts/0-255代表虚拟终端，一般是远程连接的终端。
STAT：进程状态。常见状态有：
	D：不可被唤醒的睡眠状态，通常用于I/O情况
	R：该进程正在运行
	S：该进程在睡眠状态，可被唤醒
	T：停止状态，可能是在后台暂停或进程在除错状态
	W：内存交互状态
	X：死掉的进程
	Z：僵尸进程。进程已经终止，但部分程序还在内存当中
	<：高优先级
	N：低优先级
	L：被锁入内存
	s：包含子进程
	l：多线程
	+：位于后台
START：该进程的启动时间
TIME：该进程占用CPU的运算时间，注意不是系统时间
COMMAND：产生此进程的命令名
```

```bash
# 查看系统中所有进程，使用Linux标准命令格式。
[veroll@MiWiFi-CR8809-srv ~]$ ps -le
F S   UID    PID   PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
4 S     0      1      0  0  80   0 - 48423 ep_pol ?        00:00:03 systemd
1 S     0      2      0  0  80   0 -     0 kthrea ?        00:00:00 kthreadd
1 S     0      4      2  0  60 -20 -     0 worker ?        00:00:00 kworker/0:0H
1 S     0      6      2  0  80   0 -     0 smpboo ?        00:00:00 ksoftirqd/0

上述参数解释：
F：进程标志，说明进程的权限，常见的标志有：
	1：进程可以复制，但不能执行
	4：进程使用超级用户权限
S：进程状态。具体的状态和ps aux命令中的STAT状态一致
UID：进程是哪个UID用户调用运行的
PID：进程的ID号
PPID：父进程的ID号
C：该进程的CPU使用率，单位是百分比
PRI：进程的优先级，数值越小该进程优先级越高，越快被CPU执行
NI：进程的优先级，也是数值越小越早被执行
ADDR：该进程在内存的位置
SZ：该进程占用多大内存
WCHAN：该进程是否运行。-代表正在运行
TTY：该进程由哪个终端产生
TIME：该进程占用CPU的运算时间，注意不是系统时间
CMD：产生此进程的命令名
```

```bash
# 列出所有进程，并显示环境变量，而且显示全格式。推荐使用
[root@localhost ~]# ps -ef
UID         PID   PPID  C STIME TTY          TIME CMD
root          1      0  0 09:40 ?        00:00:04 /usr/lib/systemd/systemd --switched-root --system --deserialize 22
root          2      0  0 09:40 ?        00:00:00 [kthreadd]
root          4      2  0 09:40 ?        00:00:00 [kworker/0:0H]
root          6      2  0 09:40 ?        00:00:00 [ksoftirqd/0]

上述参数解释：
UID: 用户的ID ，但输出的是用户名
PID:进程的ID
PPID: 父进程的ID
C: 进程占用CPU的百分比
STIME: 进程启用到现在的时间
TTY: 该进程在哪个终端上运行，若与终端无关，则显示？，若为pts/0等，则表示由网络连接主机进程
TIME: 该进程实际使用CPU运行的时间
CMD: 命令的名称和参数
```


```bash
# 查看所有的ssh进程
[root@localhost ~]# ps -ef | grep 'ssh'
root       1154      1  0 09:41 ?        00:00:00 /usr/sbin/sshd -D
root       4859   1154  0 11:44 ?        00:00:00 sshd: veroll [priv]
root       4870   1154  0 11:44 ?        00:00:00 sshd: veroll [priv]
veroll     4872   4859  0 11:44 ?        00:00:00 sshd: veroll@pts/0
veroll     4922   4870  0 11:45 ?        00:00:00 sshd: veroll@notty
veroll     4923   4922  0 11:45 ?        00:00:00 /usr/libexec/openssh/sftp-server
root       6581   1154  0 12:15 ?        00:00:00 sshd: veroll [priv]
root       6592   1154  0 12:15 ?        00:00:00 sshd: veroll [priv]
veroll     6594   6581  0 12:15 ?        00:00:00 sshd: veroll@pts/1
veroll     6639   6592  0 12:15 ?        00:00:00 sshd: veroll@notty
veroll     6640   6639  0 12:15 ?        00:00:00 /usr/libexec/openssh/sftp-server
root       7025   6255  0 12:22 pts/0    00:00:00 grep --color=auto ssh


```

## top
作用：动态显示系统的资源使用情况以及进程信息  
使用格式：`top [选项]`  
选项：  

```bash
-d 秒数：指定top命令每隔几秒更新。默认是3秒
-b：使用批处理模式输出。一般和-n选项合用，用于把top命令重定向到文件中
-n 次数：指定top命令执行的次数。一般和-b选项合用
-p：指定PID。只查看某个PID的进程
-s：使top在安全模式运行，避免在交互模式中出现错误
-u 用户名：只监听某个用户的进程
```

交互模式：

```bash
？或h：显示交互模式的帮助
P：以CPU使用率排列，默认就是此项
M：以内存的使用率排序
N：以PID排序
T：按照CPU的累积运算时间排序，也就是用TIME+项排序
k：按照PID号，给予某个进程一个信号。一般用于终止某个进程，信号9是强制终止的信号
r：按照PID号，给某个进程重设优先级值
q：退出top
```

举例：

```bash
[veroll@MiWiFi-CR8809-srv ~]$ top
top - 03:59:23 up 14:48,  2 users,  load average: 0.00, 0.01, 0.05
Tasks: 150 total,   1 running, 149 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem :  3861292 total,  3330904 free,   343056 used,   187332 buff/cache
KiB Swap:  2097148 total,  2097148 free,        0 used.  3298472 avail Mem

   PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
     9 root      20   0       0      0      0 S   0.3  0.0   0:09.07 rcu_sched
  6627 root      20   0       0      0      0 S   0.3  0.0   0:00.01 kworker/3:2
  6629 veroll    20   0  162108   2336   1572 R   0.3  0.1   0:00.05 top
     1 root      20   0  193692   6756   4164 S   0.0  0.2   0:03.80 systemd

上述输出可分为两部分：
第一部分是前五行，显示的是整个系统的资源使用情况；
第二部分从第六行开始，显示的是系统中进程的信息。

第一部分：
	第一行：任务队列信息：
		03:59:23：系统当前时间
		up 14:48：系统的运行时间，本机已经运行了14小时48分钟
		2 users：当前登录了两个用户
		load average: 0.00, 0.01, 0.05：系统在之前1分钟，5分钟，15分钟的平均负载。(如果CPU是单核，则这个数超过1，就是高负载；如果CPU是四核，则这个数超过4，就是高负载。一般认为不应该超过服务器CPU的核数)
	第二行：进程信息：
		Tasks: 150 total：系统中的进程总数
		1 running：正在运行的进程数
		149 sleeping：睡眠的进程数
		0 stopped：正在停止的进程
		0 zombie：僵尸进程。如果不是0，需要手工检查僵尸进程
	第三行：CPU信息：
		%Cpu(s):  0.0 us：用户模式占用的CPU百分比
		0.0 sy：系统模式占用的CPU百分比
		0.0 ni：改变过优先级的用户进程占用的CPU百分比
		100.0 id：空闲CPU的CPU百分比
		0.0 wa：等待输入、输出的进程的占用CPU百分比
		0.0 hi：硬中断请求服务占用的CPU百分比
		0.0 si：软中断请求服务占用的CPU百分比
		0.0 st：虚拟时间百分比。就是当有虚拟机时，虚拟CPU等待实际CPU的时间百分比
	第四行：物理内存信息：
		KiB Mem :  3861292 total：物理内存的总量，单位KB
		3330904 free：空闲的物理内存数量
		343056 used：已经使用的物理内存数量
		187332 buff/cache：作为缓冲的内存数量
	第五行：交换分区信息：
		KiB Swap:  2097148 total：交换分区(虚拟内存)的总大小
		2097148 free：空闲交换分区的大小
		0 used：已经使用的交换分区的大小
		3298472 avail Mem：作为缓冲的交换分区的大小

第二部分：
	PID：进程PID
	USER：该进程所属的用户
	PR：优先级，数值越小优先级越高
	NI：优先级，数值越小优先级越高
	VIRT：该进程使用的虚拟内存的大小，单位KB
	RES：该进程使用的物理内存的大小，单位KB
	SHR：共享内存的大小，单位KB
	S：进程状态
	%CPU：该进程占用CPU的百分比
	%MEM：该进程占用内存的百分比
	TIME+：该进程总共占用的CPU时间
	COMMAND：进程的命令名
```

```bash
# 只动态查看PID为727的进程
[veroll@MiWiFi-CR8809-srv ~]$ top -p 727
top - 04:15:53 up 15:05,  2 users,  load average: 0.00, 0.01, 0.05
Tasks:   1 total,   0 running,   1 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem :  3861292 total,  3331292 free,   342620 used,   187380 buff/cache
KiB Swap:  2097148 total,  2097148 free,        0 used.  3298884 avail Mem

   PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
   727 root      20   0  273004   4816   3672 S   0.3  0.1   1:48.92 vmtoolsd
```

```bash
# 查看系统中所有的进程
# 让top命令只执行一次，把结果保存到top.log文件中，这样就可以查看所有进程了
[veroll@MiWiFi-CR8809-srv ~]$ top -b -n 1 > top.log
[veroll@MiWiFi-CR8809-srv ~]$ cat top.log
top - 04:20:00 up 15:09,  2 users,  load average: 0.00, 0.01, 0.05
Tasks: 150 total,   1 running, 149 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem :  3861292 total,  3331468 free,   342444 used,   187380 buff/cache
KiB Swap:  2097148 total,  2097148 free,        0 used.  3299060 avail Mem

   PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
     1 root      20   0  193692   6756   4164 S   0.0  0.2   0:03.84 systemd
     2 root      20   0       0      0      0 S   0.0  0.0   0:00.08 kthreadd
     4 root       0 -20       0      0      0 S   0.0  0.0   0:00.00 kworker/0:0H
```

## kill
作用：向进程发送信号  
使用格式：`kill [信号] PID`  
信号：  

```bash
1 SIGHUP 该信号让进程立即关闭，然后重新读取配置文件之后重启
2 SIGINT 程序终止信号，用于终止前台进程。相当于输入ctrl+c快捷键
8 SIGFPE 在发生致命的算术运算错误时发出
9 SIGKILL 用来立即结束程序的运行，本信号不能被阻塞、处理和忽略。一般用于强制终止进程
14 SIGALRM 时钟定时信号，计算的是实际的时间或时钟时间，alarm函数使用该信号
15 SIGTERM 正常结束进程的信号，kill命令的默认信号。有时如果进程已经发生问题，这个信号是无法正常终止进程的，我们才会尝试SIGKILL信号，也就是信号9
18 SIGCONT 该信号可以让暂停的进程恢复执行，本信号不能被阻断
19 SIGSTOP 该信号可以暂停前台进程，相当于输入ctrl+z快捷键，本信号不能被阻断
```

举例：

```bash
# 暂停一个进程
# 首先通过进程名获取PID
[root@MiWiFi-CR8809-srv veroll]# ps aux | grep 'vim' | grep -v 'grep'
veroll     1877  0.0  0.1 149300  5032 pts/0    S+   05:38   0:00 vim test.kkk
# 暂停进程
[root@MiWiFi-CR8809-srv veroll]# kill -19 1877
# 查看进程状态，由S+变为T
[root@MiWiFi-CR8809-srv veroll]# ps aux | grep 'vim' | grep -v 'grep'
veroll     1877  0.0  0.1 149300  5032 pts/0    T    05:38   0:00 vim test.kkk


# 杀掉一个进程
# 获取进程PID
[root@localhost ~]# ps -ef | grep 'vim' | grep -v 'grep'
veroll     6665   6595  0 12:15 pts/1    00:00:00 vim kkkk
# 杀掉进程
[root@localhost ~]# kill -9 6665
# 查看进程状态，进程被杀掉
[root@localhost ~]# ps -ef | grep 'vim' | grep -v 'grep'
[root@localhost ~]#
```

# 内存操作命令
## free
作用：查看内存使用状态  
使用格式：`free [选项]`  
选项：  

```bash
-b：以字节为单位显示
-k：以KB为单位显示，默认就是以KB为单位显示
-m：以MB为单位显示
-g：以GB为单位显示
```

举例：

```bash
[root@MiWiFi-CR8809-srv veroll]# free
              total        used        free      shared  buff/cache   available
Mem:        3861292      317412     3385856       11992      158024     3338748
Swap:       2097148           0     2097148

上述参数说明：
total：总内存数
used：已经使用的内存数
free：空闲的内存数
shared：多个进程共享的内存数
```


# 其他
## Linux相比windows优势
1. 稳定性高  
业界公认：Linux服务器比Windows服务器稳定性高；多年经验了解，Linux稳定性虽然比不上在IBM小型机上运行AIX，但是比Windows服务器确实高很多。

2. 初期投入成本低  
硬件投入成本低：由于Linux操作系统相比于Windows先天优越性，相同硬件条件下，Linux服务器能承受负荷普遍比Windows高20%以上。
软件投入成本更低：Windows服务器端产品价格普遍比较高，加上客户端用户授权费用，是一笔不小开支。Linux由于开源操作系统，甚至可以不花费一分钱。

3. 低维护成本  
对于入门级系统管理人员，由于Windows入门容易，Windows维护成本比Linux高；对于专业级系统管理人员而言，Linux维护成本反而比Windows维护成本低很多

4. 病毒造成破坏低  
由于Windows先天不足以及Windows在客户端高市场占有率，目前病毒绝大部分是针对Windows操作系统；Linux是开放源代码操作系统，即使出现有针对性病毒，开源社团也会从底层进行修正，从根本上杜绝类似病毒后续造成的危害

5. 无需频繁升级  
微软为保持企业持续获利，会持续发布行新产品；企业为保持服务器端稳定，只能不停的跟着微软步伐升级，耗时耗力耗财。而Linux在方面情况则好许多。

6. 保密性  
Windows由于是商业产品，源代码封闭，我们无法知道微软在里面做了什么手脚。而Linux由于是源代码开放操作系统，不存在这个问题。

## 什么是inode节点
Linux操作系统引进了一个非常重要的概念inode，中文名为索引结点，引进索引接点是为了在物理内存上找到文件块，所以inode中包含文件的相关基本信息，比如文件位置、文件创建者、创建日期、文件大小等待，输入`stat`指令可以查看某个文件的inode信息。

```bash
$ stat demo
  File: demo
  Size: 13              Blocks: 1          IO Block: 65536  regular file
Device: 161977h/1448311d        Inode: 3096224743896930  Links: 1
Access: (0644/-rw-r--r--)  Uid: (197610/292351614)   Gid: (197610/ UNKNOWN)
Access: 2022-07-11 14:28:45.869636400 +0800
Modify: 2022-07-11 14:28:42.584114700 +0800
Change: 2022-07-11 14:28:42.584114700 +0800
 Birth: 2022-07-11 14:28:42.580112000 +0800
```

也可以输入`ls -i`指令查看文件inode。

```bash
$ ls -i
3096224743896930 demo
```


## 什么是硬链接和软链接？
### 硬链接： 
 Linux 下的文件是通过索引节点(inode)来识别文件，硬链接可以认为是一个指针，指向文件索引节点的指针，系统并不为它重新分配 inode 。每添加一个一个硬链接，文件的链接数就加 1 。
 
 硬链接特征为：
 - 源文件和硬链接文件拥有相同的inode
 - 修改任意一个文件，另一个都改变
 - 删除任意一个文件，另一个都能使用
 - 硬链接不能链接目录
 - 硬链接不能跨分区
 - 硬链接表记不清，很难确认硬链接文件位置，不建议使用硬链接
### 软链接：
软链接克服了硬链接的不足，没有任何文件系统的限制，任何用户可以创建指向目录的符号链接。因而现在更为广泛使用，它具有更大的灵活性，甚至可以跨越不同机器、不同网络对文件进行链接。 

软连接特征为：
- 源文件和软链接文件拥有不同的inode
- 修改任意一个文件，另一个都改变
- 删除软链接，源文件不受影响；删除源文件，软链接不能使用
- 软链接没有实际数据，只保存源文件的inode，不论源文件多大，软链接大小不变
- 软链接的权限是最大权限lrwxrwxrwx，但由于没有实际数据，最终访问时需要参考源文件的权限
- 软链接可以链接目录
- 软链接可以跨分区
- 软链接特征明显，建议使用软链接


## 什么是交换空间？
交换空间是Linux使用的一定空间，用于临时保存一些并发运行的程序。当RAM没有足够的内存来容纳正在执行的所有程序时，就会发生这种情况。

## 有哪些常见的配置文件
- /etc/profile：系统环境变量配置文件
- /etc/sysconfig/iptables：防火墙配置文件
- /etc/hosts/：主机文件
- /etc/rc.local：开机就执行命令的文件
- /root/.bashrc_profile：当前用户环境变量配置文件

## 命令的基本格式

```bash
[root@localhost ~]#
```
- root：显示的是当前的登录用户，目前是root用户
- @：分隔符
- localhost：当前系统主机名简写(完整主机名为localhost.localdomain)
- ~：代表用户当前所在目录，`~`代表家目录
- #：命令提示符。超级用户为`#`，普通用户为`$`。如：

```bash
[veroll@localhost ~]$
```

## 如何查看命令的帮助
使用`man`命令。  
作用：获取命令的帮助手册  
使用格式：`man [选项] 命令`  
选项：

```bash
-f：查看命令拥有哪个级别的帮助
-k：查看命令相关的所有帮助
级别数字：查看某级别的帮助
```

举例：

```bash
[veroll@localhost ~]$ man -f printf
printf (1)           - format and print data
printf (1p)          - write formatted output
printf (3)           - formatted output conversion
printf (3p)          - print formatted output
```
man命令的帮助级别为
|级别|作用
|:--:|:--:|
|1|普通用户可以执行的系统命令和可执行文件的帮助|
|2|内核可以调用的函数和工具的帮助|
|3|C语言函数的帮助|
|4|设备和特殊文件的帮助|
|5|配置文件的帮助
|6|游戏的帮助(个人版的Linux中是有游戏的)
|7|杂项的帮助|
|8|超级用户可以执行的系统命令的帮助
|9|内核的帮助

## 文件的用户权限了解吗？
使用`ls -l`命令，第一列就是文件的权限。

```bash
[veroll@localhost ~]$ ls -l
total 8
-rw-rw-r--. 2 veroll veroll 28 Jul 11 04:59 demo
```
一共有11位。

第一位代表文件类型。常见文件类型有：  
- `-`：普通文件
- `b`：块设备文件。这是一种特殊设备文件，存储设备都是这种文件，如分区文件`/dev/sda1`就是这种文件
- `c`：字符设备文件。这是一种特殊设备文件，输入设备一般都是这种文件，如鼠标、键盘等
- `d`：目录文件
- `l`：软链接文件
- `p`：管道符文件
- `s`：套接字文件。这是一种特殊设备文件，一些服务支持Socket访问，就会产生这样的文件

第二到四位代表文件所有者的权限
- `-`：没有对应权限
- `r`：读取权限
- `w`：写权限
- `x`：执行权限

第五到七位代表文件所属组的权限  
第八到十位代表其他人的权限  
第十一位的`.`代表该文件存在“SELinux的安全标签”  

## 能说出几个Linux系统中常用的快捷键吗？
快捷键 | 作用
--|--
Tab|补全命令名或文件或目录名
ctrl+A|把光标移动到命令行开头
ctrl+E|把光标移动到命令行结尾
ctrl+C|强制终止当前命令
ctrl+L|清屏，相当于clear命令
ctrl+U|删除或剪切光标之前的命令
ctrl+K|删除或剪切光标之后的命令
ctrl+Y|粘贴ctrl+U剪切的内容
ctrl+R|在历史命令中搜索
ctrl+D|退出当前终端
ctrl+Z|暂停，并放入后台
ctrl+S|暂停屏幕输出
ctrl+Q|恢复屏幕输出

## 读、写、执行对文件和目录的作用相同吗？若不同，体现在哪里？
读、写、执行对文件和目录的作用不同。
### 权限对文件的作用
- 读：代表可以读取文件中的数据。代表可以对文件执行`cat`, `more`, `less`, `head`, `tail`等文件查看命令。
- 写：代表可以修改文件中的数据。代表可以对文件执行`vim`, `echo`等修改文件数据的命令。(注意：**对文件有写权限，是不能删除文件本身的，只能修改文件中的数据，如果想要删除文件，则需要对文件的上级目录拥有写权限**)
- 执行：代表文件拥有执行权限，可以运行。在Linux中，只要文件拥有执行权限，这个文件就是执行文件了。只是这个文件到底能不能正确执行，不仅需要文件具备执行权限，还要看文件中的代码是否为正确的代码。对文件来说，执行权限是最高权限。

文件常用权限：
- 664：这是文件的基本权限，代表文件所有者和所属组拥有读、写权限，而其他人拥有只读权限。
- 775：代表所有者和所属组拥有读、写、执行权限，而其他人拥有读和执行权限。
- 777：这是文件的最大权限。在实际的生产服务器中，要尽力避免给文件赋予这样的权限，这会造成一定的安全隐患。

### 权限对目录的作用
- 读：代表可以查看目录下的内容，也就是可以查看目录下有哪些子文件和子目录。代表可以在目录下执行`ls`命令，查看目录内容。
- 写：代表可以修改目录下的数据，也就是可以在目录中新建、删除、复制、剪切子文件或子目录。代表可以在目录下执行`touch`, `rm`, `cp`, `mv`命令。对目录来说，写权限是最高权限。
- 执行：目录是不能运行的，对目录来说，拥有执行权限，代表可以进入目录。代表可以对目录执行`cd`命令。

目录常用权限：
- 775：这是目录的基本权限，代表所有者和所属组拥有目录的完全权限，而其他人拥有基本的目录浏览和进入权限。
- 777：这是目录的最大权限。在实际的生产服务器中，要尽力避免赋予这样的权限，这会造成一定的安全隐患。

## 你知道Linux命令中单引号和双引号的区别吗？
- 单引号可保证其内部所有字符不被shell解析。如单引号与grep命令配合使用，则单引号内部字符将直接发送给grep命令进行正则表达式的解析。  
- 双引号保护特殊元字符和通配符不被shell解析，但是允许变量和命令的解析，以及转义符的解析。

## 你知道哪些常用的正则表达式？
Linux中用来在文件中搜索字符串的命令，如grep, sed, awk等命令支持正则表达式与扩展正则表达式。

- grep使用扩展正则表达式需加上-E选项
- sed使用扩展正则表达式需要加上-r选项
### 基础正则表达式
符号|	解释|	示例|	
--|--|--|
*| 匹配0次或多次 |	b.*t	|  可以匹配bt / bat / bdaf44fdsat / b#$%t等
.	|匹配任意字符|	b.t	|可以匹配bat / but / b#t / b1t等
^	|匹配字符串的开始|	^The|	可以匹配The开头的字符串
$	|匹配字符串的结束|	.exe$|	可以匹配.exe结尾的字符串
[]|	匹配来自字符集的任意单一字符|	[aeiou]|	可以匹配任一元音字母字符

### 扩展正则表达式
符号	|解释|	示例|	说明
--|--|--|--
+|匹配1次或多次|	b.+t	| 可以匹配bat / bdaf23dsat / b4@#32t 等
?|	匹配0次或1次|	b.?t	| 可以匹配bt / bat等
{N}|	匹配N次|	H.{3}o	| 可以匹配Hello / H#@$o / H234o等
{M,}|	匹配至少M次|	H.{3,}o	|可以匹配Hello / Haaaaaaao / H234#@o等
{M,N}|	匹配至少M次至多N次|	Ha{3,5}o	|可以匹配Haaao / Haaaao / Haaaaao等
\| |	分支|	foo\|bar|	可以匹配foo或者bar
(exp)|	匹配exp并捕获到自动命名的组中|(dog)+|匹配dog、dogdog、dogdogdog等

## 你知道哪些搜索命令，它们有什么区别？
`find`和`grep`。
- `find`命令用于在系统中搜索符合条件的**文件名**，如果需要模糊查询，可以使用通配符进行匹配，通配符是完全匹配。也可以加上`-regex`选项，使用正则表达式匹配。
- `grep`命令用于在文件中搜索符合条件的**字符串**，如果需要模糊查询，可以使用正则表达式进行匹配，正则表达式是包含匹配

## Linux系统中，你知道哪些可以创建文件的命令？
- 重定向符号: >
```bash
[veroll@localhost demo_creat]$ > testFile1
[veroll@localhost demo_creat]$ ls
testFile1
```
- touch
```bash
[veroll@localhost demo_creat]$ touch testFile2
[veroll@localhost demo_creat]$ ls
testFile1  testFile2
```
- echo
```bash
[veroll@localhost demo_creat]$ echo 'Hello World!' > testFile3
[veroll@localhost demo_creat]$ ls
testFile1  testFile2  testFile3
[veroll@localhost demo_creat]$ cat testFile3
Hello World!
```
- printf
```bash
[veroll@localhost demo_creat]$ printf 'Hello World!' > testFile4
[veroll@localhost demo_creat]$ ls
testFile1  testFile2  testFile3  testFile4
[veroll@localhost demo_creat]$ cat testFile4
Hello World![veroll@localhost demo_creat]$
```
- vi
```bash
[veroll@localhost demo_creat]$ vi testFile5
[veroll@localhost demo_creat]$ ls
testFile1  testFile2  testFile3  testFile4  testFile5
```
- cat
```bash
[veroll@localhost demo_creat]$ cat > testFile6
Hello
World
[veroll@localhost demo_creat]$ ls
testFile1  testFile2  testFile3  testFile4  testFile5  testFile6
[veroll@localhost demo_creat]$ cat testFile6
Hello
World


## 如何在当前用户家目录中查找haha.txt文件？
```bash
[veroll@localhost /]$ find ~/haha.txt
/home/veroll/haha.txt
```
## 如何动态查看/var/log/messages这个日志文件?
```bash
[root@localhost ~]# tail -f /var/log/messages
Jul 19 12:09:56 localhost dbus[724]: [system] Activating via systemd: service name='net.reactivated.Fprint' unit='fprintd.service'
Jul 19 12:09:56 localhost systemd: Starting Fingerprint Authentication Daemon...
Jul 19 12:09:56 localhost dbus[724]: [system] Successfully activated service 'net.reactivated.Fprint'
Jul 19 12:09:56 localhost systemd: Started Fingerprint Authentication Daemon.
Jul 19 12:09:58 localhost su: (to root) veroll on pts/0
Jul 19 12:09:58 localhost dbus[724]: [system] Activating service name='org.freedesktop.problems' (using servicehelper)
Jul 19 12:09:58 localhost dbus[724]: [system] Successfully activated service 'org.freedesktop.problems'
Jul 19 12:10:01 localhost systemd: Created slice User Slice of root.
Jul 19 12:10:01 localhost systemd: Started Session 25 of user root.
Jul 19 12:10:01 localhost systemd: Removed slice User Slice of root.

# Ctrl+C退出动态查看
```

## 如何查询出vim这个进程，并杀掉这个进程？
```bash
# 获取进程PID
[root@localhost ~]# ps -ef | grep 'vim' | grep -v 'grep'
veroll     6665   6595  0 12:15 pts/1    00:00:00 vim kkkk
# 杀掉进程
[root@localhost ~]# kill -9 6665
# 查看进程状态，进程被杀掉
[root@localhost ~]# ps -ef | grep 'vim' | grep -v 'grep'
[root@localhost ~]#
```

## 如何查看系统硬盘空间？
```bash
[veroll@MiWiFi-CR8809-srv ~]$ df -h
Filesystem               Size  Used Avail Use% Mounted on
devtmpfs                 1.9G     0  1.9G   0% /dev
tmpfs                    1.9G     0  1.9G   0% /dev/shm
tmpfs                    1.9G   12M  1.9G   1% /run
tmpfs                    1.9G     0  1.9G   0% /sys/fs/cgroup
/dev/mapper/centos-root   17G  1.5G   16G   9% /
/dev/sda1               1014M  154M  861M  16% /boot
tmpfs                    378M     0  378M   0% /run/user/1000
```

## 如何查看当前监听(listen)了哪些端口？
```bash
[root@MiWiFi-CR8809-srv veroll]# netstat -lnp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 0.0.0.0:111             0.0.0.0:*               LISTEN      725/rpcbind
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1154/sshd
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      1377/master
tcp6       0      0 :::111                  :::*                    LISTEN      725/rpcbind
tcp6       0      0 :::22                   :::*                    LISTEN      1154/sshd
tcp6       0      0 ::1:25                  :::*                    LISTEN      1377/master
udp        0      0 0.0.0.0:68              0.0.0.0:*                           2283/dhclient
udp        0      0 0.0.0.0:111             0.0.0.0:*                           725/rpcbind
udp        0      0 127.0.0.1:323           0.0.0.0:*                           759/chronyd
udp        0      0 0.0.0.0:899             0.0.0.0:*                           725/rpcbind
udp6       0      0 :::111                  :::*                                725/rpcbind
udp6       0      0 ::1:323                 :::*                                759/chronyd
udp6       0      0 :::899                  :::*                                725/rpcbind
raw6       0      0 :::58                   :::*                    7           828/NetworkManager
```

## 如何查看某个端口是否被占用？并且查询到占用该端口的PID，比如查询22端口。
```bash
[root@MiWiFi-CR8809-srv veroll]# netstat -anp | grep '.*:22'
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1154/sshd
tcp        0     48 192.168.2.172:22        192.168.2.224:9838      ESTABLISHED 8312/sshd: veroll [
tcp        0      0 192.168.197.207:22      192.168.197.57:2885     ESTABLISHED 6592/sshd: veroll [
tcp        0      0 192.168.197.207:22      192.168.197.57:2855     ESTABLISHED 6581/sshd: veroll [
tcp        0      0 192.168.197.207:22      192.168.197.57:10172    ESTABLISHED 4859/sshd: veroll [
tcp        0      0 192.168.197.207:22      192.168.197.57:10200    ESTABLISHED 4870/sshd: veroll [
tcp        0      0 192.168.2.172:22        192.168.2.224:9847      ESTABLISHED 8318/sshd: veroll [
tcp6       0      0 :::22                   :::*                    LISTEN      1154/sshd
```

或

```bash
[root@MiWiFi-CR8809-srv veroll]# netstat -anp | awk '$4~/.*:22/ {print $0}'
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1154/sshd
tcp        0     48 192.168.2.172:22        192.168.2.224:9838      ESTABLISHED 8312/sshd: veroll [
tcp        0      0 192.168.197.207:22      192.168.197.57:2885     ESTABLISHED 6592/sshd: veroll [
tcp        0      0 192.168.197.207:22      192.168.197.57:2855     ESTABLISHED 6581/sshd: veroll [
tcp        0      0 192.168.197.207:22      192.168.197.57:10172    ESTABLISHED 4859/sshd: veroll [
tcp        0      0 192.168.197.207:22      192.168.197.57:10200    ESTABLISHED 4870/sshd: veroll [
tcp        0      0 192.168.2.172:22        192.168.2.224:9847      ESTABLISHED 8318/sshd: veroll [
tcp6       0      0 :::22                   :::*                    LISTEN      1154/sshd

```