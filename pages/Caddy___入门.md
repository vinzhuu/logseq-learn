## 文档阅读
	- 先通读下面两篇文章
	- [Caddy Server - Getting Started](https://caddyserver.com/docs/getting-started)
	  logseq.order-list-type:: number
	- [Caddy Server - Quick-starts](https://caddyserver.com/docs/getting-started)
	  logseq.order-list-type:: number
- ## Caddy 的配置文件
	- Caddy 支持 JSON 格式的配置，也支持 Caddyfile 格式的配置，以及其他 Caddy 兼容的格式。
- ## 启动、停止与配置重载
	- ``` sh
	  # 启动 caddy
	  caddy run --config 配置文件路径
	  
	  # 在后台启动 caddy
	  caddy start --config 配置文件路径
	  
	  # 停止 caddy
	  caddy stop
	  
	  # 重载配置
	  caddy reload
	  ```
- ## 静态文件服务器
	- ``` sh
	  # Caddyfile
	  # 这里填写域名会有 automic https
	  example.com {
	          root * /path/to/my-site
	          file_server
	  }
	  ```
-