CentOS7的yum源中默认好像是没有mysql的。为了解决这个问题，我们要先下载mysql的repo源。
1. 下载mysql的repo源
$ wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
2. 安装mysql-community-release-el7-5.noarch.rpm包
$ sudo rpm -ivh mysql-community-release-el7-5.noarch.rpm
安装这个包后，会获得两个mysql的yum repo源：/etc/yum.repos.d/mysql-community.repo，/etc/yum.repos.d/mysql-community-source.repo。
3. 安装mysql
$ sudo yum install mysql-server
根据步骤安装就可以了，不过安装完成后，没有密码，需要重置密码。
4. 重置密码
重置密码前，首先要登录
$ mysql -u root
登录时有可能报这样的错：ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/lib/mysql/mysql.sock' (2)，原因是/var/lib/mysql的访问权限问题。下面的命令把/var/lib/mysql的拥有者改为当前用户：
$ sudo chown -R openscanner:openscanner /var/lib/mysql
然后，重启服务：
$ service mysqld restart
（需将目录换到拥有者或者跟重启防火墙一样试试）
接下来登录重置密码：
$ mysql -u root
mysql > use mysql;
mysql > update user set password=password('123456') where user='root';
mysql > exit;
5. 开放3306端口
$ sudo vim /etc/sysconfig/iptables
添加以下内容：
-A INPUT -p tcp -m state --state NEW -m tcp --dport 3306 -j ACCEPT
保存后重启防火墙：
$ systemctl restart firewalld.service
6. 创建普通用户并授权
示例（使用root用户登录，并假定已经创建了openscannerstore数据库）：
mysql > use mysql;
＃创建openscanner用户与密码并设置为从安装mysql服务的机器本地访问
mysql > grant all on openscannerstore.* to 'openscanner'@'localhost' 
            identified by 'scanner888';
#设置openscanner用户与密码，并从任何机器都可以访问mysql
mysql > grant all on openscannerstore.* to 'openscanner'@'%' identified by 'scanner888';
mysql > flush privileges;            #刷新才会生效
现在就可以从客户机连接mysql服务器了，如果连接报这样的错：ERROR 2003 (HY000): Can't connect to MySQL server on '192.168.x.xxx' (113)。因为我们是centos7，请先确认防火墙是否开启来，centos7默认是firewall，我们可以把它停止并禁止使用，然后启动我们熟悉的iptables，这样就好了！
注：mysql客户机是需要安装mysql客户端的。
