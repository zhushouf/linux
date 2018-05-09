## Linux

1，搭建环境：VMware 14.1.1 虚拟机下安装 CentOS 6.7
	
	（1）下载并安装虚拟机软件，VMware 14.1.1试用版（30天）、VirtualBox 5.2免费
	http://www.vmware.com/cn/products/workstation/workstation-evaluation.html
	https://www.virtualbox.org/wiki/Downloads
	
	（2）服务器操作系统
	CentOS 6.8~7.4 64位
	Ubuntu 16.04 14.04 64位
	Windows Server 2016
	Windows Server 2012 R2
	
	（3）下载系统镜像
	http://vault.centos.org/
	http://archive.kernel.org/centos-vault/6.7/isos/x86_64/
	
	（4）安装CentOS 6.7
	
	
	（5）修改网络配置
	vi /etc/sysconfig/network-scripts/ifcfg-eth0
	
	#自动获取IP
	DEVICE=eth0
	HWADDR=00:50:56:35:9F:60
	TYPE=Ethernet
	UUID=366a8af0-0be5-4c6f-b6b7-c79a05d1229a
	ONBOOT=yes
	NM_CONTROLLED=yes
	BOOTPROTO=dhcp

2，客户端工具：SecureCRT.exe
	
	（1）下载并安装
	http://www.kuaihou.com/soft/169214.html

	（2）连接本地Linux系统

3，linux教程（练习）

	http://www.runoob.com/linux/linux-tutorial.html
	
	
	
	
	
	
	
	
	

4，学习资料

	http://www.runoob.com/linux/linux-install.html
	https://www.linuxidc.com
