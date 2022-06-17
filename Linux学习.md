#       Linux学习

## Linux常用命令

### **一、命令基本格式**

[root@localhost  ~]#

用户名：root

local host：计算机主机名

~ ：当前所在目录（初始目录）

#：超级用户的提示符

$: 普通用户的提示符



命令  [选项] [参数]

注意：个别命令使用不遵循此格式，当有多个选项时，可以写在一起简化选项与完整选项。-a == --all 



命令：

pwd：显示当前所在位置

ls: 查询目录中内容

​	ls [选项] [文件或目录]

​	选项：

​		-a 显示所有文件，包括隐藏文件

​		-l  显示详细信息

​		-d 查看目录属性

​		-h 人性化显示文件大小

​		-i 显示inoode



权限类型 (Linux中考权限类型区分文件)

**-rw-r--r--**（十位组成）

![image-20191119140846589](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191119140846589.png)

1. 第一位

	- **-**:文件类型
	- **d**: 目录类型 
	- **|** :软链接类型（快捷方式）

2. 后面的每三位为一组，表示不同身份

   第一组：u代表所有者

   第二组：g代表所属组

   第三组：o代表其他人

   **r**:读  **w**:写  **x**:执行  

3.  **1** : 应用计数



### **二、** **文件处理命令**

1. ​	**目录处理命令（类比于windows中文件夹）**

   **建立目录**：**mkdir**  目录名   => 创建单个目录

   mkdir -p   [目录名]   递归创建   => 创建一系列的目录，就是目录下的目录

   

   **切换所在目录**：**cd**  [目录名]

   cd ~ : 进入当前用户的家目录 

   cd ： 进入当前用户的家目录 

   cd - :进入上次所在目录

   cd .. ：进入上一级目录

   cd . :  进入当前目录

   

   **查看当前所在位置**：**pwd**

​		

​		**删除空目录**：**rmdir** =>只能删除空的目录

​		**删除文件或目录**： **rm  -rf** [文件或目录]  => 强制删除文件或目录下所有的文件

​		

​		**复制命令：cp**

​			cp [选项] [原文件或目录] [目标目录]

​		选项：

​			-r  复制目录

​			-p 连带文件属性复制

​			-d 若源文件是链接文件，则复制链接属性

​			-a 相当于  -pdr

​			

​		**剪切或改名命令： mv** 

​			mv [原文件或目录] [目标目录]

2. **文件处理命令**

   **常用目录的作用**

![image-20191119153858913](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191119153858913.png)

1. ​	 根目录：根目录下的bin和sbin，usr目录下的bin和sbin，这四个目录都是用来保存系统命令的。
2. /bin : 命令保存目录（普通用户就可以读取的命令）
3. /boot ： 启动目录，启动相关文件
4. /dev : 设备文件保存目录
5. /etc：配置文件保存目录
6. /home： 普通用户的家目录
7. /lib ： 系统库保存目录
8. /mnt： 系统挂载目录
9. /media： 挂载目录
10. /root: 超级用户的家目录
11. /tmp：临时目录
12. /sbin： 命令保存目录（超级用户才能使用的目录）
13. /proc： 直接写入内存的
14. /sys
15. /usr：系统软件资源目录
    1. /usr/bin/ ：系统命令（普通用户）
    2. /usr/sbin/ :系统命令（超级用户）
16. /var：系统相关文档内容

3.**链接命令**

链接命令: ln

软链接： -s

​	特征：

1. 类似Windows快捷方式

2. 软链接拥有子级的I节点和Block块，但是数据块中只保存原文件的文件名和I节点号，并没有实际的文件数据

3. Irwxrwxrwx   I 软链接

   ​	软链接文件权限都为rwxrwxrwx

4. 修改任意文件，另一个都改变

5. 删除源文件，软链接不能使用

   

硬链接： 

​	特征：

1. 拥有相同的id节点和存储block快，可以看做是同一个文件
2. 可通过id节点识别
3. 不能跨分区
4. 不能针对目录使用

### **三、文件搜索命令**

1. 文件搜索命令locate （搜索速度快）

   **locate  文件名**  

   在后台数据库中按文件名搜索

   

   **/var/lib/mlocate**

   locate命令所搜索的后台数据库（默认一天更新一次）

   

   **updatedb**

   更新数据库

2. 命令搜索命令 where is 与 which

   **whereis 命令名**（**只能搜索系统文件**）

   搜索命令所在**路径**及**帮助文档**所在位置

   选项：

   ​	-b： 只查找可执行文件

   ​	-m： 只查找帮助文件

   **which** 

   搜索命令所在路径及**别命**

   **PATH 环境变量**

   定义的是系统搜索命令的**路径**

   

3. 文件搜索命令 find （相比于locate要慢，占用资源大，功能强大）

   **find命令**

   find [搜索范围] [搜索条件]

   

   **find / -name install.log**

   避免大范围搜索，会非常消耗系统资源

   find：是在系统当中搜索符合条件的文件名。如果需要匹配，使用通配符匹配，通配符是完全匹配。

   

   **Linux中的通配符**

   *** **    匹配任意内容

   **？**	匹配任意一个字符

   **[]**	  匹配任意一个中括号内的字符

   

   **find /root -iname install.log**

   不区分大小写

   

   **find /root -user root**

   按照所有者搜索

   

   **find /root -nouser**

   查找没有所有者的文件

   

   f**ind  /var/log/ -mtime  **+10

   查找10天前修改的文件

   

   -10  10天内修改文件

   10 	10天当天修改的文件

   +10	10天前修改的文件

   

   atime  文件访问时间

   ctime	改变文件属性

   mtime	 修改文件内容

   

   **find  .  -size  25k**

   查找文件大小是25KB的文件

   

   -25k	小于25KB的文件

   25k	等于25KB的文件

   +25k	大于25KB的文件

    

   **find	.	 -inum 	262422**

   查找i节点是262422的文件

   

   **find  /etc  -size  +20k  -a  -size  -50k**

   查找/etc/目录下，大于20kb并且小于20kb的文件

   -a  and   逻辑与，两个条件都满足

   -o    or	逻辑或，两个条件满足一个即可

   

   **find	/etc	-size	+20k	-a	-size	-50k	-exec ls	-lh {}  \;**

   查找/etc/目录下，大于20kb并且小于20kb的文件，并显示详细信息

   -exec/-ok  命令 {}\;	对搜索结果执行操作

   

4. 字符串搜索命令 grep

   grep [选项] 字符串	文件名

   在文件当中匹配符合条件的字符串

   选项：

   ​	-i  忽略大小写

   ​	-v  排除指定字符串

5. find命令与grep命令的区别

   find命令：在系统当中搜索符合条件的文件名，如果需要匹配，使用通配符匹配，通配符是完全匹配。

   grep命令：在文件当中搜索符合条件的字符串，如果需要匹配，使用正则表达式进行匹配，正则表达式时包含匹配。

### **四、帮助命令**

1. 帮助命令man

   **man命令**

   获取指定命令的帮助

   

   **man -f 命令**

   相当于

   **whatis 命令**

   

   **man -k 命令**

   相当于

   **apropos 命令**

   

   **man ls**

   查看ls的帮助

2. 其他帮助命令

   **命令	--help**

   获取命令选项的帮助

   例如：ls	--help

   

   **shell内部命令帮助**

   help 	shell内部命令

   获取shell内部命令的帮助

   

   例如：

   ​	**whereis   cd**

   ​		确定是否是shell内部命令

   ​	**help cd**

   ​		 获取内部命令帮助

   

   **详细命令帮助info**

   **info 命令**

   ​	—回车： 进入子帮助页面（带有*号标记）

   ​	— u：进入上层页面

   ​	— n： 进入下一个帮助小节

   ​	— p:	进入上一个帮助小节

   ​	— q： 推出

