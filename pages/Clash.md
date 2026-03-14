tags:: [[网络代理]]
---

-
- ## 如何设置代理忽略
	- 参考: [mac配置clashx代理忽略列表](https://wonderlq.github.io/archives/87d77c17.html)
	- 1、在 `~/.config/clash/` 新建 `proxyIgnoreList.plist` 文件。
	- 2、编辑文件，内容如下：
		- ``` xml
		  <?xml version="1.0" encoding="UTF-8"?>
		  <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
		  <plist version="1.0">
		  <array>
		      <string>192.168.0.0/16</string>
		      <string>10.0.0.0/8</string>
		      <string>172.16.0.0/12</string>
		      <string>127.0.0.1</string>
		      <string>localhost</string>
		      <string>*.docker-cn.com</string>
		      <string>*.cn</string>
		  </array>
		  </plist>
		  ```
	- 3、编辑保存后，重启 clashx 即可。
	- ---
	- ### 更多资料
		- 1、[分享一个新的 clash 客户端](https://www.v2ex.com/t/838078)
		- 2、[clash更新订阅时保留自己的规则](https://blog.hifool.cn/posts/f42b65b0/)
		- 3、[ClashX自定义配置文件管理](https://web.archive.org/web/20220809052657/https://donnadie.top/manage-clashx-custom-config/)
		- 4、[如何自定义流量规则 - Clashx Issue](https://github.com/yichengchen/clashX/discussions/636)
-