title: "linux中qq崩溃解决办法"
id: 212
date: 2011-04-08 05:08:37
tags: 
- linux
- qq
categories: 
- Linux学习
---

linux中qq崩溃解决办法
/usr/bin/qq 在第二行加入：export GDK_NATIVE_WINDOWS=true
#！ /bin/sh
export GDK_NATIVE_WINDOWS=true
cd /usr/share/tencent/qq/
./qq