### **五、压缩与解压缩命令**

1. ​	常用压缩格式： .zip	.gz	.bz2

   **.zip格式压缩**

   **zip 压缩文件名发	源文件 **

   压缩文件

   

   **zip  -r   压缩文件名   源目录**

   压缩目录

   

   **.zip格式解压缩**

   **unzip 压缩文件**

   解压缩.zip文件

   

   **.gz格式压缩**

   **gzip  源文件**

   压缩为.gz格式的压缩文件，源文件会消失

   

   **gzip	-c	源文件  >  压缩文件**

   压缩为.gz格式，源文件保留

   例如： gzip	-c cangls	>   cangls.gz

   

   **gzip -r 目录**

   压缩目录下所有的子文件，但是不能压缩目录

   

   **.gz格式解压缩**

   **gzip  -d   压缩文件**

   解压缩文件

   

   **gunzip  压缩文件**

   解压缩文件

   

   **.bz2格式压缩**

   **bzip2	源文件**

   压缩为.bz2格式，不保留源文件

   

   **bzip2	-k	源文件**

   压缩之后保留源文件

   **注意**：bzip2命令不能压缩目录

   

   **.bz2格式解压缩**

   **bzip2  -d   压缩文件**

   解压缩，-k保留压缩文件

   

   **bunzip2   压缩文件**

   解压缩，-k保留压缩文件

   

2. ​    常用压缩格式：.tar.gz		.tar.bz2

    **打包命令tar**

   **tar -cvf  打包文件名   源文件**

   选项：

   ​	-c： 打包

   ​	-v： 显示过程

   ​	-f： 指定打包后的文件名

   例如：

   ​	tar   -cvf    longzls.tar    longzls

   

   **解打包命令**

   **tar	-xvf  打包文件名**

   ​	选项：

   ​		-x: 解打包

   ​	例如：

   ​		tar -xvf  longzls.tar

   

   **.tar.gz压缩格式**

   **其实.tar.gz格式是先打包为.tar格式，再压缩为.gz格式**

   **tar -zcvf  压缩包名.tar.gz  源文件**

   选项：	

   ​	-z:  压缩为.tar.gz格式

   

   **tar -zxvf  压缩包名.tar.gz**

   选项:

   ​	-x:  解压缩.tar.gz格式

   

   **.tar.bz2压缩格式**

   **tar -zcvf  压缩包名.tar.bz2    源文件**

   选项：	

   ​	-j:  压缩为.tar.bz2格式

   **tar -jcvf  压缩包名.tar.bz2  **

   选项：	

   ​	-x:  压缩为.tar.bz2格式

### **六、关机和重启命令**

1. ​	shutdown命令

   shutdown   [选项] 时间

   ​	选项：	

   ​		-c ： 取消前一个关机命令

   ​		-h ： 关机

   ​		-r ： 重启

2.    logout  退出

### **七、其他常用命令**

1. 挂载命令

   1. **查询与自动挂载**

      **[root@localhost ~] # mount**

      查询系统中已经挂在的设备

      

      **[root@localhost ~] # mount  -a**

      依据配置文件/etc/fstab的内容，自动挂载

      

   2. **挂载命令格式**

      **[root@localhost ~] # mount [-t 文件系统] [-o 特殊选项]  设备文件名   挂载点**

      选项：

      ​	-t  文件系统： 加入文件系统类型来指定挂载的类型，可以ext3、ext4、iso9660等文件系统

      ​	-o  特殊选项 ： 可以指定挂载的额外选项

   3. **挂载光盘**

      **[root@localhost ~] # mkdir /mnt/cdrom/**

      建立挂载点

      **[root@localhost ~] #  mount -t iso9660  /dev/cdrom/mnt/cdrom/**

      挂载光盘

       mount  /dev/sr0/     /mnt/cdrom/

      

   4. **卸载命令**

      **[root@localhost ~]# umount**

       设备文件名或挂载点

      

      **[root@localhost ~] # umount/mnt/cdrom**

       

   5. **挂载u盘**

      **[root@localhost ~] #  fdisk -l**

      查看u盘设备文件名

      

      **[root@localhost ~] #  mount -t  vfat  /dev/sdb1/mnt/usb/**

      **注意**：Linux默认是不支持NTFS文件系统的

2. 用户登录查看和用户交互命令

   1. **查看登录用户细信息**

      w  用户名

      命令输出：

      ​	USER：登录的用户名

      ​	TTY： 登陆终端

      ​	FROM: 从哪个IP地址登录

      ​	LOGIN@ : 登陆时间；

      ​	IDLE: 用户闲置时间；

      ​	JCPU: 指的是和该终端连接的所有进程占用的时间。这个时间里并不包括过去的后台作业时间，但却包括当前正在运行的后台作业所占用的时间；

      ​	PCPU：是指当前进程所占用的时间；

      ​	WHAT：当前正在运行的命令

   2. **who  用户名**

      命令输出：

      ​	— 用户名

      ​	— 登录终端

      ​	— 登录时间（登录来源IP地址）

   3. **查询当前登录和过去登录的用户信息**

      last

      last命令默认是读取/var/log/wtmp文件数据

      命令输出

      ​	— 用户名

      ​	— 登陆终端

      ​	— 登录IP

      ​	— 登录时间

      ​	— 退出时间（在线时间）

   4. **查看所有用户的最后一次登录时间**

      lastlog

      lastlog命令默认是读取/var/log/lastlog文件内容

      命令输出

      ​	— 用户名

      ​	— 登陆终端

      ​	— 登录IP

      ​	— 最后一次登陆时间

## Shell基础

### 一、Shell概述

Shell是一个命令行解释器，它为用户提供了一个向Linux内核发送请求以便运行程序的界面系统级程序，用户可以用Shell来启动、挂起、停止甚至是编写一些程序。



Shell还是一个功能相当强大的编程语言，易编写，易调试，灵活性较强。Shell是解释执行的脚本语言，在Shell中可以直接调用Linux系统命令。



Shell的两种主要语法类型有**Bourne**和**C**，这两种语法彼此不兼容。



**Bash**：Bash与sh兼容，现在使用的Linux就是使用Bash作为用户的基本Shell。

1. **脚本执行方式**

   1. **echo 输出命令**

      echo [选项] [输出内容]

      选项:

      ​	-e :  支持反斜线控制的字符转换

      [root@localhost ~]# echo  -e "hell**\b**o"

      '**\b**': 删除左侧字符

      [root@localhost ~]# echo  -e "h**\t**el**\n**lo"

      '**\t**':制表符

      '**\n**':换行符

      [root@localhost ~]# echo  -e "**\x**68"

      '**\x**':十六进制符

      [root@localhost ~]# echo  -e "**\e[1;31m**巴拉巴拉**\e[0m**"

      '**\e[1;31m**':开启颜色

      '**\e[0m**':关闭颜色

      '**3xm**':代表颜色

   2. **第一个脚本**

      [root@localhost ~]# vi hello.sh

      **#!/bin/bash**  :不是注释，代表这之下的内容都是Linux的标准脚本

   3. **脚本执行**

      赋予执行权限，直接运行

      **chmod 755 hello.sh**

      **./hello.sh**

      通过Bahs调用执行脚本

      **bash hello.sh**

### 二、Bash的基本功能

