title: "ubuntu texlive 中文支持以及编辑器"
id: 200
date: 2011-04-08 05:10:00
tags: 
categories: 
- Linux
- ubuntu
---

这几天要和别人讨论问题，得把自己的问题和做法写出来，就花了一天多时间专门搞了一个中文tex，不过总算搞好了

首先安装texlive，其实不用安装iso文件，sudo apt-get install texlive*

查看texlive版本以及安装位置:

dpkg -l texlive

dpkg -L texlive

接下来安装中文支持，首先上网下载AdobeFonts 共有四种，宋体，仿宋，楷体，黑体。

解压出来复制到：/usr/share/fonts

然后查看以下：fc-list :lang=zh-cn &gt;&gt; zhcn.txt
看看zhcn中有没有adobe字体：

Adobe 楷体 Std,Adobe Kaiti Std,Adobe Kaiti Std R,Adobe 楷体 Std R:style=R,Regular
Adobe 黑体 Std,Adobe Heiti Std,Adobe Heiti Std R,Adobe 黑体 Std R:style=R,Regular
Adobe 宋体 Std,Adobe Song Std,Adobe Song Std L,Adobe 宋体 Std L:style=L,Regular
Adobe 仿宋 Std,Adobe Fangsong Std,Adobe Fangsong Std R,Adobe 仿宋 Std R:style=R,Regular
如果安装成功就会显示上面的内容。
下面是编辑latex如何使用Adobe字体。按照下面的做法不会出错，字体也很漂亮
documentclass[11pt, a4paper]{article}
usepackage{fontspec}
setmainfont{Adobe Fangsong Std} %这里Fangsong 可以换成Adobe其他三种的任何一种，Song, Heiti,Kaiti
begin{document}
你好，Tex
end{document}
记住最后用 xelatex 进行编译，直接生成的是一个pdf文件，打开看看就知道字体使用对了没有。
之前有篇日志讲如何用gedit编辑latex，最近发现了一个比较好玩的东西，分享一下：gummi
一个所见所得的编辑器，其实就是自己不停的在编译。对于小文档用这个还不错
Ubuntu用户可以通过以下的命令来安装gummi.
<table border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td></td>
<td>
<div>
<div>`sudo apt-add-repository ppa:gummi/gummi
sudo apt-get update`</div>
<div>`sudo apt-get install gummi`</div>
</div></td>
</tr>
</tbody>
</table>
[![](http://lwjmdj.files.wordpress.com/2011/04/http_imgload-cgi.png?w=630&amp;h=354 "gummi效果图")](http://lwjmdj.files.wordpress.com/2011/04/http_imgload-cgi.png)效果如图

gummi从下面看到：

http://ruilinliu.com/blog/2010/11/gummi-a-linux-lightweight-latex-editor/

&nbsp;
