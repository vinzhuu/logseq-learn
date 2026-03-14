tags:: [[VPN]]
---

-
- ## 常见问题
	- ### Transport Error: socket_protect error (TCP)
		- 参见: [Github Issue](https://github.com/OpenVPN/openvpn3/issues/258)
		- Mac 电脑在连接 VPN 前执行:
		- ``` sh
		  sudo /Library/Frameworks/OpenVPNConnect.framework/Versions/Current/usr/sbin/ovpnagent
		  ```
		- 在 `System Settings > General > Login Items > Allow in the Background` 允许 OpenVPN Client 的后台运行。
		- ![image.png](../assets/image_1703435574166_0.png)
	-