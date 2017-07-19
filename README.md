阿里云搞事情
====
### 服务器安装node.js

#### 1.安装必要的make以及gcc,gcc-c++编译器
 yum -y install make gcc gcc-c++
#### 2.获取源码
 wget wget -c https://nodejs.org/dist/v6.10.3/node-v6.10.3.tar.gz
#### 3.解压源码
 tar -zxvf node-v6.10.3.tar.gz
#### 4.进行编译及安装
cd node-v0.8.14
<br/>
./configure
<br/>
make && make install
#### 5.检查是否安装成功
node -v
