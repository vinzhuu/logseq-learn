tags:: [[Docker]]
---

- ## CentOS
	- ### 使用 YUM 从 RPM 仓库下载
		- ``` sh
		  # 卸载已安装的 Docker
		  sudo yum remove docker \
		                    docker-client \
		                    docker-client-latest \
		                    docker-common \
		                    docker-latest \
		                    docker-latest-logrotate \
		                    docker-logrotate \
		                    docker-engine
		                    
		  # (可选)删除 旧 docker 生成的文件 (Images, containers, volumes, and networks)
		  rm -rf /var/lib/docker/
		  
		  # 安装 yum-utils ，yum-utils 提供了 yum-config-manager
		  sudo yum install -y yum-utils
		  # 使用 yum-config-manager 配置 docker 所在仓库
		  sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
		  
		  # 下载 docker 相关组件
		  sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
		  
		  # 启动 docker
		  sudo systemctl start docker
		  
		  # 下载并启动 hello-world 镜像，以测试是否安装成功
		  sudo docker run hello-world
		  ```
	-