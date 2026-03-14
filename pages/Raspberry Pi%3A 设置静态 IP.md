tags:: [[Raspberry Pi]]
---

- ## 步骤
	- 远程连接树莓派.
	  logseq.order-list-type:: number
	- 执行 `sudo nano /etc/dhcpcd.conf` ，在文件末尾加入如下内容 ( `ctrl+o` -> `enter` -> `ctrl+x` 保存并退出 )
	  logseq.order-list-type:: number
		- ```sh
		  # 有线网络配置
		  interface eth0
		  static ip_address=192.168.5.11/24
		  static routers=192.168.5.1
		  static domain_name_servers=114.114.114.114
		   
		  # 无线网络配置
		  interface wlan0
		  # 静态IP
		  static ip_address=192.168.5.11/24
		  # 网关 这个查看自己路由器的网关
		  static routers=192.168.5.11
		  # DNS 114.114.114.114 为给国内常用的共用DNS服务器
		  static domain_name_servers=114.114.114.114
		  ```
	- 执行 `sudo reboot` 重启树莓派.
	  logseq.order-list-type:: number
- ## 参考
	- [树莓派设置静态ip的方法](https://blog.csdn.net/qq_41204553/article/details/127936312)
	  logseq.order-list-type:: number