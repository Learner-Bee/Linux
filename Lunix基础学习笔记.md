#Linux教程
##Linux简介
Linux是一套免费使用和自由传播的类Unix系统。是一个基于POSIX和Unix的**多用户、多任务、多线程、多CPU**的操作系统。  
  支持32位和64位硬件  
**Linux VS Windows**   
Linux主要应用在服务器上，而桌面操作是Windows    
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
>1.通过ifconfig获取操作系统的ip地址  
>2.在SecureCRT上新建连接，在connection下新建name，默认选择SSH2（安全外壳协议Secure Shell缩写）。  
>3.在SSH2 下输入hostname (即连接系统的ip地址)，输入登录系统的用户名连接，输入密码即可
##系统启动过程  
###启动过程分五个阶段：  
*内核的引导  
*运行init  
*系统初始化  
*建立终端  
*用户登录系统  
### Linux系统7个运行级别  
*0：系统停机状态，默认不能设为0，否则不能启动  
*1：单用户工作状态，root权限。用于系统维护，禁止远程访问  
*2：多用户状态（没有NFS，Network File System ）  
*3：完全的多用户状态（有NFS）。登录后进入控制台命令行模式  
*4：系统未使用，保留  
*5：X11控制台。登陆后进入图形GUI模式  
*6：系统正常关闭并重启。默认运行级别不能是6，否则不能正常启动   
###Linux关机  
正确的关机流程sync>shutdown>reboot>halt  
关机指令shutdown。可通过man shutdown查看帮助文档   
**给用户添加sudo权限**    
>1.由普通用户进入超级用户模式（即进入root模式）。在普通模式下输入'su-'，然后输入root密码，回车，进入超级用户模式 
>2.输入命令'visudo' 进入编辑模式。（编辑sudo的配置文件/etc/sudoers）
>3.找到'root ALL=(ALL) ALL'(可能当前页找不到，一直回车)在该行下面添加 Lilybo ALL=(ALL) ALL  
>4.保存退出：w(保存)，exit(退出)  

sync 将数据由内存同步到硬盘中（关闭或重启前一定要执行）  
shutdown -h 10 'this server will shutdown after 10mins'  10分钟后系统关机，信息会显示在登录用户的当前屏幕 (h是halt缩写，停止的意思)   
shutdown -h now 立马关机    
halt 关闭系统   等同于上面命令和poweroff  、init0
shutdown -h 20:25 系统会在20:25关机  
shutdown -h +10 十分钟后  
shutdown -r now 系统立马重启（reboot）    
reboot 重启，等同意上面命令、init6
shutdown -r +10 系统1分钟后重启    
##Linux系统目录结构 
**ls和ls /区别**  
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




