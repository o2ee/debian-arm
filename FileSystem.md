# debian-arm

安装bootstrap，这是一个Debian提供的工具，可以用来自定义安装系统，也可以用来生成指定构架的文件系统：
1	aptitude install bootstrap
在工作目录下创建文件夹：
1	mkdir fs_debian_mini
下载基本文件系统：
1	sudo debootstrap --arch=armel --foreign squeeze fs_debian_mini/ http://ftp.us.debian.org/debian
根据网速不同大约要30分钟左右；

1	echo "proc /proc proc none 0 0" >> fs_debian_mini/etc/fstab 
2	echo "tiny210" > fs_debian_mini/etc/hostname 
3	mkdir -p fs_debian_mini/usr/share/man/man1/ 
4	mknod fs_debian_mini/dev/console c 5 1
最后面一步可能会提示已存在，不用管。
启动Minitools，在kernel Commandline一项填写： 
1	console=ttySAC0 init=/bin/sh root=/dev/nfs nfsroot=192.168.86.240:/root/fs/fs_emdebian_mini ip=192.168.86.241:192.168.86.240:192.168.86.253:255.255.255.0:debian:eth0:off
其中nfsroot为开发主机的地址，ip依次为：开发板临时IP：开发主机地址：网关：掩码：主机hostname：网卡设备：off，根据自己的情况修改。
参考Tiny210用户手册上的介绍，完成以下工作，连接好开发板的串口并上电：  
