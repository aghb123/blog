---
title: Linux
---
# Linux系统学习(Centos 8)

## 快捷键

|        功能        |      快捷键       |
| :----------------: | :---------------: |
|    快速打开终端    |    Ctrl+Alt+T     |
| 快速至当前行的行首 |       Home        |
| 快速至当前行的行尾 |        End        |
|     快速至某行     | 冒号(:)+行号+回车 |
|   快速至最后一行   |  冒号(:)+$+回车   |
|  刷新屏幕（清屏）  |       clear       |

添加快速打开终端快捷键

> /usr/bin/gnome-terminal

Centos8中文输入

> sudo dnf install ibus-libpinyin.x86_64 -y

## 命令解析器

`shell -- UNIX  bash -- Linux`

本质：根据命令的名字，调用对应的可执行程序

###快捷键

|        作用        |     快捷键      |
| :----------------: | :-------------: |
|      历史命令      | ctrl+P 、ctrl+N |
|      光标移动      | ctrl+B、ctrl+F  |
|   光标移动到头部   |     ctrl+A      |
|   光标移动到尾部   |     ctrl+E      |
| 删除光标前面的字符 |     ctrl+H      |
| 删除光标后面的字符 |     ctrl+D      |
|        清屏        |     ctrl+L      |

命令(目录)提示：`tab`

## 目录结构

> 1.根目录
>
> 2./bin 存放着最经常使用的命令
>
> /boot 存放启动Linux时使用的一些核心文件
>
> /dev 存放的是Linux的外部设备
>
> /etc 存放所有的系统管理需要的配置文件
>
> /home  存放所有用户的目录
>
> /lib 存放系统最基本的动态链接共享库
>
> /media  挂载外设
>
> /usr 用户的很多应用程序和文件都放在这个目录下，类似于windows下的program files

## 用户目录

1. 绝对路径：从根目录开始写 /home/admin

2. 相对路径： 相对于当前的工作目录而言

   `.`当前目录

   `..`当前的上一级目录

   `-` 在临近的两个目录中切换

`root@wz ~`:root 当前用户名，wz 主机名，~用户家目录

`$`:普通用户

`#`:超级用户（root)

## 文件和目录操作

### 查看目录结构

1.安装tree

> 文件或目录颜色-一般情况
>
> 白色--普通文件
>
> 蓝色--目录
>
> 绿色--可执行文件
>
> 红色--压缩文件
>
> 青色--链接文件
>
> 黄色--设备文件（block块，字符，FIFO 管道）
>
> 灰色--其它文件

```drwx------.  5 root root    66 12月 18 21:37 .mozilla
drwxr-----.  3 root root    19 12月 17 21:38 .pki
drwxr-xr-x.  2 root root   160 12月 18 20:42 projects
drwxr-xr-x.  2 root root   167 12月 18 22:42 so_lib
```

第`1`个字符

`-`普通文件

`d`目录

`l`链接符号

`b`块设备

`c`字符设备

`s`socket文件

`p`管道

第`2-4`个字符：文件所有者权限

第`5-7`个字符：文件所属组权限

第`8-10`个字符：其他人权限

第`11`个字符：文件的硬链接数

后面的对应分别是文件或目录所有者，所属组，占用的存储空间，文件最后创建或修改的时间，文件名

###目录及文件相关命令

创建复合目录

`mkdir a/b/c -p` 或者 `mkdir -p a/b/c`

删除目录

`rm -r`递归删除目录及文件

`rm -ri`增加询问是否删除

创建文件 `touch`(文件不存在则创建文件，文件存在修改文件时间)

查看文件内容 `cat`

复制文件

`cp hello.c temp` hello.c源文件 temp目标文件（如果目标文件已存在，将覆盖）

复制目录

`cp myTest/ newDir -r`需要加参数`r`

文件过长，使用`more`命令

使用回车键阅读下一行，使用空格阅读下一页，`Q`键或`Ctrl+C`组合键退出

也可以使用`less`命令，回车显示下一行，空格显示下一页，`ctrl+p`或:arrow_up:滚动到上一行，`ctrl+n`或:arrow_down:滚动到下一行，`Q`推出浏览

查看前十行：`head 文件名`

查看后十行：`tail 文件名`

`mv 源文件名 目标文件名`修改文件名

如果目标文件名存在且为目录，那么执行的是移动文件的操作

创建链接

`ln -s 原始文件 目标文件` 加参数`-s`为软链接，类似快捷方式，不加类似`shared_ptr`

查看文件大小`du -h`

查看磁盘使用情况`df -h`

查看(外部)命令位置`which`

###修改文件的权限

1.文字设定法

`chmod [who] [+|-|=] [mode]`

`who`:文件所有者`u`，文件所属组`g`，其他人`o`，所有人`a`

`+`添加权限，`-`减少权限，`=`覆盖原来的权限

`mode`:`r`读，`w`写，`x`执行

例`chmod o+w nju`

 2.数字设定法

`-`：没有权限

`r`：4，`w`：2，`x`：1

例`chmod 777 nju2`

`chmod -001 nju2`

### 修改文件所有者和文件所属组

