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
$ cd node-v6.10.3
<br/>
$ ./configure
<br/>
$ make && make install
#### 5.检查是否安装成功
$ node -v
<br/>
显示node版本号即为安装成功
<br/>
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
$ cd mongodb/mongodb3.2.4/bin
#### 9. 在 /usr/local/mongodb/mongodb3.2.4/bin/ 目录中创建一个存放日志的目录：
$ mkdir -p data/test/logs
#### 10.在 /usr/local/mongodb/mongodb3.2.4/bin/ 目录中创建一个存放数据文件的目录：
$ mkdir -p data/test/db
#### 11. 创建配置文件 mongodb.conf：
$ vi mongodb.conf
#### 12.在 mongodb.conf 写入如下内容：
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
参数解释:
<br/>
--dbpath 数据库路径(数据文件)
<br/>
--logpath 日志文件路径<br/>
--master 指定为主机器<br/>
--slave 指定为从机器<br/>
--source 指定主机器的IP地址<br/>
--pologSize 指定日志文件大小不超过64M.因为resync是非常操作量大且耗时，最好通过设置一个足够大的oplogSize来避免resync(默认的 oplog大小是空闲磁盘大小的5%)。<br/>
--logappend 日志文件末尾添加，即使用追加的方式写日志<br/>
--journal 启用日志<br/>
--port 启用端口号<br/>
--fork 在后台运行<br/>
--only 指定只复制哪一个数据库<br/>
--slavedelay 指从复制检测的时间间隔<br/>
--auth 是否需要验证权限登录(用户名和密码)<br/>
--syncdelay 数据写入硬盘的时间（秒），0是不等待，直接写入<br/>
--notablescan 不允许表扫描<br/>
--maxConns 最大的并发连接数，默认2000<br/>  
--pidfilepath 指定进程文件，不指定则不产生进程文件<br/>
--bind_ip 绑定IP，绑定后只能绑定的IP访问服务
#### 13.启动 mongodb 服务：
##### 13.1 以自定义的 mongodb 配置文件方式启动：
$ ./mongod --config mongodb.conf
##### 13.2 以修复模式启动 mongodb：
$ ./mongod --repair -f mongodb.conf
##### 13.3 以参数式启动：
$ ./mongod /usr/local/mongodb/mongodb3.2.4/bin/mongod --dbpath=/usr/local/mongodb/mongodb3.2.4/bin/data/test/db --logpath=/usr/local/mongodb/mongodb3.2.4/bin/data/test/logs/mongodb.log --fork
<br/>
如果报如下错误：<br/>
  ERROR: child process failed, exited with error number 1<br/>
很可能是 mongodb.conf 中配置的路径不一致问题；<br/>
如果报如下错误：<br/>
  ERROR: child process failed, exited with error number 100<br/>
很可能是没有正常关闭导致的，那么可以删除 mongod.lock 文件<br/>

#### 14.查看 mongodb 进程：
$ ps aux |grep mongodb

#### 15.查看 mongodb 服务的运行日志：
$ tail -200f /usr/local/mongodb/mongodb3.2.4/bin/data/test/logs/mongodb.log

#### 16.检查端口是否已被启动：
$ netstat -lanp | grep 27017

#### 17.杀死 mongodb 进程，即可关闭 mongodb 服务：
$ kill -15 PID<br/>
//PID 可以通过步骤 16 查看到
