tags:: [[Linux]], [[RPM]], [[YUM]] 
---

- ## 安装 YUM
	-
- ## 安装常用工具
	- ``` sh
	  ################# 安装 unzip 和 zip #################
	  yum install unzip
	  yum install zip
	  
	  
	  ################# 安装 git #################
	  ################# https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git
	  yum install git-all
	  # 查看版本
	  git version
	  
	  
	  ################# 安装 node.js #################
	  ################# https://nodejs.org/en/download/package-manager 
	  # installs nvm (Node Version Manager)
	  curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
	  # download and install Node.js (you may need to restart the terminal)
	  nvm install 20
	  # verifies the right Node.js version is in the environment
	  node -v # should print `v20.15.0`
	  # verifies the right NPM version is in the environment
	  npm -v # should print `10.7.0`
	  
	  
	  ################# 配置 npm 淘宝镜像 #################
	  npm config set registry https://registry.npmmirror.com
	  # 查看配置
	  npm config get registry
	  
	  
	  ################# 安装 hexo #################
	  ################# https://hexo.io/docs/index.html#Install-Hexo
	  npm install hexo-cli -g
	  # 查看 hexo 版本
	  hexo version
	  
	  
	  ################# 安装 sdkman #################
	  ################# https://sdkman.io/install
	  curl -s "https://get.sdkman.io" | bash
	  source "$HOME/.sdkman/bin/sdkman-init.sh"
	  # 查看 sdkman 版本
	  sdk version
	  # 发现好像 sdkman 中没有 openjdk 或 oracle jdk 的 1.8 版本
	  
	  
	  ################# 安装 openjdk 1.8 #################
	  ################# https://openjdk.org/install/
	  su -c "yum install java-1.8.0-openjdk"
	  # 查看 java 版本
	  java -version
	  
	  ################# 安装 Maven #################
	  ################# https://maven.apache.org/download.cgi
	  # 貌似官方未提供 yum 包
	  yum install maven
	  # 查看 Maven 版本
	  mvn -version
	  # 新建 ~/.m2/settings.xml 文件编辑如下内容
	  
	  ```
- ## 安装一些服务
	- ``` sh
	  ################# 安装 Caddy #################
	  ################# https://caddyserver.com/docs/install#fedora-redhat-centos
	  yum install yum-plugin-copr
	  yum copr enable @caddy/caddy
	  yum install caddy
	  
	  
	  ################# 安装 Redis #################
	  ################# https://redis.io/docs/latest/operate/oss_and_stack/install/install-redis/install-redis-on-linux/
	  # 官方文档中没有提到 redis 在 yum 仓库的包
	  yum install redis
	  # 后台启动 redis
	  systemctl start redis
	  # 设置 redis 开机自启
	  systemctl enable redis
	  # 连接 redis 进行测试
	  redis-cli
	  ```
	- ### 安装 MySQL
		- ``` sh
		  ################# 安装 MySQL #################
		  ################# https://dev.mysql.com/doc/refman/8.4/en/linux-installation-yum-repo.html
		  # 1. 到这里安装下载对应系统的包：https://dev.mysql.com/downloads/repo/yum/
		  # 2. 安装下载的包(安装成功后会在系统增加 MySQL的 Yum 仓库)
		  yum localinstall 下载的RPM文件路径
		  # 查看 repo 是否已启用
		  yum repolist enabled | grep mysql.*-community
		  # 查看所有已配置的 repo (已启用的是最新版本的 MySQL 的库)
		  yum repolist all | grep mysql
		  ####### 以上步骤只需执行一次即可
		  ####### 下面直接安装最新版本的 MySQL
		  # 安装 MySQL 服务端 (同时也会安装客户端 mysql-community-client)
		  yum install mysql-community-server
		  # 启动 MySQL 服务 (mysqld 默认开机自启)
		  systemctl start mysqld
		  # 查看 MySQL 服务状态
		  systemctl status mysqld
		  # 查看 root 的 临时密码
		  sudo grep 'temporary password' /var/log/mysqld.log
		  # 使用上述密码登录 MySQL
		  mysql -uroot -p
		  # 修改 root 的密码
		  mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'xxxx';
		  #### 执行以下几行代码，以创建可以在任何主机上连接 mysql 的 root 用户，并赋予所有其所有权限。
		  CREATE USER 'root'@'%' IDENTIFIED BY 'xxxx';
		  GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;
		  FLUSH PRIVILEGES;
		  ```
		-