`chown root:admin nju`所有者（也可以设定所属组）

`chgrp admin nju2`所属组

**目录应该拥有执行权限，否则无法访问目录内的内容**

### 文件的查找

1.按文件属性查找

1>文件名：`find + 查找的目录 + -name + 文件的名字`，文件名可能有必要加双引号

2>文件大小：`find + 查找目录 + -size + 文件大小`

例`find /root/ -size +10M -100M`大于10M，小于100M

3>文件类型：`find + 查找目录 + -type + d/f/b/c/s/p/l`

### 文件的检索

`grep -r 查找的内容 路径`

## 软件的安装和卸载

`ubuntu`

`sudo apt-get install tree`安装

`sudo spt-get remove tree`移除

`sudo apt-get update`更新软件列表

`sudo apt-get clean`清理所有软件安装包

## 挂载设备

`fdisk -l`查看系统连接的硬盘设备

`mount 设备名称 挂载目录`挂载设备

`umount 设备名称`卸载设备

尽量挂载在`/mnt`目录下

## 压缩

1. `gzip\bzip2 压缩内容`	

2. `tar`: 参数 `c`-创建-压缩 `x`- 释放-解压缩 `v`- 显示提示信息-压缩解压缩 `f`-指定压缩文件的名字 `z`-使用`gzip`方式压缩文件-`.gz`  `j`- 使用`bzip2`方式压缩文件-`.bz2`

   例：`tar zcvf 生成的压缩包名称 压缩的文件目录`

   解压缩 `tar zxvf 压缩包名称 (-C 解压目录)`

3. `rar`: 参数 `a`压缩 `x`解压缩

   <https://www.cnblogs.com/wangdidi/p/11394096.html>

   <https://www.cnblogs.com/934827624-qq-com/p/9640780.html>

   压缩 `rar a 生成的压缩文件的名字(temp) 压缩的文件或目录(-r)`

   解压缩 `rar x 压缩文件名 （解压缩目录）`

4. `zip`

   压缩：`zip 压缩包名字 压缩的文件或目录(-r)`

   解压缩：`unzip 压缩包的名字`  `unzip 压缩包的名字 -d 解压目录`

## 进程管理

###查看进程

`ps`:`-a`显示所有进程；`-u`用户以及其它详细信息；`-x`显示没有控制终端的进程

### 管道符

`A|B`:把命令`A`原本要输出到屏幕的标准正常数据当作是命令`B`的标准输入

### 查看进程的环境变量

`env`

## 用户管理

`adduser`

`useradd`

`groupadd`

`usermod`

`passwd`

`userdel`

## 服务器搭建

### ftp服务器

作用：文件的上传和下载，不允许操作目录

1>服务器端

`yum install vsftpd`安装服务程序

1）修改配置文件

`vim /etc/vsftpd/vsftpd.conf`

2）重启服务

`systemctl restart vsftpd`

3）将服务加入到启动项

`systemctl enable vsftpd`

<https://www.xuebuyuan.com/3204429.html>

<https://blog.csdn.net/wade3015/article/details/90725871>

**注意关闭防火墙**

2>客户端

1）实名用户登录

`ftp serverIP`

输入用户名

输入密码

文件的上传`put 文件` 登入`ftp`服务器时所在的目录才能上传

文件的下载`get 文件`

目录可以采取打包形式上传和下载

2）匿名用户登录

`ftp serverIP`

用户名：`anonymous`

密码：直接回车

**不允许匿名用户在任意目录直接切换**

需要在`ftp`服务器上创建一个匿名用户的目录--匿名用户的根目录

`/etc/vsftpd/vsftpd.conf`添加`anon_root=/home/admin/ftp_dir`

默认目录`/srv/ftp/`

其它相关配置

```
wirte_enable=YES
anonymous_enable=YES
anon_upload_enable=YES
anon_mkdir_write_enable=YES
```

3）退出

`quit` `bye` `exit`

2. `lftp`

   `ftp`**客户端**程序

   ```
   [admin@wz ~]$ lftp 192.168.186.134
   lftp 192.168.186.134:~> login
   用法：login <user|URL> [<pass>]
   lftp 192.168.186.134:~> 
   lftp 192.168.186.134:/> lpwd //查看登入ftp服务器时所在目录
   /home/admin
   lftp 192.168.186.134:/> pwd
   ftp://192.168.186.134/
   ```

   切换本地目录进行上传

   ```
   [admin@wz ~]$ lftp 192.168.186.134
   lftp 192.168.186.134:~> lcd /home/admin/projects
   lcd 成功，本地目录=/home/admin/projects
   lftp 192.168.186.134:/> mput nju nju2 nju3
   89104 bytes transferred
   Total 3 files transferred
   lftp 192.168.186.134:/> 
   ```

   `put`上传文件

   `mput`上传多个文件

   `get`下载文件

   `mget`下载多个文件

   `mirror`下载整个目录以及子目录

   `mirror -R`上传整个目录以及子目录

   **注**：从`vsftpd 2.3.5`之后，`vsftpd`增强了安全检查，如果用户被限定在其主目录下，则该用户的主目录不能再具有写权限了!如果检查发现还有写权限，就会报该错误

