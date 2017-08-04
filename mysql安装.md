一、安装及配置
====
#### 1.安装第三方源，更新
wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm  
<br/>
sudo rpm -ivh mysql-community-release-el7-5.noarch.rpm
<br/>
yum update
#### 2.安装并启动MySQL服务
sudo yum install mysql-server
<br/>
sudo systemctl start mysqld
<br/>
#### 3.运行安全设置
运行以下命令之后程序会对接下来的设置项（3.1-3.5）进行询问。
<br/>
sudo mysql_secure_installation
<br/>
#### 3.1Set root password? [Y/n]
是否为root用户设置密码？
<br/>
默认情况下MySQL中root用户的密码为空，输入Y并回车开始设置root用户的新密码，如无需设置则输入n并回车。
#### 3.2Remove anonymous users? [Y/n]
是否移除匿名用户？
<br/>
安全起见，请移除匿名用户，输入Y并回车。
<br/>
#### 3.3Remove test database and access to it? [Y/n]
是否移除测试数据库及其访问权限？
<br/>
建议移除，输入Y并回车。
<br/>
#### 3.4Disallow root login remotely? [Y/n]
是否禁用root用户的远程访问权限？
<br/>
安全起见，请禁止此权限，输入Y并回车。
<br/>
#### 3.5Reload privilege tables now? [Y/n]
是否重载MySQL权限及配置？
<br/>
如果希望之前修改的内容立即生效则需要重载，输入Y并回车。

