tags:: [[Conda]], [[Registry]]
---

- ## 啥是 Conda Channel
	-
- ## 有哪些 Channel
	- [[Bioconda]] : [Bioconda Package Index](https://bioconda.github.io/conda-package_index.html)
	  logseq.order-list-type:: number
	- [Anaconda - Search Packages](https://anaconda.org/)
	  logseq.order-list-type:: number
	- [[conda-forge]] : [Packages in conda-forge](https://conda-forge.org/packages/)
	  logseq.order-list-type:: number
- ## 有哪些 Channel 镜像
	-
- ## 配置 Channel
	- 在 `%HOMEPATH%\.condarc` / `~/.condarc` 中加入如下配置（如果没有则新建该文件）:
		- 下面配置参见 [清华镜像](https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/)
		- ```yaml
		  channels:
		    - defaults
		  show_channel_urls: true
		  default_channels:
		    - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
		    - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
		    - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
		  custom_channels:
		    conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
		    msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
		    bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
		    menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
		    pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
		    simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
		  ```
	- 配置后执行 `conda clean --i` 以清除索引缓存，保证用的是镜像站提供的索引.
	- 下载依赖时可能需要多试几次 (可能要关闭代理) .
	-
	-