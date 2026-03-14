tags:: [[Raspberry Pi]]
---

- ## 步骤
	- 确保树莓派处于未通电状态, 插入 `microSD` (或其他存储设备) .
	  logseq.order-list-type:: number
	- 连接 鼠标, 键盘 和 显示器.
	  logseq.order-list-type:: number
	- 连接电源: 
	  logseq.order-list-type:: number
		- 树莓派会自动启动
		  logseq.order-list-type:: number
		- 指示灯亮起
		  logseq.order-list-type:: number
		- 显示器显示启动画面
		  logseq.order-list-type:: number
	- 连接网络 (Wi-Fi 或 有线).
	  logseq.order-list-type:: number
- ## 未成功启动
	- 查看指示灯, 了解详细信息 (参见 [[Raspberry Pi: 指示灯]])
	- 按如下步骤重新安装系统:
		- 如果用了非 SD Card , 则改用 SD Card .
		  logseq.order-list-type:: number
		- 重新安装系统 (参见 [[Raspberry Pi: 安装系统]]), 并确保不跳过 Verify 步骤.
		  logseq.order-list-type:: number
			- ==如果还是不行, 则进行下一步==
		- 更新 bootloader (参见 [[Raspberry Pi: 更新 bootloader]]), 重新安装系统 (参见 [[Raspberry Pi: 安装系统]]), 并确保不跳过 Verify 步骤.
		  logseq.order-list-type:: number
- ## 问题处理
	- ### 连接显示器没反应
		- 参考: [树莓派连接显示器不亮屏的解决方案](https://zhuanlan.zhihu.com/p/55366332)
		- 需要修改 `config.txt` 文件
		- ``` properties
		  hdmi_force_hotplug=1
		  config_hdmi_boost=4
		  hdmi_group=2
		  hdmi_mode=9
		  # hdmi_drive=2
		  hdmi_ignore_edid=0xa5000080
		  disable_overscan=1
		  ```
- ## 参考
	- [Set up your Raspberry Pi](https://www.raspberrypi.com/documentation/computers/getting-started.html#set-up-your-raspberry-pi)
	  logseq.order-list-type:: number