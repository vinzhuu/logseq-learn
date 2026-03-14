alias:: [[YUM Utils]]
---

- ## 什么是 yum-utils
	- ### 一句话解释
		- yum-utils 是 YUM 官方提供的增强 YUM 的工具集，通过命令行可以使用相关工具。
	- ### yum-utils 列表
		- 参见 [Yum Utils 列表](http://yum.baseurl.org/wiki/YumUtils.html)
- ## 如何安装 yum-utils
	- 执行 yum 命令: `yum install yum-utils` , 遇到问题输入 `y` 即可。
- ## yum-utils 之 yumdownloader
	- 从 YUM Repo 下载 RPM Package File 到本地的工具。
	- `yumdownloader [options] package1 [package2...]`
	- ``` sh
	  # 下载 nginx 包到指定目录
	  yumdownloader --destdir /var/tmp nginx
	  
	  # 查询 nginx 包所在的地址
	  yumdownloader --urls nginx
	  ```
- ## yum-utils 之 yumdownloader