1. 命令别名与快捷键

   **命令别名（小名）**

   **查看与设定别名**

   **alias**

   查看系统中所有的命令别命

   **alias    别命 = ‘原命令’**

   设定命令别命

   

   **别命永久生效与删除别名**

   **vi ~/.bashrc**

   写入环境变量配置文件

   **unalias 别名**

   删除别名

   

   **命令生效顺序**

   **第一顺位执行用绝对路径或相对路径执行的命令。**

   **第二顺位执行别名。**

   **第三顺位执行Bash的内部命令。**

   **第四顺位执行按照$PATH环境变量定义的目录查找顺序找到的第一个命令**

   

   **常用快捷键**

   ctrl + c 	强制终止当前命令

   ctrl + l		清屏

   ctrl + a		光标移动到命令行首

   ctrl + e		光标移动到命令行尾

   ctrl + u		从光标所在位置删除到行首

   ctrl + z		把命令放入后台

   ctrl + r		在历史命令中搜索

    

2. 历史命令

   **history [选项] [历史命令保存文件]**

   选项：

   ​	-c : 清空历史命令

   ​	-w: 把缓存中的历史命令写入历史命令保存文件~/.bash_history

3. 输出重定向

   1.**标准输入输出**

   | 设备   | 设备文件名  | 文件描述符 | 类型         |
   | ------ | ----------- | ---------- | ------------ |
   | 键盘   | /dev/stdin  | 0          | 标准输入     |
   | 显示器 | /dev/sdtout | 1          | 标准输出     |
   | 显示器 | /dev/sdterr | 2          | 标准错误输出 |

   2.**输出重定向**

   | 类型                       | 符号                  | 作用                                                     |
   | -------------------------- | --------------------- | -------------------------------------------------------- |
   | 标准输出重定向             | 命令 >文件            | 以覆盖的方式，把命令的正确输出输出到指定的文件或设备当中 |
   |                            | 命令 >> 文件          | 以追加的方式，把命令的正确输出输出到指定的文件或设备当中 |
   | 标准错误输出重定向         | 错误命令 2> 文件      | 以覆盖的方式，把命令的错误输出输出到指定的文件或设备当中 |
   |                            | 错误命令 2>> 文件     | 以追加的方式，把命令的错误输出输出到指定的文件或设备当中 |
   | 正确输出和作物输出同时保存 | 命令 > 文件 2>&1      | 以覆盖的方式，把正确输出和错误输出都保存到同一个文件当中 |
   |                            | 命令 >> 文件 2>&1     | 以追加的方式，把正确输出和错误输出都保存到同一个文件当中 |
   |                            | 命令 &> 文件          | 以覆盖的方式，把正确输出和错误输出都保存到同一个文件当中 |
   |                            | 命令 &>> 文件         | 以追加的方式，把正确输出和错误输出都保存到同一个文件当中 |
   |                            | 命令>>文件1  2>>文件2 | 把正确的输出追加到文件1中，把错误的输出追加到文件2中     |

   3.**输入重定向**

   **[root@localhost ~]# wc  [选项] [文件名]**

   选项：

   ​	-c 统计字节数

   ​	-w 统计单词数

   ​	-l 统计行数

   

   **命令<文件**     把文件作为命令的输入

   **命令<<标识符**

   标识符把标识符之间内容作为命令的输入

4. 管道符

   1. **多命令顺序执行**

      | 多命令执行符 |       格式       | 作用                                                         |
      | :----------: | :--------------: | ------------------------------------------------------------ |
      |      ；      |  命令1 ; 命令2   | 多个命令顺序执行，命令之间没有任何逻辑联系                   |
      |      &&      |   命令1&&命令2   | 逻辑与      当命令1正确执行，则命令2才会执行    当命令1执行不正确，则命令2不会执行 |
      |     \|\|     | 命令1 \|\| 命令2 | 逻辑或    当命令1执行不正确，则命令2才会执行     当命令1正确执行，则命令2不会执行 |

   2. **管道符**

      **命令格式：**

      **[root@localhost ~]# 命令1 | 命令2**

      命令1的正确输出作为命令2的操作对象

5. 通配符

   | 通配符 | 作用                                                         |
   | :----: | ------------------------------------------------------------ |
   |   ？   | 匹配一个任意字符                                             |
   |   *    | 匹配0个或任意多个任意字符，也就是可以匹配任何内容            |
   |   []   | 匹配中括号中任意一个字符。例如：[abc]代表一定匹配一个字符，或者是a，或者是b，或者是c。 |
   |  [-]   | 匹配中括号中任意一个字符，-代表一个范围。例如：[a-z]代表匹配一个小写字母。 |
   |  [^]   | 逻辑非，表示匹配不是中括号内的一个字符。                     |

   [^0-9] :表示匹配一个不是数字的字符



## Liunx网络基础

### 一、网络基础

1. **iso/osi七层模型**

   iso：国际标准化组织

   osi：开放系统互联模式

   ios：苹果操作系统

   <img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210808101619636.png" alt="image-20210808101619636" style="zoom: 50%;" />

   | 层级名称   | 特点                                                         | 常见设备   |
   | ---------- | ------------------------------------------------------------ | ---------- |
   | 物理层     | 数据传递，设备之间的比特流的传输、物理接口、电气特性等。二进制：0101010 | 网线、网卡 |
   | 数据链路层 | 成帧、用MAC(物理地址)地址访问媒介、错误检测与修正            |            |
   | 网络层     | 提供逻辑地址（ip地址），选路                                 |            |
   | 传输层     | 可靠(**tcp**)与不可靠(**udp**)的传输，传输前的错误检测、流控 |            |
   | 会话层     | 对应用会话的管理、同步                                       |            |
   | 表示层     | 数据的表现形式、特定功能的实现如-加密                        |            |
   | 应用层     | 用户接口                                                     |            |

   

