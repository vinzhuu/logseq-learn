tags:: [[Antigravity]]
---

- ## 使用 Proxifier
	- 直接使用代理软件的话, 需要开启 `TUN` / 增强模式. 这对访问其他网站是有影响的.
	- 使用 Proxifier , 按如下图片设置:
		- ![image.png](../assets/image_1765043756802_0.png){:height 425, :width 860}
		- ``` sh
		  # Applications
		  "Antigravity.app"; "Antigravity"; com.google.antigravity; "Antigravity Helper"; com.google.antigravity.helper; language_server_macos_arm
		  
		  # Target Hosts (这个一定要加, 不加就不行)
		  *.googleapis.com;*.googleusercontent.com
		  ```
- ## 参考
	- [保姆级教程教你如何解决antigravity登不上，我奶奶看了都能学会](https://linux.do/t/topic/1190137)
	  logseq.order-list-type:: number
		- 只有这个教程提到要加 `Target Hosts`
	- [Antigravity 如何使用代理模式访问，需要改什么配置？ tun 模式使用不方便](https://v2ex.com/t/1173881)  > [发现了Antigravity登录时浏览器无法跳转的解决办法](https://linux.do/t/topic/1185942)
	  logseq.order-list-type:: number
	-