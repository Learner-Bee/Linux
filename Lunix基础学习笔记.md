#Linux教程
##Linux简介
Linux是一套免费使用和自由传播的类Unix系统。是一个基于POSIX和Unix的**多用户、多任务、多线程、多CPU**的操作系统。  
  支持32位和64位硬件  
**Linux VS Windows**   
1. Linux主要应用在服务器上，而桌面操作是Windows  
2. 同样内存，linux上运行速度更快，因为windows会存储一些图形化界面的数据占了部分内容  
3. linux开源免费。windows收费  
4. linux对用户的权限管理严格  
5. windows对用户没有要求，普通用户可以所以操作，安全性较低。而linux对用户要求较高，规避了一些风险  
6. linux系统安全性更高，没有漏洞、木马等的侵害  
##Linux安装  
以CentOS 6.8为例  
**版本选择**  
网易镜像：http://mirrors.163.com/centos/6/isos/  
1. binDVD：普通安装版本，需安装到本地计算机硬盘，bin版是最完整的版本，一般比较大，因为包含了大量常用软件。安装时无需在线下载。若是安装在虚拟机中学习，首选。  
DVD1：基本系统+部分软件包  
DVD2：更多的软件包  
2. liveDVD：光盘安装版。  
3. liveCD：相比liveDVD，是个精简的光盘CentOS系统，体积更小，便于维护。  
4. mininal版：迷你版，精简了更多东西。虚拟机学习，不推荐使用。因不带一些基本的软件，使用起来比较麻烦。  
5. netinstall：网络安装版，不推荐。   
**通过SecureCRT连接虚拟机上的Linux**  
>1. 通过ifconfig获取操作系统的ip地址  
>2. 在SecureCRT上新建连接，在connection下新建name，默认选择SSH2（安全外壳协议Secure Shell缩写）。  
>3. 在SSH2 下输入hostname (即连接系统的ip地址)，输入登录系统的用户名连接，输入密码即可  


##系统启动过程  
###启动过程分五个阶段：  
* 内核的引导  
* 运行init  
* 系统初始化  
* 建立终端  
* 用户登录系统  
### Linux系统7个运行级别  
* 0：系统停机状态，默认不能设为0，否则不能启动  
* 1：单用户工作状态，root权限。用于系统维护，禁止远程访问  
* 2：多用户状态（没有NFS，Network File System ）  
* 3：完全的多用户状态（有NFS）。登录后进入控制台命令行模式  
* 4：系统未使用，保留  
* 5：X11控制台。登陆后进入图形GUI模式  
* 6：系统正常关闭并重启。默认运行级别不能是6，否则不能正常启动   
###Linux关机  
正确的关机流程sync>shutdown>reboot>halt  
关机指令shutdown。可通过man shutdown查看帮助文档   
**给用户添加sudo权限**    
>1. 由普通用户进入超级用户模式（即进入root模式）。在普通模式下输入'su-'，然后输入root密码，回车，进入超级用户模式   
>2. 输入命令'visudo' 进入编辑模式。（编辑sudo的配置文件/etc/sudoers）  
>3. 找到'root ALL=(ALL) ALL'(可能当前页找不到，一直回车)在该行下面添加 Lilybo ALL=(ALL) ALL  
>4. 保存退出：w(保存)，exit(退出)  
###关机相关命令
* sync 将数据由内存同步到硬盘中（关闭或重启前一定要执行）  
* shutdown -h 10 'this server will shutdown after 10mins'  10分钟后系统关机，信息会显示在登录用户的当前屏幕 (h是halt缩写，停止的意思)   
* shutdown -h now 立马关机    
* halt   关闭系统   等同于上面命令和poweroff  、init 0（普通用户用命令sodu init 0）
* shutdown -h 20:25 系统会在20:25关机  
* shutdown -h +10 十分钟后  
* shutdown -r now 系统立马重启（reboot）    
* reboot 重启，等同意上面命令、init6  
* shutdown -r +10 系统10分钟后重启    
* shutdown -c 取消正在进行的重启  
* shutdown -k 10 并非真正关机，只是显示警告信息 。系统将在10分钟后关机  
##Linux系统目录结构 
**ls和ls / 区别**  
>ls 是文件列表命令，显示当前目录下的所有文件  
>ls / '/'表示根目录的意思，该命令意思显示根目录下的文件  

