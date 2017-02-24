#Linux教程
##Linux简介
Linux是一套免费使用和自由传播的类Unix系统。是一个基于POSIX和Unix的**多用户、多任务、多线程、多CPU**的操作系统。  
  支持32位和64位硬件  
**Linux VS Windows**   
Linux主要应用在服务器上，而桌面操作是Windows    
##Linux安装  
以CentOS 6.4为例  
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
###系统初始化  
在Init的配置文件中有一行：si::syinit:/etc/rc.d/rc.sysinit  它调用执行了etc/rc.d/rc.sysinit ,rc.sysinit是一个bash shell的脚本
