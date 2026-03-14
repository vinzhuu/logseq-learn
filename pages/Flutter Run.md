tags:: [[Flutter]]
---

- ## 真机连接方式
	- 注意, 进行 debug 模式运行时到 **真机设备** 时, 最好使用 **有线连接** , **无线连接** 可能会有问题.
	- 比如, 我使用 IDE (IDEA 或 VS Code) 集成的运行功能, 进行 debug 模式运行时:
		- 会出现白屏, 并有如下日志.
		- ``` zsh
		  [  +56 ms] Connecting to service protocol: http://192.168.5.32:62301/xxxxx/
		  [+75005 ms] Exception attempting to connect to the VM Service: SocketException: Operation timed out (OS Error: Operation timed out, errno = 60), address = 192.168.5.32, port = 60928
		  [        ] This was attempt #1. Will retry in 0:00:00.100000.
		  [+75105 ms] Exception attempting to connect to the VM Service: SocketException: Operation timed out (OS Error: Operation timed out, errno = 60), address = 192.168.5.32, port = 61226
		  [        ] This was attempt #2. Will retry in 0:00:00.200000.
		  [+75203 ms] Exception attempting to connect to the VM Service: SocketException: Operation timed out (OS Error: Operation timed out, errno = 60), address = 192.168.5.32, port = 61537
		  [        ] This was attempt #3. Will retry in 0:00:00.400000.
		  [+75403 ms] Exception attempting to connect to the VM Service: SocketException: Operation timed out (OS Error: Operation timed out, errno = 60), address = 192.168.5.32, port = 61808
		  [        ] This was attempt #4. Will retry in 0:00:00.800000.
		  ```
		- (命令行执行时, 不会白屏, 但执行 `flutter run --debug --verbose` 也会出现如上日志),
		- 貌似是 "电脑连接手机上 App 内置的 Debugger 失败" 导致.
		  id:: 69a44930-ed50-4f93-899f-cf9833e92347
		- ==暂不知道具体原因==
	-
-