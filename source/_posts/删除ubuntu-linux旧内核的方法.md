title: "删除Ubuntu Linux旧内核的方法"
id: 204
date: 2011-04-13 03:42:25
tags: 
- grub.cfg
- ubuntu
- 内核
categories: 
- Linux
---

首先就是使用如下命令，列出所有安装的内核，下表中，带有image的就是内核文件。
dpkg --get-selections|grep linux

然后用
 sudo apt-get remove linux-image-2.6.24-16-generic

&nbsp; &nbsp; &nbsp; &nbsp; sudo apt-get remove linux-headers-2.6.24-16-generic

这样就可以实现自动删除内核文件了，还可以释放磁盘空间。
最后 用一条记录命令

&nbsp;&nbsp; uname -a

注意，新版本的ubuntu不用修改/boot/grub/grup.cfg文件来设置启动项，上面的命令已经自动移除了，自己可以查看以下grub.cfg文件看看是否已经没有删除过的内核文件。

enjoy！