```
500 OOPS: vsftpd: refusing to run with writable root inside chroot()
```

​			可以将文件传输到主目录底下的文件夹中

<https://www.cnblogs.com/wplvqj/p/10537070.html>

### nfs服务器

1.服务器端

（1）创建共享目录

（2）修改配置文件

`/etc/exports`

`/home/admin/nfsshare 192.168.186.*(rw,sync)`

（3）重启服务

`systemctl restart nfs-server`

2.客户端

（1）挂载服务器共享目录

`mount serverIP:目录 挂载目录`

### ssh服务器

1. 服务器端

（1）安装`ssh`

2. 客户端

（1）远程登陆

`ssh userName@serverIP`

（2）退出登录

`logout`

3. `scp`命令

`scp -r 目标用户名@目标主机IP地址:/目标文件的绝对路径 /保存到本机的绝对（相对）路径`

拷贝目录需要加参数`-r`

## 其它命令

`man`看手册

`alias`查看别名

`alias pag='ps aux|grep'`设置别名，长久有效需要去设置配置文件`.bashrc`

## **vim**

vim是从vi发展过来的一款文本编辑器

### 命令模式

（1）光标的移动

`H J K L`

前 下 上 后

行首 `0`

行尾 `$`

文件开始位置：`gg`

文件末尾：`G`

行跳转：`300G`

