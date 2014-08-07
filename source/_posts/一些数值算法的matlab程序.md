title: "一些数值算法的matlab程序"
id: 109
date: 2008-11-22 22:12:58
tags: 
categories: 
- Windows Live Space
---


刚才整理电脑发现大学时候写的一些matlab程序，和我刚才写的那些C程序是相对的，因此一并发上来.大学的时候老师说最好用C或者fortran写，当时很纳闷，为什么不提倡用matlab？还极力给老师建议用matlab.等上了研究生第一次写数值代数的程序时也用的matlab，但是那个老师上课的时候还点名说了一次：以后不准用matlab！最后上讨论班的时候小师兄说他写的有限元程序要处理一个几十万的矩阵，用matlab处理起来很慢，在所里的机群上跑起来都很慢，最后改用C了.这样我才算有点明白，不过matlab对于初学者来说写起代码来还是很方便的.下面的代码我都运行过没有什么大问题.

第一个Jacobi的M程序：

function x=Jacobi(A,b,x0,e,N)
%x0为初始值,e为误差限,N为迭代次数
n=length(b);
x=x0;
x0=x+2*e;
k=0;D=diag(diag(A));iAl=inv(D);
J=-iAl*(A-D);
f=iAl*b;
while   norm(x0-x,inf)&gt;e&amp;k&lt;N
k=k+1;
x0=x;
x=J*x0+f;
disp(x');
end
disp('迭代次数')
disp(k)
if  k==N
warning('已达迭代次数上限');
end

第二个Gauss-seidel的M程序:

function x=GS(A,b,x0,e,N)
%x0为初始值,e为误差限,N为迭代次数
n=length(b);
x=x0;
x0=x+2*e;
k=0;Al=tril(A);iAl=inv(Al);
G=-iAl*(A-Al);f=iAl*b;
while   norm(x0-x,inf)&gt;e&amp;k&lt;N
k=k+1;
x0=x;
x=G*x0+f;
disp(x');
end
disp('迭代次数')
disp(k)
if  k==N
warning('已达迭代次数上限');
end

第三个SOR的M程序：

function x=SOR(A,b,w,x0,e,N)
%x0为初始值,e为误差限,N为迭代次数
n=length(b);
x=x0;
x0=x+2*e;
k=0;L=tril(A,-1);U=triu(A,1);
while   norm(x0-x,inf)&gt;e&amp;k&lt;N
k=k+1;x0=x;
for i=1:n
x1(i)=(b(i)-L(i,1:i-1)*x(1:i-1,1)-U(i,i+1:n)*x0(i+1:n,1))/A(i,i);
x(i)=(1-w)*x0(i)+w*x1(i);
end
disp('迭代次数')
disp(k)
disp(x')
end
if  k==N
warning('已达迭代次数上限');
end

第四个加权数值法的M程序：

function x=shuzhi(A,b,a,e,N,x0)
%e为误差限,N为迭代次数,a为参数,x0为初始值
n=length(b);
x1=(A+a*eye)(b+a*x0);
r=b-A*x1;
d=(A+a*eye)r;
x=x1+d;
k=0;
while   norm(d)/norm(x)&gt;e&amp;k&lt;N
k=k+1;
x1=x;
r=b-A*x1;
d=(A+a*eye)r;
x=x1+d;
disp('残差  r')
disp(r)
end
disp('迭代次数')
disp(k)
if  k==N
warning('超过最大迭代次数')
end

第五个迭代校正法解线性方程组的M程序：

function x=jiaozheng(A,b,e,N)
%e为误差限,N为迭代次数
x1=Ab;
r=b-A*x1;
d=Ar;
x=x1+d;
k=0;
while   (norm(d)/norm(x))&gt;e&amp;k&lt;N
k=k+1;
x1=x;
r=b-A*x1;
d=Ar;
x=x1+d;
disp('残差   r')
disp(r)
end
disp('迭代次数')
disp(k)
if  k==N
warning('超出最大迭代次数')
end

第六个Gauss消去法：

function x=Gauss(A,b,flag)
if  nargin&lt;3
flag=0;
end
n=length(b);
A=[A b];
%消元
for k=1:n-1;
A(k+1:n,k+1:n+1)=A(k+1:n,k+1:n+1)-A(k+1:n,k)/A(k,k)*A(k,k+1:n+1);
if  flag==0
disp('增广矩阵的变换次数及形式')
disp(k)
disp(A);
end
end
%回代
x=zeros(n,1);
x(n)=A(n,n+1)/A(n,n);
for i=n-1:-1:1
x(i)=(A(i,n+1)-A(i,i+1:n)*x(i+1:n))/A(i,i);
end

第七个LU分解法的M程序：

function [L,U,x]=LU(A,b)
%A和b满足 Ax=b;
n=length(A);
U=zeros(n,n);
L=eye(n,n);
U(1,:)=A(1,:);
L(2:n,1)=A(2:n,1)/U(1,1);
for k=2:n
U(k,k:n)=A(k,k:n)-L(k,1:k-1)*U(1:k-1,k:n);
L(k+1:n,k)=(A(k+1:n,k)-L(k+1:n,1:k-1)*U(1:k-1,k))/U(k,k);
end
%回代求解  Ly=b
y=zeros(n,1);
y(1)=b(1);
for i=2:n
y(i)=b(i)-L(i,1:i-1)*y(1:i-1);
end
%回代求解 Ux=y
x=zeros(n,1);
x(n)=y(n)/U(n,n);
for i=n-1:-1:1
x(i)=(y(i)-U(i,i+1:n)*x(i+1:n))/U(i,i);
end

第八个列主元的Gauss消去法：

function x=Gauss2(A,b)
%A和b满足 Ax=b;
n=length(b);
A=[A,b];
for k=1:n-1;
%选主元
[ap,p]=max(abs(A(k:n,k)));
p=p+k-1;
if  p&gt;k
t=A(k,:);A(k,:)=A(p,:);A(p,:)=t;
end
%消元
A(k+1:n,k+1:n+1)=A(k+1:n,k+1:n+1)-A(k+1:n,k)/A(k,k)*A(k,k+1:n+1);
% disp(A);
end
%回代
x=zeros(n,1);
x(n)=A(n,n+1)/A(n,n);
for i=n-1:-1:1
x(i)=(A(i,n+1)-A(i,i+1:n)*x(i+1:n))/A(i,i);
end

第九个追赶法的M程序：

function x=zhuigan(A,b)
%A和b满足 Ax=b;
n=length(b);
c=zeros(n,1);
d=zeros(n,1);
c(1)=A(1,1);  d(1)=A(1,2)/A(1,1);
for i=2:n-1
c(i)=A(i,i)-A(i,i-1)*d(i-1);
d(i)=A(i,i+1)/c(i);
end
c(n)=A(n,n)-A(n,n-1)*d(n-1);
%回代求解  Ly=b
y=zeros(n,1);
y(1)=b(1)/A(1,1);
for i=2:n
y(i)=(b(i)-A(i,i-1)*y(i-1))/c(i);
end
%回代求解 Ux=y
x=zeros(n,1);
x(n)=y(n);
for i=n-1:-1:1
x(i)=y(i)-d(i)*x(i+1);
end

第十个cholesky分解法的M程序：

function L=cholesky(A)
n=size(A);
L=zeros(n,n);
L(1,1)=sqrt(A(1,1));
for i=2:1:n
L(i,1)=A(i,1)/L(1,1);
end
for j=2:1:n
sum1=0;
for k=1:1:j-1
sum1=sum1+L(j,k)^2;
end
L(j,j)=sqrt(A(j,j)-sum1);
for i=j+1:1:n;
sum2=0;
for k=1:1:j-1
sum2=sum2+L(i,k)*L(j,k);
end
L(i,j)=(A(i,j)-sum2)/L(j,j);
end
end

Comments
