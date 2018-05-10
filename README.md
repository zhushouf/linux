## Linux

1，安装JDK
	
	（1）下载
		http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
		
		jdk-8u171-linux-x64.rpm
	
	（2）安装
		cd /usr/local/download
		rpm -ivh jdk-8u171-linux-x64.rpm
		默认安装路径：/usr/java
	
	（4）检查
		java -version
	
	（5）配置环境变量
		vi /etc/profile
		
		在最后面增加：
		export JAVA_HOME=/usr/java/jdk1.8.0_171-amd64
		export JRE_HOME=/usr/java/jdk1.8.0_171-amd64/jre
		export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib:$CLASSPATH
		export PATH=$JAVA_HOME/bin:$JRE_HOME/bin:$PATH
	
2，安装Tomcat

	（1）下载
		https://tomcat.apache.org/download-80.cgi
		http://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-8/v8.0.51/bin/apache-tomcat-8.0.51.tar.gz
		
		apache-tomcat-8.0.51.tar.gz
		
	（2）安装
		cd /usr/local/download
		tar -tzvf apache-tomcat-8.0.51.tar.gz
		tar -xzvf apache-tomcat-8.0.51.tar.gz -C /usr/local/
		
		cd /usr/local
		mv apache-tomcat-8.0.51/ tomcat
		
	（3）启动
		cd /usr/local/tomcat/bin
		sh start.sh
		
	（4）访问服务
		http://192.168.0.122:8080
	
	（5）防火墙
		防火墙即时生效，重启后失效
		查询，service iptables status
		开启，service iptables start
		关闭，service iptables stop
		
		vi /etc/sysconfig/iptables
		# -A INPUT -p tcp -m state --state NEW -m tcp --dport 3306 -j ACCEPT
		# -A INPUT -p tcp -m state --state NEW -m tcp --dport 6379 -j ACCEPT
		# -A INPUT -p tcp -m state --state NEW -m tcp --dport 8080 -j ACCEPT
		
3，安装MySQL

	（1）下载
		https://dev.mysql.com/downloads/mysql/5.6.html#downloads
		
		MySQL-5.6.40-1.el6.x86_64.rpm-bundle.tar
	
	（2）安装
		cd /usr/local/download
		tar -tvf MySQL-5.6.40-1.el6.x86_64.rpm-bundle.tar
		tar -xvf MySQL-5.6.40-1.el6.x86_64.rpm-bundle.tar
		
		yum install perl
		yum install numactl
		
		rpm -ivh MySQL-devel-5.6.40-1.el6.x86_64.rpm
		rpm -ivh MySQL-server-5.6.40-1.el6.x86_64.rpm
		rpm -ivh MySQL-client-5.6.40-1.el6.x86_64.rpm
		
	（3）启动服务
		/etc/init.d/mysql start
		查看进程：ps -ef|grep mysqld
			
	（4）查看密码
		vi /root/.mysql_secret
		2rnR0kL56ypsg8QP

		修改密码
		mysql -u root -p;
		mysql> use mysql;
		mysql> grant all privileges on *.* to 'root'@'%' identified by '123456' with grant option;
		mysql> select * from user;
		mysql> flush privileges;
	
	（5）使用客户端连接
		Navicat Premium
		
	（6）创建数据库，导入数据
		
	
4，安装Redis

	（1）下载
		http://download.redis.io/releases/
		
		redis-4.0.0.tar.gz
	
	（2）安装
		cd /usr/local/download
		tar -ztvf redis-4.0.0.tar.gz
		tar -zxvf redis-4.0.0.tar.gz -C /usr/local
		mv redis-4.0.0 redis
		
		
		cd /usr/local/redis
		make
		
		make 报错，需要安装程序：yum -y install gcc automake autoconf libtool make
		make MALLOC=libc
	
	（3）修改配置
		cd /usr/local/redis
		vi redis.conf
		
		requirepass 123456
	
	（4）启动
		cd /usr/local/bin
		./redis-server /usr/local/redis/redis.conf 
	
	（5）使用客户端连接
		cd /usr/local/bin
		./redis-cli
	
5，部署程序

	（1）图书：Spring + SpringMVC + Mybatis + MySQL
	https://github.com/liyifeng1994/ssm
	
	（2）订单：Spring + SpringMVC + Mybatis + MySQL + Redis
	https://github.com/wosyingjun/beauty_ssm
		
		[1]打包
		在本地maven install生成war包ssm-demo2_0.0.1-SNAPSHOT_20180509.war
		
		[2]创建路径
		mkdir -p /home/www/war
		mkdir -p /home/www/webapps/demo1
		mkdir -p /home/www/webapps/demo2
		mkdir -p /home/www/logs/demo1
		mkdir -p /home/www/logs/demo2
		
		[3]上传
		FTP上传ssm-demo2_0.0.1-SNAPSHOT_20180509.war到/home/www/war目录下
		
		[4]解压
		cd /home/www/war
		jar -tvf ssm-demo2_0.0.1-SNAPSHOT_20180509.war
		jar -xvf ssm-demo2_0.0.1-SNAPSHOT_20180509.war /home/www/webapps/demo2
		
		[5]修改tomcat配置
		参考：server.xml
		
		[6]启动tomcat，访问测试
		http://ip:8080/user/list
		http://ip:8080/goods/list
		