2. **TCP/IP四层模型**

   ![img](https://images2018.cnblogs.com/blog/1295451/201803/1295451-20180306155925918-725762113.png) 

   | 层级名称   | 概念                                                         |
   | ---------- | ------------------------------------------------------------ |
   | 网络接口层 | 网络接入层与OSI参考模型中的物理层和数据链路层相对应。它负责监视数据在主机和网络之间的交换。事实上，TCP/IP本身并未定义该层的协议，而由参与互联的各网络使用自己的物理层和数据链路层协议，然后与TCP/IP的网络接入层进行连接。地址解析协议(ARP)工作在此层，即OSI参与模型的数据链路层。 |
   | 网际互联连 | 网际互联层对应于OSI参考模型的网络层，主要解决主机到主机的通信问题。它所包含的协议设计数据包在整个网络上的逻辑传输。该层有三个主要协议：网际协议(IP)、互联网组管理协议(IGMP)和互联网控制报文协议(ICMP) |
   | 传输层     | 传输层对应于OSI参考模型的传输层，为应用层体提供端到端的通信功能，保证了数据包的顺序传送及数据的完整性。该层定义了两个主要的协议：传输控制协议(TCP)和用户数据报协议(UDP). |
   | 应用层     | 应用层对应OSI参考模型的高层，为用户提供所需要的各种服务。例如:FTP、Telnet、DNS、SMTP等 |

   #### TCP/IP三次握手

   ![image-20210808131825769](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210808131825769.png)

   ![img](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/11.png) ![image-20210808131801940](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210808131801940.png)

   

   TCP/IP模型与OSI模型的比较

   - 共同点

     OSI参考模型和TCP/IP参考模型都采用了层次结构的概念

     都能够提供面向连接和无连接两种通信服务机制

   - 不同点

     前者为七层模型、后者是四层结构

     对可靠性要求不同(后者更高)

     OSI模型是在协议开发前设计的，具有通用性。TCP/IP是先有协议集然后建立模型，不适用于非TCP/IP网络。

     实际市场应用不同(OSI模型只是理论上的模型，并没有成熟的产品，而TCP/IP已经成为“实际上的国际标准”)。

3. **IP地址**

    ip包头![这里写图片描述](http://www.pianshen.com/images/631/bc269448946232ada0023f482600b69f.png) 

   

    IP地址分类

   ![ip地址分类](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/ip_class.png) ![image-20191210151125990](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191210151125990.png)

    注：**不同类型的ip地址中对应的不同的网络号和主机号的位数，这是由子网掩码所决定的。**

   ip地址和子网掩码必须要在一起查看，不能分开查看。

![image-20210808134923336](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210808134923336.png)

4. **端口的作用**

   ​       TCP包头![fb1a4e4988fa28ce8395d61329ebbd47.png](http://kwin.xyz/passages/Linux/NetworkManage/网络基础/18.png) 

   UDP包头

    ![img](http://kwin.xyz/passages/Linux/NetworkManage/网络基础/19.png) 

   常见端口号

   FTP (文件传输协议) : 20、21

   SSH (安全shell协议) ：22

   telnet (远程登录协议)：23

   DNS (域名系统)：53

   http (超文本传输协议)：80

   SMTP (简单邮件传输协议)： 25

   POP3 (邮局协议3代)： 110

   

   查看本机启用的端口

    netstat -an
   选项：
     -a：查看所有链接和监听端口
     -n：显示IP地址和端口号，而不显示域名和服务名 

5.  **DNS作用**

   例子：http://www.baidou.com/  => 域名

   192.168.80.68 => ip地址

   ip地址和域名之间的相互转换

   

   hosts文件

   windows中的位置：C:\windows\System32\drivers\etc\hosts

   作用：做静态IP和域名对应

   

   从Hosts文件到DNS

   早期Hosts文件解析域名

   ​	名称解析效能下降

   ​	主机维护困难

   DNS服务

   ​	层次性

   ​	分布式

    ![36bae27e3ac13bcb2e05b9ececf0b8d7.png](http://kwin.xyz/passages/Linux/NetworkManage/%E7%BD%91%E7%BB%9C%E5%9F%BA%E7%A1%80/20.png)

    将域名解析为IP地址

   ​	客户机向DNS服务器发送域名查询请求

   ​	DNS服务器告知客户机Web服务器的IP地址

   ​	客户机与Web服务器通信

   

   域名空间结构

   ![image-20191210164754643](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191210164754643.png)

   组织域

    <img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191210165153406.png" alt="image-20191210165153406" style="zoom:80%;" />

   国家或地区域

   ![image-20191210165421920](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191210165421920.png)

   

   DNS查询过程

    ![5be2adb43172d7a969686b7d97802eb3.png](http://kwin.xyz/passages/Linux/NetworkManage/网络基础/22.png)

   

   DNS查询类型

   - 从查询方式上分
     – 递归查询
       - 要么做出查询成功响应，要么做出查询失败的响应。一般客户机和服务器之间属递归查询，即当客户机向DNS服务器发出请求后，若DNS服务器本身不能解析，则会向另外的DNS服务器发出查询请求，得到结果后转交给客户机。
     – 迭代查询
       - 服务器收到一次迭代查询回复一次结果，这个结果不一定是目标IP与域名的映射关系，也可以是其他DNS服务器的地址。
   - 从查询内容上分
     – 正向查询由域名查找IP地址
     – 反向查询由IP地址查找域名

6. **网关作用**

   理论概念 

   - 网关(Gateway)又称网间连接器、协议转换器。
   - 网关在网络层以上实现网络连接，是最复杂的网络互联设备，仅用于两个高层协议不同的网络互连。
   - 网关既可以用于广域网互连，也可以用于局域网互连。
   - 网关是一种充当转换重任的服务器或路由器

   总结：
   
   - 网关在又有内网计算机访问的不是本网段（不在局域网内）的数据包时使用
   - 网关负责将内网IP转换为公网IP，公网IP转换为内网IP。



### 二、Linux网络配置

1. **Linux配置IP地址**

   - ifconfig命令临时配置IP地址

   - setup工具永久配置IP地址
   - 修改网络配置文件
   - 图形界面配置IP地址

2. **Linux网络配置文件**

   **网卡信息文件**

   /etc/sysconfig/network-scripts/ifcfg-eth0

   ![image-20191212142527194](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191212142527194.png)

   

   **主机名文件**

   vi /etc/sysconfig/network

   ![image-20191212143116587](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191212143116587.png)

   

   **DNS配置文件**

   vi  /etc/resolv.conf

   ![image-20191212143217302](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191212143217302.png)

   

3. **虚拟机网络参数配置**

   1.配置LinuxIP地址

   ![image-20191212144837390](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191212144837390.png)

   2.启动网卡

   ![image-20191212144901015](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191212144901015.png)

   3.修改UUID

   修改UUID的目的：首先是进行了克隆操作，复制了一份虚拟机，导致UUID相同，相同的情况就会导致无法上网，因此需要修改UUID。

   ![image-20191212144936720](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191212144936720.png)

   4.设置虚拟机网络连接方式

   ​	桥接：VM生成的虚拟网卡利用真实的网卡来实现连接。优点：配置简单。缺点：需要占用一				个IP。

   ​	NAT：虚拟机和真实机之间通讯 ,可以访问公网，但是不可以与局域网其他计算机进行访问。

   ​	Host-only: 只能和真实机之间进行通讯，既不能访问公网，也不能与局域网内其他计算机访				问。

   5.修改桥接网卡

   ​	

### 三、Linux网络命令

1. 网络环境查看命令

   - ifconfig：查看与配置网络状态命令

   - ifdown: 网卡设备名

     禁用该网卡设备

   - ifup： 网卡设备名

     启动该网卡设备

   - netstat 选项  ：查询网络状态 

     选项：

     ​	-t：列出TCP协议端口

     ​	-u：列出UDP协议端口

     ​	-n：不适用域名与服务名，而使用IP地址和端口号

     ​	-l：仅列出在监听状态网络服务

     ​	-a：列出所有的网络连接

   - netstat -rn

     选项:

     ​	-r：列出路由列表，功能和route命令一致 

   - route -n  : 查看路由列表（可以看到网关）

   - nslookup [主机名或IP]：进行域名与IP地址解析

2. 网络测试命令

   - ping  ip或域名

     探测指定IP或域名的网络状态

     选项：

     ​	-c 次数：指定ping包的次数

   - telnet [域名或IP] [端口]

     远程管理与端口探测命令

   - traceroute [选项] IP或域名

     路由跟踪命令

     选项:

     ​	-n 使用IP,不适用域名，速度更快

   - **wget :下载命令**

   - tcpdump -i eh0 -nnX port 21

     选项:

     ​	-i 指定网卡接口

     ​	-nn	将数据包中的域名与服务转为IP和端口

     ​	-X	以十六进制和ASCII码显示数据包内容

     ​	port	指定监听的端口 

### 四、远程登陆

1. SSH协议原理

   **对称加密算法**

   采用单钥密码系统的加密方法，同一个密钥可以同时用作信息的加密和解密，这种加密方法称为对称加密，也称为单密钥加密。

   ![image-20191212165506354](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191212165506354.png)

   **非对称加密算法**

   非对称加密算法，又名"公开密钥加密算法",非对称加密算法需要两个密钥：公开密钥和私有密钥。

   ![image-20191212165935918](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191212165935918.png)

   **SSH安全外壳协议**

   ![image-20191212170326217](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191212170326217.png)

   

      **SSH命令**

   ssh 用户名@ip

   远程管理制定Linux服务器

   

   scp [-r] 用户名@ip:文件路径  本地路径

   下载文件

   

   scp [-r] 本地文件 用户名@ip: 上传路径

   上传文件

   

2. SecureCRT远程管理工具

3. Xshell工具和WinSCP文件传输工具



## 系统管理

### 一、进程管理

- 进程管理简介

   **简介：**

   进程是正在执行的一个程序或命令，每一给进程都是一个运行的实体，都有自己的地址空间，并占用一定的系统资源。

   

   **进程管理的作用**

   - 判断服务器健康状态
   - 查看系统中所有进程
   - 杀死进程

- 进程的查看-ps命令和pstree命令

   **查看所有进程**

   ps	aux

   查看系统中所有进程，使用BSD操作系统格式

   ![image-20191213153451056](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191213153451056.png)

   ![image-20191213154033266](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191213154033266.png)

   ps	-le

   查看系统中所有进程，使用Linux标准命令格式

   选项

   ​	a：显示一个终端的所有进程，除了会话引线

   ​	u：显示进程的归属用户及内存的使用情况

   ​	x：显示没有控制终端的进程

   ​	-l：长格式显示。显示更加详细的信息

   ​	-e：显示所有进程，和-a作用一致

   **查看进程数**

   pstree [选项]

   选项：

   -p：显示进程的PID

   -u：显示进程的所属用户

- 进程的查看-top命令

   **查看系统健康状态**

   top [选项]

   选项：

   ​	-d 秒数：指定top命令每隔几秒更新。默认是3秒

   ​	-b：使用批处理模式输出。一般和"-n"选项合用

   ​	-n次数：指定top命令执行的次数。一般和"-b"选项合用

    在top命令的交互模式当中可以执行的命令：

   ​	？或h：显示交互模式的帮助

   ​	p：以CPU使用率排序，默认就是此项

   ​	M：以内存的使用率排序

   ​	N：以PID排序

   ​	q：推出top	

   

   ![image-20191213161404464](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191213161404464.png)

   第一行信息为**任务队列信息**

   | 内容                           | 说明                                                         |
   | ------------------------------ | ------------------------------------------------------------ |
   | 09:42:37                       | 系统当前时间                                                 |
   | up 13:10                       | 系统的运行时间，本机已经运行13小时10分钟                     |
   | 3 users                        | 当前登录了两个用户                                           |
   | load average: 0.01, 0.01, 0.00 | 系统在1分钟之前，5分钟，15分钟的平均负载。一般认为小于1时，负载较小。如果大于1，系统已经超出负荷。 |

   第二行为**进程信息**

   | 内容             | 说明                                      |
   | ---------------- | ----------------------------------------- |
   | Tasks: 241 total | 系统中的进程总数                          |
   | 1 running        | 正在运行的进程数                          |
   | 236 sleeping     | 睡眠的进程                                |
   | 4 stopped        | 正在停止的进程                            |
   | 0 zombie         | 僵尸进程。如果不是0，需要手工检测僵尸进程 |

    第三行为**CPU信息**

   | 内容            | 说明                                  |
   | --------------- | ------------------------------------- |
   | Cpu(s):  0.0%us | 用户模式占用的CPU百分比               |
   | 0.0%sy          | 系统模式占用的CPU百分比               |
   | 0.0%ni          | 改变过优先级的用户进程占用的CPU百分比 |
   | 99.9%id         | 空闲CPU的CPU百分比                    |
   | 0.0%wa          | 等待输入/输出的进程的占用CPU百分比    |
   | 0.0%hi          | 硬中断请求服务占用的CPU百分比         |
   | 0.0%si          | 软中断请求服务占用的CPU百分比         |
   | 0.0%st          | st(Steal   time) 虚拟时间百分比。     |

   第四行为**物理内存信息**

   | 内容                  | 说明                                                         |
   | --------------------- | ------------------------------------------------------------ |
   | Mem:   1029652k total | 物理内存的总容量，单位为KB                                   |
   | 488388k used          | 已经使用的物理内存数量                                       |
   | 541264k free          | 空闲的物理内存数量，我们使用的是虚拟机，总共只分配了628MB内存，所有只有53MB的空闲内存了 |
   | 55972k buffers        | 作为缓冲的内存数量                                           |

   第五行为**交换分区(swap)信息**

   | 内容                  | 说明                         |
   | --------------------- | ---------------------------- |
   | Swap:  1023996k total | 交换分区（虚拟内存）的总大小 |
   | 0k used               | 已经使用的交换分区的大小     |
   | 1023996k free         | 空闲交换分区的大小           |
   | 308340k cached        | 作为缓存的交换分区的大小     |

   

- 杀死进程

   **kill命令**（对**单一**进程起作用）

   kill -l 

   查看可用的进程信号

   ![image-20191213172243138](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191213172243138.png)

   **平滑重启**

   作用：重新加载配置文件，但是不会断开正在连接服务器的用户信号。

   kill  -HUP  [Id号]

    

   **杀死单个进程**

   kill  -[信号]  [Id号]

   

   **killall命令** (杀死多个进程) 

   killall [选项] [信号] 进程名

   按照进程名杀死进程

   选项：

   ​	-i：交互式，询问是否要杀死某个进程

   ​	-I：忽略进程名的大小写

   

   **pkill命令** (杀死多个进程) 

   pkill [选项] [信号] 进程名

   按照进程名终止进程

   选项：

   ​	-t：终端号：按照终端号踢除用户

   **w**

   使用w命令查询本机已经登录的用户

   

- 修改进程优先级

  **简介**：Linux操作系统是一个多用户、多任务的操作系统，Linux系统中通知运行着非常多的进程。但是CPU在同一个时钟周期内只能运算一个指令。进程优先级决定了每个进程处理的先后顺序。 

   

  **PRI**代表**Priority**，**NI**代表**Nice**。这两个值都是优先级，**数字越小**代表该**进程优先级越高**

  ![image-20191216103850062](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191216103850062.png)

  

  **修改NI值时有几个注意事项**

  -  NI的值的范围是-20到19； 
  - 普通用户调整NI值的范围是0-19，而且只能调整自己的进程
  - 普通用户只能调高NI值，而不能降低，如原本NI值为0，则只能调整为大于0；
  - root用户才能设定进程NI值为负值，而且可以调整任何用户的进程。
  - PRI（最终值）=PRI（原始值）+NI
  - 用户只能修改NI的值，不能直接修改PRI

  

   **nice命令**

  nice [选项] 命令

  nice命令可以给新执行的命令直接赋予NI值，但是不能修改已经存在进程的NI值

  选项：

  ​	-n Ni: 给命令赋予NI值

  例如：

  ​	nice	-n	-5	service httpd start

  

### 二、工作管理

- 工作管理简介

  **简介**：工作管理指的是：在单个登录终端中（也就是登录的shell界面中）同时管理多个工作的行为。

   **注意事项**：

  - 当前的登录终端，只能管理当前终端的工作 ，而不能管理其他登录终端的工作
  - 放入后台的命令必须可以持续运行一段时间，这样我们才能捕捉和操作这个工作
  - 放入后台执行的命令不能和前台用户有交互或需要前台输入，否则放入后台只能暂停，而不能执行

- 工作管理方法

  **把进程放入后台**

  **在命令后面 + &符号**

  tar  -zcf etc.tar.gz/etc	&

  把命令放入后台，并在后台**执行**

  

  top

  按下ctrl+z快捷键，放在后台**暂停**

  

  **查看后台的工作**

  jobs	[-l]

  选项：

  ​	-l：显示工作的PID

  注：”+“号代表最近一个放入后台的工作，也是工作恢复时，默认恢复的工作。 ”-“号代表倒数第二个放入后台的工作

  

  **将后台暂停的工作恢复到前台执行**

  fg	%工作号

  参数：

  ​	-%工作号：%号可以省略，但是注意工作号和PID的区别

  

  **将后台暂停的工作恢复到后台执行**

  bg	%工作号

  注：后台恢复执行的命令，是不能和前台有交互的，否则不能恢复到后台执行

  

- 后台命令脱离登录终端执行

  **简介**：把命令放入后台，只能在当前登录终端执行。一旦退出或关闭终端，后台程序就会停止。

  

  **后台命令脱离登录终端执行的方法**

  第一种方法是需要后台执行的命令加入/etc/rc.local文件

  第二种方法是使用系统定时任务，让系统在指定的时间执行某个后台命令

  第三种方法是使用nohup命令

  

  **nohup命令**

  nohup[命令]	&

  

### 三、系统资源查看

- **vmstat命令监控系统资源**

  vmstat	[刷新延时  刷新次数]

  例如：

  -vmstat 1 3

  ![image-20191216153124621](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191216153124621.png)

  procs：进程信息字段：

  ​	r：等待运行的进程数，数量越大，系统越繁忙

  ​	b：不可被唤醒的进程数量，数量越大，系统越繁忙

  memory:	内存信息字段

  ​	swpd：虚拟内存的使用情况，单位KB

  ​	free：空间的内存容量，单位KB

  ​	buff:	缓冲的内存容量，单位KB

  ​	cache：缓存的内存容量，单位KB

  

  **缓冲和缓存的区别**

  简单来说缓存（cache）是用来加速数据从硬盘中“读取”的，而缓冲（buffer）是用来加速数据“写入”硬盘的。

  

  swap:交换分区的信息字段：

  ​	si：从磁盘中交换到内存中数据的数量，单位KB

  ​	so：从内存中交换到磁盘中数据的数量，单位KB。此两个数越大，证明数据需要经常在磁盘			和内存之间交换，系统性能越差。

  io：磁盘读写信息字段：

  ​	bi：此块设备读入数据的总量，单位是块。

  ​	bo：写到块设备的数据的总量，单位是块。此两个数越大，代表系统的I/O越繁忙

  CPU：CPU信息字段

  ​	us：非内核进程消耗CPU运算时间的百分比。

  ​	sy：内核进程消耗CPU运算时间的百分比。

  ​	id：空闲CPU的百分比。

  ​	wa：等待I/O所消耗的CPU百分比。

  ​	st：被虚拟机所盗用的CPU占比。

- **dmesg开机时内核检测信息**

  dmesg

  dmesg | grep  CPU

- **free命令查看内存使用状态**

  free [-b|-k|-m|-g]

  选项：

  ​	-b:	以字节为单位显示

  ​	-k：以KB为单位显示，默认就是以KB为单位显示

  ​	-m:	以MB为单位显示

  ​	-g：以GB为单位显示

- **查看CPU信息**

  cat/proc/cpuinfo

- **uptime命令**

  uptime

  显示系统的启动时间和平均负载，也就是top命令的第一行。w命令也可以看到这个数据。

- **查看系统与内核相关信息**

  uname [选项]
  选项：

  ​	-a: 查看系统所有相关信息

  ​	-r：查看内核版本

  ​	-s：查看内核名称

- **判断当前系统的位数**

  file/bin/ls

- **查询当前Linux系统的发行版本**

  lsb_release -a

- **列出进程打开或使用的文件信息**

  lsof	[选项]

  列出进程调用或打开的文件的信息

  选项：

  ​	-c字符串：只列出以字符串开头的进程打开的文件

  ​	-u用户名：只列出某个用户的进程打开的文件

  ​	-p	pid：列出某个PID进程打开的文件

  lsof | more

  查询系统中所有进程调用的文件

  lsof	/sbin/init

  查询某个文件被哪个进程调用

  lsof	-c	httpd

  查看httpd进程调用了哪些文件

  lsof	-u	root

  按照用户名，查询某用户的进程调用的文件名

### 四、系统定时任务

- **at一次性定时任务**

  - **确定at安装**

    chkconfig	--list | grep atd

    at服务是否安装

    

    service	atd	restart

    at服务的启动

  - **at的访问控制**

    如果系统中有/etc/at.allow文件，那么只有写入/etc/at.allow文件（白名单）中的用户可以使用at命令（/etc/at.deny文件会被忽略）

    如果系统中没有/etc/at.allow文件，只有/etc/at.deny文件,那么只有写入/etc/at.deny文件（黑名单）中的用户不能使用at命令。对root不起作用

    如果系统中这两个文件都不存在，那么只有root用户可以使用at命令。

  - **at命令**

    at	[选项] 时间

    选项：

    ​	-m:	当at工作完成后，无论是否命令有输出，都用email通知执行at命令的用户

    ​	-c	工作号：	显示该at工作的实际内容

    时间：

    ​	HH:MM

    ​	HH:MM	YYYY-MM-DD

    ​	HH:MM[am|pm]	[month] [date]

  - **其他at管理命令**

    atq

    查询当前服务器上的at工作

    

    atrm [工作号]

    删除指定的at任务

- **crontab循环定时任务**

  - **crond服务管理与访问控制**

    service	crond	restart

    chkconfig	crond	on	

  - **访问控制**

    如果系统中有/etc/cron.allow文件，只有写入此文件的用户可以使用crontab命令，没有写入的用户不能使用crontab命令。同样如果有此文件，/etc/cron.deny文件文件会被忽略，/etc/cron.allow文件的优先级更高。

    如果系统中只有/etc/at.deny文件，则写入此文件的用户不能使用crontab命令。没有写入文件的用户可以使用crontab命令。

  - **用户的crontab设置**

    crontab	[选项]

    选项：

    ​	-e：编辑crontab定时任务

    ​	-l：查询crontab任务

    ​	-r：删除当前用户所有的crontab任务

    crontab	-e

    进入crontab编辑界面。会打开vim编辑你的工作

    ***	*	*	*	* **  + 执行的任务

    ![image-20191216180401792](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191216180401792.png)

    ![image-20191216180751653](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191216180751653.png)

    

- **系统的crontab设置**

  - "crontab	-e"是每个用户执行的命令，也就是说不同的用户身份可以执行自己的定时任务。可是有些定时任务需要系统执行，这时我们就需要编辑/etc/crontab这个配置文件了

  - **系统定时任务**

    第一种是把需要定时执行的脚本复制到/etc/cron.{daily,weekly,monthly}目录中的任意一个

    第二个是修改/etc/crontab配置文件

- **anacron配置**

  - **anacron是什么**

    anacron是用来保证在系统关机的时候错过的定时任务，可以在系统开机之后再执行

  - **anacron检测周期**

    anacron会使用一天，七天，一个月作为检测周期

    在系统的/var/spool/anacron/目录中存在cron.{daily,weekly,monthly}文件，用于记录上次执行cron的时间

    和当前时间做比较，如果两个时间的差值超过了anacron的指定时间差值，证明有cron任务被楼执行

  - **anacron配置文件**

    ![image-20191217105612131](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191217105612131.png)

  - **cron.daily工作来说明执行过程**

    ![image-20191217110649583](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191217110649583.png)

​	

## 服务管理

### 一、简介与分类

- **系统的运行级别**

  ![image-20191217112520073](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191217112520073.png)

  - **运行级别命令**

    runlevel

    查看运行级别命令

    

    init 运行级别

    修改运行级别命令

    

  - **系统默认运行级别**

    vim /etc/inittab

    id:3:initdefault:

    系统开机后直接进入哪个运行级别

- **服务的分类**

  - **什么是服务**

    ![image-20191217142006163](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191217142006163.png)

    

  - **查询已安装的服务**

    RPM包安装的服务

    chkconfig	--list

    查看**服务自启动状态**，可以看到所有RPM包安装的服务，但是不能查看到源码包的自启动状态

    

    源码包安装的服务

    查看服务安装位置，一般是/usr/local/下

  - **启动与自启动**

    服务启动：就是在当前系统中让服务运行，并提供功能

    服务自启动：自启动是指让服务在系统开机或重启动之后，随着系统的启动而自动启动服务

- **服务于端口**

  - **端口**

    概念：如果把IP地址比作一间房子，端口就是出入这间房子的门。真正的房子只有几个门，但是一个IP地址的端口可以有65536个。

    ![image-20191218181025570](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191218181025570.png)

    

  - **端口与服务的对应**
  
    /etc/services
  
  - **查询系统中开启的服务**
  
    netstat -tlunp
  
    ​	-t :列出tcp数据
  
    ​	-u：列出udp数据
  
    ​	-l：列出正在监听的网络服务（不包含已经连接的网络服务）
  
    ​	-n：用端口号来显示服务，而不是用服务名
  
    ​	-P：列出该服务的进程ID(PID)
  
    
  
    列出系统中所有的已经**启动的服务**

### 二、RPM包服务管理

- **独立服务的管理**

  - **服务分类图**

    ![image-20191219102347554](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191219102347554.png)

    ![image-20191219102612502](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191219102612502.png)

     

  - **独立服务的启动**

    /etc/init.d/独立服务名

    start|stop|status|restart

    

    service	独立服务名

    start|stop|status|restart

    

  - **独立服务的自启动**

    chkconfig	[--level运行级别] [独立服务名] [on|off]

    

    修改/etc/rc.d/rc.local 文件

    

    使用ntsysv命令管理自启动

- **基于xinetd服务的管理**
  (不占用内存，但是效率低)
  
- **安装xinetd**
  
  yum	-y	install xinetd
  
- **xinetd服务的启动**
  
  ![image-20191219113718758](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191219113718758.png)
  
  
  
- **重启xinetd服务**
  
  service	xinetd	restart
  
  
  
- **xinetd服务的自启动**
  
  开启
  
  chkconfig rsync on
  
  
  
  关闭
  
  chkconfig rsync off
  
  
  
  ntsysv
  
  xinetd的自启动有缺陷：当关闭它的自启动时，同时也会关闭当前的服务。开启也是如此。

### 三、源码包服务管理

- **源码包安装服务的启动**

  使用绝对路径，调用启动脚本来启动。不同的源码包的启动脚本不同。可以查看源码包的安装说明，查看启动脚本的方法。

- **源码包服务的自启动**

  ![image-20191220105455425](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191220105455425.png)

  **RPM包的自启动方式**

  chkconfig	[--level运行级别] [独立服务名] [on|off]

  

  修改/etc/rc.d/rc.local 文件

  

  使用ntsysv命令管理自启动

  

  **源码包的自启动方式**

  只能通过修改/etc/rc.d/rc.local文件

  

- **让源码包服务被服务管理命令识别**（service、chkconfig不能默认识别源码包）

  软链接：ln -s

  ln	-s 	/usr/local/apache2/bin/apachectl		/etc/init.d/apache

  通过软链接就可以通过service命令来启动apache

- **让源码包的apache服务能被chkconfig与ntsysv命令管理自启动**

  ​	/etc/init.d/apache时通过上一步的软链接创建的

  在/etc/init.d/apache中加入图中的两句话

  ![image-20191220110532409](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191220110532409.png)

  **启动顺序：是哪个级别就进入哪个目录下**

  ![image-20191220111721862](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191220111721862.png)

  **进入目录后：**

  ![image-20191220112003447](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191220112003447.png)

  **启动顺序和关闭顺序：选择目录中没有的顺序号**

  

  **chkconfig --add	apache**

  

  **ntsysv  命令  默认也进行了配置，打开可以查找到**

### 四、服务管理总结

- 总结图

  ![image-20191220113948540](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191220113948540.png)

  

## 软件安装管理

### 一、软件包管理简介

- **软件包分类**

  - **源码包**

    脚本安装包

    优点：

    - 开源、如果有足够的能力，可以修改源代码
    - 可以自由选择所需的功能
    - 软件是编译安装，所以更适合自己的系统，更加稳定也有率更高
    - 卸载方便

    缺点：

    - 安装过程步骤较多，尤其安装较大的软件集合时（如LAMP环境搭建），容易出现拼写错误
    - 编译过程时间较长，安装比二进制包安装时间长
    - 因为是编译安装，安装过程中一旦报错新手很难解决

  - **二进制包（RPM包，系统默认包）**

    优点：

    - 包管理系统简单，只通过几个命令就可以实现包的安装、升级、查询和卸载
    - 安装速度比源码包安装快的多

    缺点：

    - 经过编译，不再可以看到源代码
    - 功能选择不如源码包灵活
    - 依赖性

  - **编译**

    abcd   =>  010101

### 二、rpm命令管理

- **RPM包命名规则**

  - **RPM包的来源**

    RPM包在系统光盘中

    /mnt/cdrom/Packages

  - **RPM包命名原则**

    ![image-20191217153041926](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191217153041926.png)

  -  **RPM包依赖性**

    树形依赖：a->b->c

    环形依赖：a->b->c->a

    模块依赖：查询网站：www.rpmfind.net

- **安装命令**

  - **包全名与包名**

    包全名：操作的包是没有安装的软件包时，使用包全名。而且要注意路径、

    包名：操作已经安装的软件包时，使用包名，是搜索/var/lib/rpm/中的数据库

  - **RPM安装**

    rpm -ivh 包全名

    选项：

    ​	-i(install)	安装

    ​	-v(verbose)	显示详细信息

    ​	-h(hash)	显示进度

    ​	--nodeps	不检测依赖性

- **升级与卸载**

  - **RPM包升级**

    rpm	-Uvh	包全名

    选项：

    ​	-U（upgrade）升级

  - **卸载**

    rpm	-e	包名

    选项：

    ​	-e(erase)	卸载

    ​	--nodeps不检测依赖性

- **RPM包查询**

  - **查询是否安装**

    rpm	-q	包名

    查询包是否安装

    

    ### rpm	-qa 

    查询所有安装的RPM包

  - **查询软件包详细信息**

    rpm	-qi	包名

    选项：

    ​	-i：查询软件信息（information）

    ​	-p：查询未安装包信息（package）

  - **查询包中文件安装位置**

    rpm -ql 包名

    选项：

    ​	-l 	列表（list）

    ​	-p	查询未安装包信息（package）

  - **RPM包默认安装位置**

    | RPM包默认安装路径 |                            |
    | ----------------- | -------------------------- |
    | /etc/             | 配置文件安装目录           |
    | /usr/bin/         | 可执行的命令安装目录       |
    | /usr/lib/         | 程序所使用的函数库保存位置 |
    | /usr/share/doc/   | 基本的软件使用手册保存位置 |
    | /usr/share/man/   | 帮助文件保存位置           |

  - **查询系统文件属于哪个RPM包**

    rpm 	-qf	系统文件名

    选项：	

    ​	-f：查询系统文件属于哪个软件包（file）

  - **查询软件包的依赖性**

    rpm	-qR 包名

    选项：

    ​	-R	查询软件包的依赖性（requires）

    ​	-p	查询未安装包信息（package）

- **RPM包校验**

  - **RPM包校验**

    rpm	-V 已安装的包名

    选项：

    ​	-V	校验指定RPM包中的文件（verify）

    ![image-20191217171334495](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191217171334495.png)

    ![image-20191217171848717](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191217171848717.png)

    

  - **RPM包中文件提取**

    rpm2cpio	包全名 | cpio	-idv.文件绝对路径

    rpm2cpio	

    将rpm包转换为cpio格式的命令

    cpio	

    是一个标准工具，它用于创建软件档案文件和从档案文件中提取文件

    

    cpio	选项 < [文件|设备]

    选项：

    ​	-i：copy-in模式，还原

    ​	-d: 还原是自动新建目录

    ​	-v：显示还原过程

### 三、yum在线管理

- **yum源文件**

  ![image-20191217174257933](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191217174257933.png)

  ![image-20191217174227479](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191217174227479.png)

- **光盘搭建yum源**

  - **挂在光盘**

    mkdir  /mnt/cdrom

    建立挂载点

    mount	/dev/cdrom   /mnt/cdrom/

    挂载光盘

  - **使网络yum源失效**

    cd	/etc/yum.repos.d/

    进入yum源目录

    mv	CentOS-Base.repo	CentOS-Base.repo.bak

    修改yum源文件后缀名，时期失效

  - **使光盘yum源生效**

    ![image-20191218093853980](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191218093853980.png)

    

- **yum命令**

  - **常用yum命令**

    查询

    yum 	list

    查询所有可用软件包列表

    

    yum	search	关键字

    搜索服务器上所有和关键字相关的包

    

  - **安装**

    yum -y install	包名（不再是rpm包中的包全名）

    选项：

    ​	install	安装

    ​	-y			自动回答yes

    例如：yum	-y	install	gcc	c语言的编译器

  - **升级**

    yum	-y	update	包名

    选项：

    ​	update	升级

    ​	-y				自动回答yes

  - **卸载**

    yum	-y	remove	包名

    选项：

    ​	remove		卸载

    ​	-y					自动回答yes

  - **yum软件组管理命令**、、

    yum	grouplist

    列出所有可用的软件组列表

    

    yum	groupinstall	软件组名

    安装指定软件组，组名可以由grouplist查询出来

    

    yum	groupremove	软件组名

    卸载指定软件组

### 四、源码包管理

- **源码包和RPM包的区别**

  - **区别**

    安装之前的区别：概念上的区别

    安装之后的区别：安装位置不同

  - **RPM包安装位置**

    | RPM包默认安装路径 |                            |
    | ----------------- | -------------------------- |
    | /etc/             | 配置文件安装目录           |
    | /usr/bin/         | 可执行的命令安装目录       |
    | /usr/lib/         | 程序所使用的函数库保存位置 |
    | /usr/share/doc/   | 基本的软件使用手册保存位置 |
    | /usr/share/man/   | 帮助文件保存位置           |

  - **安装位置不同带来的影响**

    RPM包安装的服务可以使用系统服务管理命令(service)来管理，例如RPM包安装的apache的启动方法是：

    ​	/etc/rc.d/init.d/httpd start

    ​	service httpd start

  - **源码包安装位置**

    安装在指定位置当中，一般是	/usr/local/软件名/

    

    源码包没有卸载命令

    

    而源码包安装的服务则不能被服务管理命令管理，因为没有安装到默认路径中。所以只能用绝对路径进行服务的管理。

    如：

    /usr/local/apache2/bin/apachectl start

- **源码包安装过程**

  - **安装准备**

    安装C语言编译器

    yum	-y	install	gcc	c语言的编译器

    

    下载源码包

     http://archive.apache.org/dist/httpd/ 

    

  - **安装注意事项**

    源代码保存位置：/usr/local/src/

    软件安装位置：/usr/local/

    如何确定安装过程报错：

    ​	安装过程停止

    ​	并出现error、warning或no的提示

  - **源码包安装过程**

    下载源码包

    解压缩下载的源码包

    进入解压缩目录

  - **./configure 软件配置与检测**

    定义需要的功能选项

    检测系统环境是否符号安装要求

    把定义好的功能选项和检测系统环境的信息都写入Makefile文件，用于后续的编辑

  - **make编译**

    make clean	清楚编译后的缓存文件

  - **make install    编译安装**

  - 源码包的卸载

    不需要卸载命令，直接删除安装目录即可。不会遗留任何垃圾文件。

### 五、脚本安装包

- **强大的Nginx服务器**

  简介：Nginx是一款轻量级的Web服务器/反向代理服务器及电子邮件(IMAP/POP3)代理服务器，由俄国公司在2004年发布

- **准备工作**

  - **关闭RPM包安装的httpd和MySQL**

  - **保证yum源正常使用**

  - **关闭SELinux和防火墙i**

  - **一键安装包下载**

    https://lnmp.org/download.html 

  -  **解压缩**

    tar -zxvf  lnmp1.0-full.tar.gz

  - **centos.sh脚本分析**

    ![image-20191218154135666](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191218154135666.png)

    

  - **执行centos.sh脚本**

    ./centos.sh

    

## 权限管理

### 一、文件基本权限

- **基本权限的修改**

  ![image-20191220143041959](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20191220143041959.png)

  - **chmod	[选项]	模式	文件名**

    选项

    ​	-R   递归

    模式

    ​	[ugoa]	[+-=]	[rwx]

    ​	[mode=421]

  -  **修改权限的方式**

    添加

    chmod	u+x	文件

    chmod	g+w,o+w	文件

    删除

    chmod	u-x	文件

    chmod	g-w,o-w	文件

    

    更方便	(全部)

    chmod	a=rwx	文件

    

  - **权限的数字表示**

    r	----	4

    w	-----	2

    x	-----	1

    

    rwxr-xr-x

    7	5	5

    

    chmod	755    文件

- **权限的作用**

  -   **权限对文件的作用**

    r:	读取文件内容(cat	more	head	tail)

    w:	编辑、新增、修改文件内容(vi	echo)

    ​	但是不包含删除文件

    x：可执行

    

    **注意**：对文件的权限，r和x不用多说，字面上的意思，但是对于w的权限，需要注意的是，除了编辑、新增以及修改的功能外，最重要的一点是：即使拥有了r、w、x这三个权限，你所能操作的也只是文件中的数据而已，你不能对文件本身进行操作，你不能删除它。如果想做到删除文件，你需要的是获得当前文件的上一级目录的权限，你需要去操作目录才能删除文件。

  - **权限对目录的作用**

    r：可以查询目录下文件名 （ls）

    

    w：具有修改目录结构的权限。如新建文件和目录，删除此目录下文件和目录，重命名此目录下文件和目录，剪切（touch、rm、mv、cp）

    

    x:	可以进入目录	(cd)

- **其他权限命令**

  - **修改文件的所有者**

    chown	用户名	文件名

    例如：chown	ds	fengj.av

    

  -  b chgrp	组名	文件名

    例如：chgrp	group1	fengi.av

  - 

- 

### 二、文件默认权限

### 三、ACL权限

### 四、文件特殊权限

### 五、不可改变位权限

### 六、sudo权限