<u>[vim编辑器代码格式设置](https://blog.csdn.net/qq_37934101/article/details/80287879)</u>

（2）删除(剪切)操作

`x`删除光标后面的字符 `X`删除光标前面的字符

删除单词：`dw`(光标移动到单词的开始位置)

删除光标到行首的字符串：`d0`

删除光标到行尾的字符串：`D(d$)`

删除光标当前行：`dd`

删除多行：`ndd`(n--自然数)

（3）撤销

`u`撤销上一步操作

反撤销`ctrl+r`

（4）粘贴

`p`粘贴到光标所在行下面

`P`粘贴到光标所在行

（5）复制

复制光标当前行：`yy`

复制多行：`nyy`(n--自然数)

（6）可视模式

切换可视模式`v`

选择内容：`h j k l`

操作：复制：`y` 删除：`d`

（7）查找操作

1. `/string`

2. `?string`

3. `#`--把光标移动到查找的单词身上，按`#`

   遍历的快捷键`N/n`

4. 取消查找

   `:noh`命令行模式

<u>[vim编辑器查找替换](https://blog.csdn.net/u010003835/article/details/83146301)</u>

<u>[vim编辑器查找替换](https://blog.csdn.net/qq_30123335/article/details/83374849?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.control)</u>

（8）`r`替换当前字符

缩进：向右`>>` 向左`<<`

查看`man`文档，光标停留在想要查看的内容上，按`shift + k`

（9）切换文本模式

`a`：在光标所在位置的后边插入

`A`：在当前行的尾部插入

`i`：在光标所在位置的前边插入

`I`：在光标所在行的行首插入

`o`：在光标所在行的下边开辟一个新的行

`O`：在光标所在行的上边开辟一个新的行

`s`：删除光标后边的字符

`S`：删除光标所在的行

### 末行模式

`:数字`跳转到某一行

`:s/tom/jack`：替换当前行的第一个tom为jack

`:s/tom/jack/g`：替换当前行所有的tom为jack

`:%s/tom/jack`：替换整个文档的tom为jack

`:27,30s/tom/jack/g`：替换第27-30行的所有tom为jack

**`:!pwd`：执行命令**

`:x`：保存退出

**命令模式下保存退出：`zz`**

### 分屏操作

末行模式下

`sp`水平分屏

`vsp`垂直分屏

`sp(vsp) + 文件名`水平或垂直拆分窗口显示两个不同的文件

`ctrl + w + w`分屏切换

`wqall`保存并退出所有屏幕

`wq`保存并退出光标所在的屏幕

### 配置文件

系统级配置文件目录：`/etc/vim/vimrc`

用户级配置文件目录：`/home/admin/.vimrc`

<https://www.icode9.com/content-3-684756.html>

<u>[自动在运算符两边加上空格](https://blog.csdn.net/weixin_30342827/article/details/95561651)</u>(**去除`<>`，否则`#include<stdio.h>`会出问题**)

<u>[vim教程](https://www.w3cschool.cn/vim/)</u>

## gcc编译

预处理器`cpp`：头文件展开，宏替换，注释去掉 `gcc -E hello.c -o hello.i`

编译器`gcc`：c文件变成汇编文件`gcc -S hello.i -o hello.s`

汇编器`as`：汇编文件变为二进制文件`gcc -c hello.s -o hello.o`

链接器`ld`：将函数库中相应的代码组合到目标文件中`gcc hello.o -o hello`

## 编译器安装

1.安装编译器``gcc&g++``

```markdown
yum install gcc //安装gcc
yum install gcc-g++ //安装g++
```

2.编写第一个程序

```markdown
vim main.cpp
#include<iostream>
#include<vector>
#include<string>
using namespace std;
int main()
{
	vector<string> msg{"Hello,","NanJing University!"};
	for(auto word:msg){
		cout<<word;
	}
	cout<<endl;
	return 0;
}
g++ main.cpp
./a.out
```

3.修改vim编辑器的缩进等格式

```markdown
vim ~/.vimrc
set tabstop=4 //设置制表符宽度
set softtabstop=4 //设置制表符宽度
set shiftwidth=4 //设置缩进的空格数
set number //显示行数
set autoindent //每行的缩进值与上一行相等
set cindent //使用C/C++语言的自动缩进方式
set ruler //显示标尺
imap {<CR> {<CR>}<ESC>O //设置括号自动缩进
imap [ []<ESC>i //输入左中括号的时候自动补齐右中括号，并在括号中间输入i
imap ( ()<ESC>i //输入左小括号的时候自动补齐右小括号，并在括号中间输入i
imap [ []<LEFT> //输入左中括号的时候自动补齐右中括号
imap ( ()<LEFT> //输入左小括号的时候自动补齐右小括号
set nonumber //不显示行号
```

4.生成可执行文件的别名

```
g++ main.cpp -o nju
```

##C与C++混合编程

<https://blog.csdn.net/qq_33750826/article/details/83868555>

增加一个C文件程序，假如是``a.h``

```c
#ifndef _A_H_
#define _A_H_
extern "C"{
    void testC();
}
#endif
```

编写实现``a.c``

```c
#include "a.h"
#include <stdio.h>
void testC(){
    printf("I'm C language program\n");
}
```

在``main.cpp``中调用`testC()`函数

```c++
#include<iostream>
#include "a.h"
#include<vector>
#include<string>
using namespace std;
int main()
{
	vector<string> msg{"Hello,","NanJing University!"};
	for(auto word:msg){
		cout<<word;
	}
	cout<<endl;
	testC();
	return 0;
}
```

编译程序

```
g++ a.c main.cpp -o nju2
```

## 编译

程序的执行顺序：**编译->链接->运行**

使用选项`-c`,如下：

```
g++ -c 文件名
```

实例：

```
g++ -c a.c -o a.o
g++ -c main.cpp -o main.o
g++ main.o a.o -o nju3
```

通过`g++`命令的`-c`选项接文件名的形式将程序进行编译

接着通过`g++`接编译后的`*.o`文件进行链接，生成可执行程序，通过

```
ldd 可执行程序
```

可以看到该可执行程序所链接的库

最后通过`./程序名`进行运行程序

**指定头文件路径**

**`gcc main.c -I ./include -o nju`**

```c
#include<stdio.h>
//#define DEBUG

int main()
{
    int a = 10; 
    int b = 20; 
    int sum = a + b;
#ifdef DEBUG
    printf("The sum value is:% d +% d =% d\n",a,b,sum);
#endif
    return 0;
}
```

**通过定义宏来决定部分代码块是否执行**

`gcc hello.c -o hello -D DEBUG`编译时指定宏

`-O`代码优化，最高等级`3`

`-Wall`提示

`-g`添加调试信息

## 编写makefile

>从前面可以知道命令
>
>``g++ -c *.o``既可编译程序
>
>``g++ *.o``既可链接文件，生成可执行程序
>
>那么当我们的程序非常庞大的时候，``.cpp、.c``文件如此之多，那么我们还是通过一个一个``g++``去敲文件名的形式去编译和链接吗？这想必是非常麻烦的，也不符合我们程序员的作风，那么这个时候便引入了`makefile`，通过该脚本，我们便可以轻松的管理我们的程序文件，接下来展示怎么编写`makefile`！

我们接着第四小节的程序，首先编写一个makefile:

```
vim makefile
start:
	g++ -o main.o -c main.cpp
	g++ -o a.o -c a.c
	g++ -o nju4 a.o main.o
```

其中

1.`makefile`为脚本的名字

2.`start`可以随便命名，这里写为`start`表示是程序的开始部分

3.`start`后面接的`:`，表示`start`为可以执行的部分，可通过命令`make start`执行

4.`g++`命令前面的空白部分，注意不是空格，必须是键盘左上角的**tab键**

最后编译`makefile`脚本，使用`make`命令（初次使用，可能需要安装），如下：

```
make或者make start
```

因为`start:`为该`makefile`脚本的第一个可执行部分脚本代码，所以直接通过`make`也可执行`start:`所示部分

可以看到通过makefile脚本编译链接后的`*.o`文件是没有作用的了，可以通过添加命令删除，如下：

```
vim makefile
start:
	g++ -o main.o -c main.cpp
	g++ -o a.o -c a.c
	g++ -o nju4 a.o main.o
clean:
	rm -rf a.o main.o
```

可以看到`makefile`中是完全兼容linux命令的，所以只要再添一个`clean:`部分，即可通过`make clean`执行，如下：

> make clean

对上面的makefile进行优化，如下：

```
vim makefile
XX=g++
start:
	$(XX) -o main.o -c main.cpp
	$(XX) -o a.o -c a.c
	$(XX) -o nju4 a.o main.o
clean:
	rm -rf a.o main.o
```

定义方式：

```
变量别名=变量值
```

使用方式：

```
$(变量别名)
```

类似于一个简单的赋值操作，也非常类似于C和C++中的宏定义去定义一个全局的变量

好处：

>当有相同变量值（文件名，命令等）重复时，可能我们需要批量去管理该变量，那么这时候只需要定义一个全局的变量，以助于我们方便管理该变量

如我们上述所示的`g++`，我们以后可能会替换成`gcc`等，那么使用之前的形式，便需要一个个修改，通过如上述所示可以直接修改`XX=`右边的值即可，很方便

继续优化，如下：

```
vim makefile
X=g++
start:main.o a.o
	$(X) -o nju4 a.o main.o
a.o:
	$(X) -o a.o -c a.c
main.o:
	$(X) -o main.o -c main.cpp
clean:
	rm -rf a.o main.o
```

可以看到修改的是：

1.`start:main.o a.o`

这表示在`start:`部分执行之前，先去查找`main.o`与`a.o`是否存在，不存在则去执行

```
a.o:
	$(X) -o a.o -c a.c
main.o:
	$(X) -o main.o -c main.cpp
```

部分，使其先生成`a.o & main.o`，如果存在则直接进行链接。

接着修改`a.c`，如下：

```
vim a.c
#include "a.h"
#include <stdio.h>

void  testC(){
	printf("I'm C language program\n");
	printf("change!!!!\n");
}
```

**删除`a.o`**，在执行`make`命令

```
g++ -o a.o -c a.c
g++ -o nju4 a.o main.o
```

通过上面的分析，可以清晰的看到好处就是：

1.当已经编译生成了`.o`文件，则不会再进行编译，会直接进行链接

2.当某个文件进行了修改，只会再次编译该缺少的文件

这样当一个项目非常大的时候，这是非常节省编译时间的，不需要去编译重复的文件

继续优化，如下：

```
mv a.c a.cpp //修改文件名
vim makefile
X=g++
start:main.o a.o
	$(X) -o nju4 main.o a.o
.cpp.o:
	$(X) -o $@ -c $<
clean:
	rm -rf a.o main.o
```

可以看到，将之前的两部分编译部分合成了一句，通过：

1.`$<`表示编译的以`.cpp`结尾的源文件，所以上面首先通过`mv`命令将`a.c`重命名为`a.cpp`方便演示

2.`$@`表示将编译的结果重命名为`.o`文件

```
vim a.cpp
#include "a.h"
#include <stdio.h>

void  testC(){
	printf("I'm C language program\n");
	printf("change!!!!\n");
	printf("change!!!again\n");
}
```

> make

`g++ -o a.o -c a.cpp`

`g++ -o nju4 main.o a.o`

通过上面的分析，可以清晰的看到好处就是：

1.当已经编译生成了`.o`文件，则不会再进行编译，会直接进行链接

2.语句更加简便，方便管理

3.当某个文件进行了修改，只会再次编译修改的文件（**不需要删除已经改动文件的`.o`文件**）

这样当一个项目非常大的时候，这是非常节省编译时间的，不需要去编译重复的文件

接着优化：

```
vim makefile
XX=g++
SRCS=main.cpp/
	    a.cpp
OBJS=$(SRCS:.cpp=.o)

EXEC=nju5

start:$(OBJS)
	$(XX) -o$(EXEC) $(OBJS)
.cpp.o:
	$(XX) -o $@ -c $<
clean:
	rm -rf $(OBJS)
```

最后可以看到，将所有可能批量修改的变量通过定义变量别名的方式定义在脚本中，`OBJS=$(SRCS:.cpp=.o)`表示将所有`.cpp`文件前缀名直接复制到文件名`.o`，这样当我们增加了`.cpp`文件后就不用手动去增加`.o`文件

**1.那么make是怎么知道你修改了哪些文件呢？**

根据`.cpp`与`.o`的最后修改时间去判断是否需要编译，当`.o`文件都不存在时，则判断失去意义

**2.为什么make不关心`.h`文件？**

因为make是不关心`.h`文件的，是编译关心的，是`g++`关心的

`g++ -E a.cpp a1.cpp`，`-E`表示预编译，可以看到`a1.cpp`是在预编译的时候包含`.h`中所有的内容的

## Linux上编译so库，并兼容.c与.cpp的调用

首先简单的声明一个比较大小的函数，通过传入两个参数，比较两个参数的大小，谁大就返回谁的形式实现它，代码如下：

```
vim mylib.h
#ifndef MY_LIB_H
#define MY_LIB_H
int max(int a,int b);
#endif
vim mylib.c
#include"mylib.h"
int max(int a,int b){
	return a>b?a:b;
}
```

编写好`max`接口后那么该如何将它编译成`so库`的形式呢？通过学习，知道Linux程序都是`makefile`来进行编译的，那么`so库`的`makefile`该如何编写？

```
vim makefile
XX=gcc
SRCS=mylib.c
OBJS=$(SRCS:.c=.o)
EXEC=libmylib.so
start:$(OBJS)
	$(XX) -o $(EXEC) $(OBJS) -shared
.c.o:
	$(XX) -o $@ -c $< -fPIC
clean:
	rm -rf $(OBJS)
```

在Linux编译`so`，

1.首先so名称必须以**lib**开头，以**so**结尾

2.编译时必须加入`-fPIC`，表示这是编译so库，没有偏移位置

3.在链接时，需要指定`-shared`选项，标明是一个共享库

共享库制作完成，那么现在通过模拟一个`main.c`程序去调用编写的共享库是否可用

```
vim main.c
#include"mylib.h"
#include<stdio.h>
int main()
{
	printf("max=%d",max(5,6));
	return 0;
}
```

然后再编写`makefile`，看看效果

```
mv makefile makefile.lib
vim makefile
XX=gcc
SRCS=main.c
OBJS=$(SRCS:.c=.o)
EXEC=mylibTest
start:$(OBJS)
	$(XX) -o $(EXEC) $(OBJS)
.c.o:
	$(XX) -o $@ -c $<
clean:
	rm -rf $(OBJS)
```

最后再`make`一下，显示报错！

发现`max`是没有定义的，因为想使用共享库，但是却没有在`makefile`中指定该共享库，因此里面的函数肯定无法找到，那么如何在`makefile`中指定共享库呢？

```
vim makefile
XX=gcc
SRCS=main.c
OBJS=$(SRCS:.c=.o)
EXEC=mylibTest
start:$(OBJS)
	$(XX) -o $(EXEC) $(OBJS) -L. -lmylib
.c.o:
	$(XX) -o $@ -c $<
clean:
	rm -rf $(OBJS)
```

此时如果想要运行`mylibTest`，需要进行如下操作：

```
#vim /etc/ld.so.conf //在新的一行中加入库文件所在目录
/root/so_lib
#ldconfig  //更新/etc/ld.so.cache文件
```

或者

```
1.将用户用到的库统一放到一个目录，如/usr/local/lib
#cp libmylib.so /usr/local/lib/
2.向库配置文件中，写入库文件所在目录
#vim /etc/ld.so.conf.d/usr-libs.conf
/usr/local/lib
3.更新/etc/ld.so.cache文件
#ldconfig
```

<https://blog.csdn.net/yjk13703623757/article/details/53217377>

如果需要将库文件运行在`main.cpp`里面呢？

```
[root@wz so_lib]# cp main.c main.cpp
[root@wz so_lib]# vim makefile
  1 XX=g++
  2 SRCS=main.cpp
  3 OBJS=$(SRCS:.cpp=.o)
  4 EXEC=mylibTest
  5 start:$(OBJS)
  6     $(XX) -o $(EXEC) $(OBJS) -L. -lmylib
  7 .c.o:
  8     $(XX) -o $@ -c $<
  9 clean:
 10     rm -rf $(OBJS)
```

因为`.cpp`需要通过`g++`编译，所以需要将`gcc`改为`g++`进行编译

```
[root@wz so_lib]# make clean
rm -rf main.o
[root@wz so_lib]# make
g++ -o main.o -c main.c
g++ -o mylibTest main.o -L. -lmylib
main.o：在函数‘main’中：
main.c:(.text+0xf)：对‘max(int, int)’未定义的引用
collect2: 错误：ld 返回 1
make: *** [makefile:6：start] 错误 1
```

会发现`max`函数找不到，是因为`.cpp`和`.c`的编译形式，导致编译结果不一样，`main.cpp`认为`max`函数是`.cpp`编译出来的，所以找不到，需要更改`mylib.h`

```
  1 #ifndef MY_LIB_H
  2 #define MY_LIB_H
  3 extern "C"{
  4 int max(int a,int b);
  5 }
  6 #endif
```

更加通用的写法：

```
  1 #ifndef MY_LIB_H
  2 #define MY_LIB_H
  3 #ifdef _cplusplus
  4 extern "C"{
  5 #endif
  6 
  7 int max(int a,int b);
  8 #ifdef _cplusplus
  9 }
 10 #endif
 11 #endif
```

## 静态库

（1）命名规则

`lib+库的名字+.a`，例`libmytest.a`

（2）制作步骤

<1>生成对应的`.o`文件

<2>将生成`.o`文件打包 `ar rcs 静态库名字(libmytest.a) 生成的所有.o文件`

（3）发布和使用静态库

<1>发布静态库

<2>头文件

```
[admin@wz src]$ gcc -c *.c -I../include
[admin@wz src]$ ar rcs libMyCal.a *.o
[admin@wz src]$ mv libMyCal.a ../lib
[admin@wz libTest]$ tree
.
├── include
│   └── head.h
├── lib
│   └── libMyCal.a
└── src
    ├── add.c
    ├── add.o
    ├── div.c
    ├── div.o
    ├── mul.c
    ├── mul.o
    ├── sub.c
    └── sub.o
[admin@wz libTest]$ vim main.c
[admin@wz libTest]$ gcc main.c lib/libMyCal.a -o sum -Iinclude /方式一,不推荐
[admin@wz libTest]$ ./sum
sum =26
[admin@wz libTest]$ gcc main.c -Iinclude -L lib -l MyCal -o sum //方式二
```

```
[admin@wz lib]$ nm libMyCal.a

add.o:
0000000000000000 T add

div.o:
0000000000000000 T main

mul.o:
0000000000000000 T main

sub.o:
0000000000000000 T sub
```

静态库的**优点**：

1.发布程序的时候，不需要提供对应的库

2.加载库的速度快

静态库的**缺点**：

1.库被打包到应用程序中，导致库的体积很大

2.库发生改变，需要重新编译程序

## 共享库

（1）命名规则

`lib+名字+.so`

（2）制作步骤

<1>生成与位置无关的代码（生成与位置无关的`.o`）

<2>将`.o`打包成共享库（动态库）

```
[admin@wz src]$ gcc -fPIC -c *.c -I../include
[admin@wz src]$ gcc -shared *.o -o libMyCal.so
[admin@wz src]$ ls
add.c  add.o  div.c  div.o  libMyCal.so  mul.c  mul.o  sub.c  sub.o
[admin@wz src]$ mv libMyCal.so ../lib
[admin@wz src]$ cd ../lib
[admin@wz lib]$ ls
libMyCal.a  libMyCal.so
[admin@wz libTest]$ gcc main.c lib/libMyCal.so -o app -Iinclude //不推荐
[admin@wz libTest]$ ls
app  include  lib  main.c  src  sum
[admin@wz libTest]$ ./app
sum =26
[admin@wz libTest]$ gcc main.c -Iinclude -L./lib -lMyCal -o app
```

**解决动态库链接失败问题**

方法一

```
[admin@wz ~]$ export LD_LIBRARY_PATH=./libTest/lib //临时 
```

方法二

在`~/.bashrc`中添加`export LD_LIBRARY_PATH=/home/admin/libTest/lib`，需要重启终端

方法三

需要找到动态链接器的配置文件`/etc/ld.so.conf`，然后将动态库的绝对路径写到配置文件中，最后更新`ldconfig`

**共享库优点**：

1.执行程序体积小

2.动态库更新了，不需要重新编译程序（函数接口不变）

**共享库缺点**

1.发布程序时，需要将动态库提供给用户

2.动态库没有被打包到应用程序中，加载速度相对较慢

## GDB调试

编译过程加入调试信息`-g`

`gcc *.c -o app -g`

启动调试`gdb 程序名称`

```
[admin@wz gdb]$ gdb app
GNU gdb (GDB) Red Hat Enterprise Linux 8.2-14.el8
Copyright (C) 2018 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-redhat-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from app...done.
(gdb) l select_sort.c:20
warning: Source file is more recent than executable.
15	        }
16	        if(minValue != i)
17	        {
18	            tmp = arr[i];
19	            arr[i] = arr[minValue];
20	            arr[minValue] = tmp;
21	        }
22	    }
23	}
```

具体调试过程

```
(gdb) b 16 //打断点
Breakpoint 1 at 0x40096e: file main.c, line 16.
(gdb) l
21		}
22		insertionSort(array2,len);
23		printf("\n ============== Gorgeous Split Line ===============\n");
24		printf("Selection Sort:\n");
25	    for(i = 0;i<len;i ++)
26		{    
27	        printf("% d  ",array[i]);
28		}
29		printf("\n");
30		return 0;
(gdb) b 27 if i==15 //条件断点
Breakpoint 2 at 0x4009ef: file main.c, line 27.
(gdb) i b //显示断点信息
Num     Type           Disp Enb Address            What
1       breakpoint     keep y   0x000000000040096e in main at main.c:16
2       breakpoint     keep y   0x00000000004009ef in main at main.c:27
	stop only if i==15
(gdb) start //开启调试
Temporary breakpoint 3 at 0x400706: file main.c, line 7.
Starting program: /home/admin/gdb/app 
Missing separate debuginfos, use: yum debuginfo-install glibc-2.28-141.el8.x86_64

Temporary breakpoint 3, main () at main.c:7
7		int array[]={12,5,33,6,10,35,67,89,87,65,54,24,58,92,100,24,46,78,99,200,55,44,33,22,11,71,2,4,86,8,9};
(gdb) n //单步调试
8		int array2[]={12,5,33,6,10,35,67,89,87,65,54,24,58,92,100,24,46,78,99,200,55,44,    33,22,11,71,2,4,86,8,9};
(gdb) 
9		int len = sizeof(array)/ sizeof(int);
(gdb) c //持续进行直到遇到断点
Continuing.
Sort Array:
 12	 5	 33	 6	 10	 35	 67	 89	 87	 65	 54	 24	 58	 92	 100	 24	 46	 78	 99	 200	 55	 44	 33	 22	 11	 71	 2	 4	 86	 8	 9	

Breakpoint 1, main () at main.c:16
16		selectionSort(array,len);
(gdb) s //进入函数体内
selectionSort (arr=0x7fffffffdf40, n=31) at select_sort.c:6
warning: Source file is more recent than executable.
6	    for(i = 0; i < n - 1; i ++)
(gdb) l
1	#include"sort.h"
2	
3	void selectionSort(int * arr,int n)
4	{
5		int i, j , minValue, tmp;
6	    for(i = 0; i < n - 1; i ++)
7	    {
8	        minValue = i;
9	        for(j = i + 1; j < n; j ++)
10	        {

(gdb) b 9 //打断点
Breakpoint 4 at 0x400a46: file select_sort.c, line 9.
(gdb) i b //显示断点信息
Num     Type           Disp Enb Address            What
1       breakpoint     keep y   0x000000000040096e in main at main.c:16
	breakpoint already hit 1 time
2       breakpoint     keep y   0x00000000004009ef in main at main.c:27
	stop only if i==15
4       breakpoint     keep y   0x0000000000400a46 in selectionSort at select_sort.c:9
(gdb) c //持续进行直到断点
Continuing.

Breakpoint 4, selectionSort (arr=0x7fffffffdf40, n=31) at select_sort.c:9
9	        for(j = i + 1; j < n; j ++)
(gdb) p j //显示变量值
$1 = -139958283
(gdb) p i
$2 = 0
(gdb) p n
$3 = 31
(gdb) n 
11	            if(arr[minValue] > arr[j])
(gdb) p arr[minValue]
$4 = 12
(gdb) ptype arr //显示变量类型
type = int *
(gdb) ptype j
type = int
(gdb) display i //展示变量i的值
1: i = 0
(gdb) display j
2: j = 5
(gdb) n
11	            if(arr[minValue] > arr[j])
1: i = 0
2: j = 6
(gdb) 
9	        for(j = i + 1; j < n; j ++)
1: i = 0
2: j = 6
(gdb) info display //查看显示变量的编号
Auto-display expressions now in effect:
Num Enb Expression
1:   y  i
2:   y  j
(gdb) undisplay 1 //不显示编号为1的变量i
(gdb) n
9	        for(j = i + 1; j < n; j ++)
2: j = 14
(gdb) 
11	            if(arr[minValue] > arr[j])
2: j = 15
(gdb) finish //跳出当前函数体（需要删除断点或者等断点都执行完）
Run till exit from #0  selectionSort (arr=0x7fffffffdf40, n=31) at select_sort.c:16

Breakpoint 4, selectionSort (arr=0x7fffffffdf40, n=31) at select_sort.c:9
9	        for(j = i + 1; j < n; j ++)
2: j = 31
(gdb) i b
Num     Type           Disp Enb Address            What
1       breakpoint     keep y   0x000000000040096e in main at main.c:16
	breakpoint already hit 1 time
2       breakpoint     keep y   0x00000000004009ef in main at main.c:27
	stop only if i==15
4       breakpoint     keep y   0x0000000000400a46 in selectionSort at select_sort.c:9
	breakpoint already hit 2 times
(gdb) d 4 //删除编号为4的断点
(gdb) i b
Num     Type           Disp Enb Address            What
1       breakpoint     keep y   0x000000000040096e in main at main.c:16
	breakpoint already hit 1 time
2       breakpoint     keep y   0x00000000004009ef in main at main.c:27
	stop only if i==15
(gdb) finish //跳出当前函数体
Run till exit from #0  selectionSort (arr=0x7fffffffdf40, n=31) at select_sort.c:9
main () at main.c:17
17		printf("Selection Sort:\n");
(gdb) 
18		for(i = 0;i<len;i ++)
(gdb) 
20			printf("% d  ",array[i]);
(gdb) p i
$5 = 1
(gdb) display i
3: i = 1
(gdb) 
(gdb) n
18		for(i = 0;i<len;i ++)
3: i = 1
(gdb) 
20			printf("% d  ",array[i]);
3: i = 2
(gdb) 
18		for(i = 0;i<len;i ++)
3: i = 2
(gdb) 
20			printf("% d  ",array[i]);
3: i = 3
(gdb) set var i=10 //直接执行到i=10
(gdb) n
18		for(i = 0;i<len;i ++)
3: i = 10
(gdb) q //跳出调试
A debugging session is active.

	Inferior 1 [process 5582] will be killed.

Quit anyway? (y or n) y
```

###1.启动GDB

`start`---只执行一步

`n`---next

`s`---step(单步)---可以进入到函数体内部

`c`---continue---直接停在断点的位置

###2.查看代码

`l`---list

`l + 行号(函数名)`

`l + 文件名：行号（函数名）`

### 3.设置断点

设置当前文件断点

`b`---break

`b + 行号(函数名)`

设置指定文件断点

`b + 文件名：行号(函数名)`

设置条件断点

`b 行号 if value==10`

删除断点

`delete - del - d`

`d 断点的编号`

​		获取编号：`info -- i`

​				`info b`

### 4.查看设置的断点

`info b`

### 5.单步调试

进入函数体内部：`s`

从函数体内部跳出：`finish`

不进入函数体内部：`n`

退出当前循环：`u`

### 6.查看变量的值

`p`---print

### 7.查看变量的类型

`ptype 变量名`

### 8.设置变量的值

`set var 变量名 = 赋值`

### 9.设置追踪变量

`display 变量`

取消追踪变量

`undisplay 编号`

获取编号：`info display`

### 10.退出gdb调试

`quit`

## makefile的编写

### makefile的命名