/bin bin是banary（二进制）缩写，该目录显示最常用的命令  
/boot 存放启动linux是的一些核心文件，包括镜像文件  
/dev device(设备)缩写。该目录存放的是linux的外部设备。访问设备和访问文件的方式是相同的  
/etc 存放所有系统管理所需要的配置文件和子目录   
/home 用户主目录。每个用户都有一个自己的目录。一般目录名已用户账号命名  
/lib 存放系统最基本的动态链接共享库。作用类似于window下的DLL文件。几乎所有的应用文件都需要用到这些共享库  
/lost+found 一般是空的。当系统非法关机后，这里会存放一些文件。  
/media linux会自动识别一些设备，如U盘、光驱等。当识别后，linux会把识别的设备挂载在该目录下  
/mnt 让用户临时挂载别的文件系统。我们可以将光驱挂载在该目录下，然后进入该目录就可以查看光驱里的内容了  
/opt 给主机额外安装软件所摆放的目录。如数据库等。默认为空  
/proc 该目录是虚拟目录。它是系统内存的映射，可以通过访问该目录获取系统信息 。该目录的内容不再硬盘上，而在内存里。可以直接修改里面的某些文件。  
/root 该目录是系统管理员，也称超级权限者的用户目录  
/sbin S是super user的意思。这里存放系统管理员使用的系统管理程序  
/selinux 该目录是Rethat/CentOS特有的。Selinux是一个安全机制，类似window下的防火墙，该目录就是存放selinux相关文件  
/srv 存放服务启动后需要读取的数据  
/sys  该目录安装文件系统sysfs  
/tmp 存放一些临时文件  
/usr 非常重要的目录。用户的很多应用程序和文件都放在这里。类似window下的program files  
/usr/bin 系统用户使用的应用程序  
/usr/sbin 超级用户使用的比较高级的管理程序  
/usr/src 内核源代码默认放置的目录  
/var 存放不断扩充的东西。习惯将经常被修改的目录放在该目录下，包括各种日志文件  
**几个比较重要不能修改的目录**  
/etc 系统配置文件，更改后可能系统不能启动  
/bin ,/sbin,/usr/bin,/usr/sbin  
/var 非常重要的目录。系统上跑的程序的日志存在该目录下。在/var/log下  
##Linux忘记root密码解决办法
###通过linux系统直接重置密码  
1. 重启linux,在3秒内回车，进入GRUB界面  
2. 选择操作系统，输入e进入  
3. 向下选择“kerner”内核那一行，输入e   
4. 在最后一行quiet 后面空格，然后输入single，回车，此时回到选择kerner 界面  
5. 按b，进入单用户模式，在这里修改密码  
6. 输入命令passwd  
7. 输入新密码，回车后，再输入一次密码  
8. init 6重启系统完成设置  
###记得root密码，通过远程连接修改密码 
1. 普通用户登录远程连接时，首先切换到root用户，输入命令su （切换到root）  
2. 输入root登录密码  
3. 进入到root下，输入passwd ，输入新密码，回车再次输入新密码。  
4. 成功后，切回普通用户，su lilybo    
###普通用户的密码忘记   
1. 进入管理员模式，su
2. 在root下输入命令：passwd lilybo,回车  
3. 输入新密码，确认密码。成功  
##Linux文件基本属性    
可以通过命令ll、ls-l来显示一个文件的属性、以及文件所属用户和组  
drwxr-xr-x  （10个字符组成，第一个表示文件类型，后面每3个一组，表示相应权限） 
   
1.  第0位。即第一个字符代表文件类型： [d]目录、[-]文件、[/]链接、[b]表示装置文件里面可供储存的接口设备（可随机存取装置）、[c]表示装置文件里面的串行端口设备，如键盘、鼠标（一次性读取装置）   
2. 以 [rwx] 组合。[r]表示read,可读；[w]write,可写；[x]execute，可执行。当没有选项时，就用[-]代替  
3. 1~3位，确定属主（文件所有者）拥有的该文件权限  
4. 4~6位，确定属组（所有者同组用户）拥有的权限  
5. 7~9位，确定其他用户对该文件的权限  
###更改文件属性  
* chgrp：更改文件属组(变更文件或目录的权限)  
  -[R] 属组名 文件名 R表示递归更改文件属组。在更改某个目录文件的属组时，该目录下的所有文件的属组都会更改   
