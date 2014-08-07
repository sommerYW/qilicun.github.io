title: "Gnome（Fedora-Linux）下安装LaTex 编辑器"
id: 195
date: 2011-04-08 05:06:00
tags: 
categories: 
- Linux
---


题外话，其实我觉得Gvim写latex 就很不错，当然背景要设置一下：bg=light

下面是gedit的设置

============================================
Fedora 13用户，请先yum install tex-live gedit-plugins
然后yum install gedit-_latex_-plugin就可以了，不需要手动

=============================================
su
yum install gedit-plugins
安装题个默认的插件，包括很重要的代码补齐，括号补齐和内置console
plugin不是自动激活的，需要手工激活
选择
Edit-Perference-Edit

激活后就可以看到console了

接下来需要安装latex插件，默认latex已经安装好了，不管是tetex还是texlive。（就是库文件，我们现在装的都是编辑器）
由于gedit latex插件编译调用了rubber
所以需要
首先su
yum install rubber
然后去http://live.gnome.org/Gedit/LaTeXPlugin 下载latex plugin
一个tar.gz的文件
解压到
~/.gnome2/gedit/plugin 如果没有则创建
得到的目录结果如下：
~./gnome2
/gedit
/plugin
/LaTexPlugin
LatexPlugin.gedit-plugin
安装就完成了。
现在创建一个文件并保存为.tex
gedit俨然成了了gnome版的kile

