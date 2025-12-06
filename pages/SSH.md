## SSH 服务端的配置
	- SSH 服务端的配置文件为  `/etc/ssh/sshd_config`
	- 常用配置项：
		- ``` config
		  # 配置是否可以通过【密码】连接
		  PasswordAuthentication no
		  
		  # 配置是否可以通过【公钥/私钥】连接 (公钥在服务端，私钥在客户端)
		  PubkeyAuthentication yes
		  ```