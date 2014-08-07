title: "迭代程序和CG算法程序"
id: 107
date: 2008-11-22 21:57:21
tags: 
categories: 
- Windows Live Space
---


这几周老师总是说要交程序，虽然嘴上说有时间的话就做一做，没有时间的话就算了，可是说着了么长时间，听的都烦，结果周二的时候竟然说了一句，我看看那些人交了，心里有个底……听他这么一说，我心里倒是咯噔了一下，这个老师真阴险……于是这些天一直过的很窝火，总想找个时间把程序了结了，但是一想起来就很心烦，干什么事情都不能集中全力总是想着程序没写心里很不爽.今天呢其实很不爽，早晨起来都1点多了，其实不是睡懒觉，早就醒了，但是就是不想起来，想着起来后也没事情干还不如睡觉，但是睡觉又会觉得很浪费时间，所以总之因此更郁闷……下午去办公室把以前的作业稍微写了一下，六点多就回来准备写程序了.起点开始到现在终于搞定了~一下写了五个程序，感觉很有成就感,当然第一个是参考了别人的编程框架，之后的几个全是自己写的，嘿嘿心里的不爽终于释放了一些.写起来还是比较容易最后又经过了一个多小时的调试，终于完全弄好了~

以下代码在DEVc++中编译通过.

第一个是Jacobi的C 程序：

#include&lt;iostream&gt;
#include&lt;math.h&gt;
#include&lt;stdlib.h&gt;
using namespace std;
const int m=10;
int main()
{

double a[m][m],b[m],e,x0[m],x1[m],w,se,max;
int n,i,j,N,k;
N=10000;e=0.000001;
cout&lt;&lt;"-------------------------------------------------------"&lt;&lt;endl;
cout&lt;&lt;"n请输入方程的个数：";
cin&gt;&gt;n;cout&lt;&lt;endl;
for(i=1;i&lt;=n;i++)
{
cout&lt;&lt;"请输入第"&lt;&lt;i&lt;&lt;"个方程的各项系数：";
for(j=1;j&lt;=n;j++)
cin&gt;&gt;a[i][j];
}
cout&lt;&lt;"n请输入各个方程等号右边的常数项:n";
for(i=1;i&lt;=n;i++)
{
cin&gt;&gt;b[i];
}
for(i=1;i&lt;=n;i++)
{
x0[i]=0;
x1[i]=x0[i];
}
for(k=1;k&lt;=N;k++)
{
for(i=1;i&lt;=n;i++)      //求x(k+1)
{
w=0;
for(j=1;j&lt;=n;j++)
{
if(j!=i)
w=w+a[i][j]*x0[j];
}
x1[i]=(b[i]-w)/double(a[i][i]);
}

max=fabs(x0[1]-x1[1]);       //求残量范数 ||x(k+1)-x(k)||/||x(k+1)||;
for(i=1;i&lt;=n;i++)
{
se=fabs(x0[i]-x1[i]);
if(se&gt;max)
max=se;
}
if(max&lt;e)              //判断迭代是否收敛
{
cout&lt;&lt;endl;
for(i=1;i&lt;=n;i++)
cout&lt;&lt;"x"&lt;&lt;i&lt;&lt;"="&lt;&lt;x1[i]&lt;&lt;endl;
cout&lt;&lt;endl;
cout&lt;&lt;"迭代次数"&lt;&lt;":"&lt;&lt;k;
break;
}
for(i=1;i&lt;=n;i++)     //赋值，重新计算
{
x0[i]=x1[i];
}
}
if(k==N)
cout&lt;&lt;"迭代失败！！"&lt;&lt;endl;
cout&lt;&lt;endl;
cout&lt;&lt;"-------------------------------------------------------"&lt;&lt;endl;
cout&lt;&lt;endl;
system("pause");
return 0;
}

第二个是Gauss-seidel的C程序：

