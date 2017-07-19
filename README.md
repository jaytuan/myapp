阿里云搞事情
====
### 服务器安装node.js

#### 1.安装必要的make以及gcc,gcc-c++编译器
 $ yum -y install make gcc gcc-c++
#### 2.获取源码
 $ wget wget -c https://nodejs.org/dist/v6.10.3/node-v6.10.3.tar.gz
#### 3.解压源码
 $ tar -zxvf node-v6.10.3.tar.gz
#### 4.进行编译及安装
$ cd node-v0.8.14
<br/>
$ ./configure
<br/>
$ make && make install
#### 5.检查是否安装成功
$ node -v
<br/>
显示node版本号即为安装成功
====
### centos7服务器安装mongodb

#### 1.新建downloadTools文件夹供下载文件使用
$ mkdir -p downloadTools
#### 2.进入到该文件夹
$ cd downloadTools
#### 3.下载与CentOS 系统匹配的 mongodb-linux-x86_64-rhel70-3.2.4.tgz 文件：
$ wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-3.2.4.tgz
#### 4.解压缩
$ tar -zxvf mongodb-linux-x86_64-rhel70-3.2.4.tgz
#### 5.重命名 mongodb-linux-x86_64-rhel70-3.2.4 文件为 mongodb3.2.4：
$ mv mongodb-linux-x86_64-rhel70-3.2.4 mongodb3.2.4
#### 6.返回到上一级目录，并创建 mongodb 目录：
$ cd ../
<br/>
$ mkdir -p mongodb
#### 7.将 mongodb3.2.4 文件从 /usr/local/downloadTools 目录中移动到 /usr/local/mongodb 目录中：
$ mv downloadTools/mongodb3.2.4/ mongodb/
#### 8. 进入到 /usr/local/mongodb/mongodb3.2.4 目录中：
$ cd mongodb/mongodb3.2.4
#### 9. 在 /usr/local/mongodb/mongodb3.2.4/bin/ 目录中创建一个存放日志的目录：
$ mkdir -p data/test/logs
#### 10.在 /usr/local/mongodb/mongodb3.2.4/bin/ 目录中创建一个存放数据文件的目录：
$ mkdir -p data/test/db
#### 11.进入 bin 目录中：
$ cd bin/
#### 12. 创建配置文件 mongodb.conf：
$ vi mongodb.conf
#### 13.在 mongodb.conf 写入如下内容：
 #idae - MongoDB config start - 2016-05-02
<br/>
#设置数据文件的存放目录
<br/>
dbpath = /usr/local/mongodb/mongodb3.2.4/bin/data/test/db
<br/>
#设置日志文件的存放目录及其日志文件名
<br/>
logpath = /usr/local/mongodb/mongodb3.2.4/bin/data/test/logs/mongodb.log
<br/>
#设置端口号（默认的端口号是 27017）
<br/>
port = 27017
<br/>
#设置为以守护进程的方式运行，即在后台运行
<br/>
fork = true
<br/>
#nohttpinterface = true
<br/>
nohttpinterface = true
<br/>
#idae - MongoDB config end - 2016-05-02
<br/>
按英文状态下的“:wq”保存并退出；
<br/>
参数解释:<p>
--dbpath 数据库路径(数据文件)
--logpath 日志文件路径
--master 指定为主机器
--slave 指定为从机器
--source 指定主机器的IP地址
--pologSize 指定日志文件大小不超过64M.因为resync是非常操作量大且耗时，最好通过设置一个足够大的oplogSize来避免resync(默认的 oplog大小是空闲磁盘大小的5%)。
--logappend 日志文件末尾添加，即使用追加的方式写日志
--journal 启用日志
--port 启用端口号
--fork 在后台运行
--only 指定只复制哪一个数据库
--slavedelay 指从复制检测的时间间隔
--auth 是否需要验证权限登录(用户名和密码)
--syncdelay 数据写入硬盘的时间（秒），0是不等待，直接写入
--notablescan 不允许表扫描
--maxConns 最大的并发连接数，默认2000  
--pidfilepath 指定进程文件，不指定则不产生进程文件
--bind_ip 绑定IP，绑定后只能绑定的IP访问服务</p>