* chown：更改文件属主，也可以同时更换属组  
  -[R] 属主名 文件名
  -[R] 属主名：属组名 文件名
  chown lilybo install.log 将install.log文件的拥有者改为lilybo 
  chown lilybo：lilybo install.log 将install.log的文件的拥有者和属组都改为lilybo  
* chmod：更改文件9个属性  
  1. 数字法  chmod -[R] xyz 文件或目录  
     r：4  w:2 x:1   
     [-rwxrwx---]  代表rwx:4+2+1=7 rwx:4+2+1=7  ---:0    最后权限数字是770（即xyz）  
     如：chmod 770 install.log   
  2. 符号类型   
     9个权限分别是user（u）、group（g）、others（o）三种身份 。 all(a)代表所有身份  
     chmod  u/g/o/a +(增加)/-(去除）/=(设定)  r/w/x  
## Linux文件与目录管理  
* 绝对路径：绝对路径的写法，由根目录“/”写起。如：/usr/share/doc  
* 相对路径：不是由“/”写起。如从/usr/share/doc 到/usr/share/man 。可以用 cd ../man.  
###处理目录的常用命令  
#### ls (list 列出目录 )  
  语法：ls [目录名称]

 *  ls -a 列出文件下所有文件，包括已‘.’开头的隐藏文件。和“.”“..”.a 代表all    
 *  ls -A 列出除了“.”和“..”以外的文件
 *  ls -l 或ll 列出目录下文件的详细信息  
 *  ls -s 在每个文件的后面打印文件的大小   
 *  ls -S 以文件大小排序显示 
 *  ls -t 按时间排序显示文件  
 *  ls -R [文件名]（recursion递归）将目录下所有子目录的文件都列出来    
 *  ls -d 仅列出目录本身。而不是列出目录下的文件
 *  ls -al 列出当前目录下的所有文件（包含隐藏文件）的详细信息
#### cd (切换目录 change directory) 
* 使用绝对路径切换目录：cd /usr/share/doc
* 使用相对路径切换目录：cd ../man    
#### pwd (显示目前所在目录 print working directory)  
#### mkdir(创建新目录 make directory) 
* mkdir -p  文件名 创建目录时将上级目录一起创建起来  
  例：mkdir -p  test/test1/test2  直接创建三个目录   
* mkdir -m 权限  文件名 创建文件时，直接配置权限 
  例：mkdir -m 711 test2  
#### rmdir (删除空的目录 remove directory) 
* rmdir -p 目录名 连同上一级空的目录一起删除。p :parents
  例：rmdir -p test1/test2/test3  连同test3的上级空目录一起删除  
#### cp (复制文件或目录)  
语法： cp 来源档（source） 目标档（destination）
  
* cp -a 相当于-pdr.pdr说明参考以下（常用）   
  例：想把/tmp/test5里面的文件和文件夹复制到 /tmp/test4  
     cp -a /tmp/test5/* /tmp/test4    
     想把/tmp/test5目录复制到/tmp/test4 下  
     cp -a /tmp/test5 /tmp/test4 (结果：/tmp/test4/test5)
* cp -d 若来源档为连结档的属性（link file ）,则复制连结档属性，而非文件本身  
* cp -f 强制（force）的意思。若目标文件已经存在，且无法打开。则移除后，再尝试一次 
* cp -i 若目标档已经存在时，再覆盖时会先询问动作的进行（常用）
* cp -l 进行硬式连接的连接档创建，而非复制文件本身  
* cp -p 连同文件的属性一起复制过去，而非使用默认属性（备份常用）
* cp -r 递归持续复制，用于目录的复制行为。（常用）
* cp -s 复制成为符号连接档（symbolic link），即【捷径】文件 
* cp -u 若destination 比source 旧。才升级destination

        
          

  
 