#include&lt;iostream&gt;
#include&lt;math.h&gt;
#include&lt;stdlib.h&gt;
using namespace std;
const int m=10;
int main()
{

double a[m][m],b[m],e,x0[m],x1[m],w1,w2,se,max1,max2,max;
int n,i,j,N,k;
N=10000;e=0.000001;
cout&lt;&lt;"-------------------------------------------------------"&lt;&lt;endl;
cout&lt;&lt;"n请输入方程的个数：";
cin&gt;&gt;n;cout&lt;&lt;endl;
for(i=1;i&lt;=n;i++)
{
cout&lt;&lt;"请输入第"&lt;&lt;i&lt;&lt;"个方程的各项系数：";
for(j=1;j&lt;=n;j++)
cin&gt;&gt;a[i][j];
}
cout&lt;&lt;"n请输入各个方程等号右边的常数项:n";
for(i=1;i&lt;=n;i++)
{
cin&gt;&gt;b[i];
}
for(i=1;i&lt;=n;i++)
{
x0[i]=0;
x1[i]=x0[i];
}
for(k=1;k&lt;=N;k++)
{
for(i=1;i&lt;=n;i++)      //求x(k+1)
{
w1=0;
for(j=i+1;j&lt;=n;j++)
{
w1=w1+a[i][j]*x0[j];
}
w2=0;
for(j=1;j&lt;=i-1;j++)
{
w2=w2+a[i][j]*x1[j];
}
x1[i]=(b[i]-w1-w2)/double(a[i][i]);
}

max1=fabs(x0[1]-x1[1]);       //求残量范数 ||x(k+1)-x(k)||/||x(k+1)||;
for(i=1;i&lt;=n;i++)
{
se=fabs(x0[i]-x1[i]);
if(se&gt;max1)
max1=se;
}
if(max1&lt;e)              //判断迭代是否收敛
{
cout&lt;&lt;endl;
for(i=1;i&lt;=n;i++)
cout&lt;&lt;"x"&lt;&lt;i&lt;&lt;"="&lt;&lt;x1[i]&lt;&lt;endl;
cout&lt;&lt;endl;
cout&lt;&lt;"迭代次数"&lt;&lt;":"&lt;&lt;k;
break;
}
for(i=1;i&lt;=n;i++)     //赋值，重新计算
{
x0[i]=x1[i];
}
}
if(k==N)
cout&lt;&lt;"迭代失败！！"&lt;&lt;endl;
cout&lt;&lt;endl;
cout&lt;&lt;"-------------------------------------------------------"&lt;&lt;endl;
cout&lt;&lt;endl;
system("pause");
return 0;
}

第三个是SOR的C程序：

#include&lt;iostream&gt;
#include&lt;math.h&gt;
#include&lt;stdlib.h&gt;
using namespace std;
const int m=10;
int main()
{

double a[m][m],b[m],e,x0[m],x1[m],w,w1,w2,se,max1,max2,max;
int n,i,j,N,k;
N=10000;e=0.000001;
cout&lt;&lt;"-------------------------------------------------------"&lt;&lt;endl;
cout&lt;&lt;"n请输入方程的个数：";
cin&gt;&gt;n;cout&lt;&lt;endl;
for(i=1;i&lt;=n;i++)
{
cout&lt;&lt;"请输入第"&lt;&lt;i&lt;&lt;"个方程的各项系数：";
for(j=1;j&lt;=n;j++)
cin&gt;&gt;a[i][j];
}
cout&lt;&lt;"n请输入各个方程等号右边的常数项:n";
for(i=1;i&lt;=n;i++)
{
cin&gt;&gt;b[i];
}
cout&lt;&lt;"n请输入松弛因子w：";
cin&gt;&gt;w;
for(i=1;i&lt;=n;i++)
{
x0[i]=0;
x1[i]=x0[i];
}
for(k=1;k&lt;=N;k++)
{
for(i=1;i&lt;=n;i++)      //求x(k+1)
{
w1=0;
for(j=i+1;j&lt;=n;j++)
{
w1=w1+a[i][j]*x0[j];
}
w2=0;
for(j=1;j&lt;=i-1;j++)
{
w2=w2+a[i][j]*x1[j];
}
x1[i]=(1-w)*x0[i]+w*(b[i]-w1-w2)/double(a[i][i]);
}

max1=fabs(x0[1]-x1[1]);       //求残量范数 ||x(k+1)-x(k)||/||x(k+1)||;
for(i=1;i&lt;=n;i++)
{
se=fabs(x0[i]-x1[i]);
if(se&gt;max1)
max1=se;
}
if(max1&lt;e)              //判断迭代是否收敛
{
cout&lt;&lt;endl;
for(i=1;i&lt;=n;i++)
cout&lt;&lt;"x"&lt;&lt;i&lt;&lt;"="&lt;&lt;x1[i]&lt;&lt;endl;
cout&lt;&lt;endl;
cout&lt;&lt;"迭代次数"&lt;&lt;":"&lt;&lt;k;
break;
}
for(i=1;i&lt;=n;i++)     //赋值，重新计算
{
x0[i]=x1[i];
}
}
if(k==N)
cout&lt;&lt;"迭代失败！！"&lt;&lt;endl;
cout&lt;&lt;endl;
cout&lt;&lt;"-------------------------------------------------------"&lt;&lt;endl;
cout&lt;&lt;endl;
system("pause");
return 0;
}

