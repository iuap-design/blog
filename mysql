#mysql安装


###工具/原料

* mysql-5.6.34-linux-glibc2.5-x86_64.tar.gz

###下载/安装

* 去myqsql官网下载安装包  http://dev.mysql.com/downloads/file/?id=465969

* 进入安装包所在目录，执行命令：tar -zxvf mysql-5.6.34-linux-glibc2.5-x86_64.tar.gz
* 复制解压后的mysql目录到系统的本地软件目录:
执行命令：cp mysql-5.6.34-linux-glibc2.5-x86_64 /usr/local/mysql -r

###安装数据库

* 添加系统mysql组和mysql用户：执行命令：groupadd mysql和useradd -r -g mysql mysql

* 进入安装mysql软件目录：执行命令 cd /usr/local/mysql
修改当前目录拥有者为mysql用户：执行命令 chown -R mysql:mysql ./
* 安装数据库：执行命令 ./scripts/mysql_install_db --user=mysql
* 修改当前目录拥有者为root用户：执行命令 chown -R root:root ./
* 修改当前data目录拥有者为mysql用户：执行命令 chown -R mysql:mysql data
到此数据库安装完毕

###启动数据库

* 启动mysql服务和添加开机启动mysql服务：
添加开机启动：执行命令cp support-files/mysql.server /etc/init.d/mysql，把启动脚本放到开机初始化目录
启动mysql服务：执行命令service mysql start
执行命令：ps -ef|grep mysql 看到mysql服务说明启动成功

###修改数据库密码

* 修改mysql的root用户密码，root初始密码为空的：
执行命令：./bin/mysqladmin -u root password '密码'