第四个是SSOR的C程序：

#include&lt;iostream&gt;
#include&lt;math.h&gt;
#include&lt;stdlib.h&gt;
using namespace std;
const int m=10;
int main()
{

double a[m][m],b[m],e,x0[m],x1[m],x2[m],w,w1,w2,se,max1,max2,max;
int n,i,j,N,k;
N=10000;e=0.000001;
cout&lt;&lt;"-------------------------------------------------------"&lt;&lt;endl;
cout&lt;&lt;"n请输入方程的个数：";
cin&gt;&gt;n;cout&lt;&lt;endl;
for(i=1;i&lt;=n;i++)
{
cout&lt;&lt;"请输入第"&lt;&lt;i&lt;&lt;"个方程的各项系数：";
for(j=1;j&lt;=n;j++)
cin&gt;&gt;a[i][j];
}
cout&lt;&lt;"n请输入各个方程等号右边的常数项:n";
for(i=1;i&lt;=n;i++)
{
cin&gt;&gt;b[i];
}
cout&lt;&lt;"n请输入松弛因子w：";
cin&gt;&gt;w;
for(i=1;i&lt;=n;i++)
{
x0[i]=0;
x1[i]=x0[i];
x2[i]=x0[i];
}
for(k=1;k&lt;=N;k++)
{
for(i=1;i&lt;=n;i++)      //求x(k+1)
{
w1=0;
for(j=i+1;j&lt;=n;j++)
{
w1=w1+a[i][j]*x0[j];
}
w2=0;
for(j=1;j&lt;=i-1;j++)
{
w2=w2+a[i][j]*x2[j];
}
x2[i]=(1-w)*x0[i]+w*(b[i]-w1-w2)/double(a[i][i]);
w1=0;
for(j=i+1;j&lt;=n;j++)
{
w1=w1+a[i][j]*x2[j];
}
w2=0;
for(j=1;j&lt;=i-1;j++)
{
w2=w2+a[i][j]*x1[j];
}
x1[i]=(1-w)*x2[i]+w*(b[i]-w1-w2)/double(a[i][i]);
}

max1=fabs(x0[1]-x1[1]);       //求残量范数 ||x(k+1)-x(k)||/||x(k+1)||;
for(i=1;i&lt;=n;i++)
{
se=fabs(x0[i]-x1[i]);
if(se&gt;max1)
max1=se;
}
if(max1&lt;e)              //判断迭代是否收敛
{
cout&lt;&lt;endl;
for(i=1;i&lt;=n;i++)
cout&lt;&lt;"x"&lt;&lt;i&lt;&lt;"="&lt;&lt;x1[i]&lt;&lt;endl;
cout&lt;&lt;endl;
cout&lt;&lt;"迭代次数"&lt;&lt;":"&lt;&lt;k;
break;
}
for(i=1;i&lt;=n;i++)     //赋值，重新计算
{
x0[i]=x1[i];
}
}
if(k==N)
cout&lt;&lt;"迭代失败！！"&lt;&lt;endl;
cout&lt;&lt;endl;
cout&lt;&lt;"-------------------------------------------------------"&lt;&lt;endl;
cout&lt;&lt;endl;
system("pause");
return 0;
}

最后一个是CG算法的C程序：

#include&lt;iostream&gt;
#include&lt;math.h&gt;
#include&lt;stdlib.h&gt;
using namespace std;
const int m=10;
int main()
{

double a[m][m],b[m],alfa,beta,p[m],rou1,rou2,e,c,x[m],r[m],w,se,max;
int n,i,j,N,k;
N=10000;e=0.000001;
cout&lt;&lt;"-------------------------------------------------------"&lt;&lt;endl;
cout&lt;&lt;"n请输入方程的个数：";
cin&gt;&gt;n;cout&lt;&lt;endl;
for(i=1;i&lt;=n;i++)
{
cout&lt;&lt;"请输入第"&lt;&lt;i&lt;&lt;"个方程的各项系数：";
for(j=1;j&lt;=n;j++)
cin&gt;&gt;a[i][j];
}
cout&lt;&lt;"n请输入各个方程等号右边的常数项：n";
for(i=1;i&lt;=n;i++)
{
cin&gt;&gt;b[i];
}
cout&lt;&lt;"n请输入x的初始值：取（0，0，0）迭代效果比较好n";
for(i=1;i&lt;=n;i++)
{
cin&gt;&gt;x[i];
}
for(i=1;i&lt;=n;i++)      //计算r0
{
for(j=1;j&lt;=n;j++)
{
r[i]=b[i]-a[i][j]*x[j];
}
}
max=fabs(r[1]);
for(i=1;i&lt;=n;i++)
{
se=fabs(r[i]);
if(se&gt;max)
max=se;
}
if(max&lt;e)
{
for(i=1;i&lt;=n;i++)
cout&lt;&lt;"x"&lt;&lt;i&lt;&lt;"="&lt;&lt;x[i]&lt;&lt;endl;
cout&lt;&lt;endl;
}
else
{
rou1=0;
for(i=1;i&lt;=n;i++)
{
p[i]=r[i];
rou1=rou1+r[i]*r[i];
}
}
for(k=1;k&lt;=N;k++)         //迭代
{
c=0;
for(i=1;i&lt;=n;i++)
{
for(j=1;j&lt;=n;j++)
{
c=c+p[i]*a[i][j]*p[j];
}
}
alfa=rou1/c;
for(i=1;i&lt;=n;i++)
{
x[i]=x[i]+alfa*p[i];
}
for(i=1;i&lt;=n;i++)
{
for(j=1;j&lt;=n;j++)
{
r[i]=r[i]-alfa*a[i][j]*p[j];
}
}
rou2=0;
for(i=1;i&lt;=n;i++)
{
rou2=rou2+r[i]*r[i];
}
beta=rou2/rou1;
for(i=1;i&lt;=n;i++)
{
p[i]=r[i]+beta*p[i];
}
rou1=rou2;
max=fabs(r[1]);
for(i=1;i&lt;=n;i++)
{
se=fabs(r[i]);
if(se&gt;max)
max=se;
}
if(max&lt;e)              //判断迭代是否收敛
{
cout&lt;&lt;endl;
for(i=1;i&lt;=n;i++)
cout&lt;&lt;"x"&lt;&lt;i&lt;&lt;"="&lt;&lt;x[i]&lt;&lt;endl;
cout&lt;&lt;endl;
cout&lt;&lt;"迭代次数"&lt;&lt;":"&lt;&lt;k&lt;&lt;endl;
break;
}
}
system("pause");
return 0;
}

Comments
