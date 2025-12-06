## Syntax
	- ``` html
	  <video src="rabbit320.webm" controls>
	    <p>
	      Your browser doesn't support HTML video. Here is a
	      <a href="rabbit320.webm">link to the video</a> instead.
	    </p>
	  </video>
	  ```
	- `src` : 视频路径
	- `controls` : 通过配置 `controls` 显示浏览器默认的视频控件 .
		- 我们也通过 JS 来自定义相关控件, 一般至少包含媒体的 播放, 暂停 和 音量调整 .
	- `<video>` 的 content : 此部分被称为 **fallback content** , 如果浏览器不支持 `<video>` 元素, 则会显示这部分内容
		- 一般会提供一个链接指向这个视频文件.
- ## Media Format
	- Media Format 有 MP3, MP4 和 WebM 等 ( 或称为 **[container formats](https://developer.mozilla.org/en-US/docs/Web/Media/Formats/Containers)** ) .
		- 不同的浏览器支持的媒体格式不同, 同一浏览器的移动和桌面版本支持的媒体格式也可能不同；
		- 此外, 浏览器可能会将媒体的播放 **转嫁 (offload)** 给用户已安装的软件.
- ## `<source>` Element
	- ``` html
	  <video controls>
	    <source src="rabbit320.mp4" type="video/mp4" />
	    <source src="rabbit320.webm" type="video/webm" />
	    <p>
	      Your browser doesn't support this video. Here is a
	      <a href="rabbit320.mp4">link to the video</a> instead.
	    </p>
	  </video>
	  ```
	- 去掉 `<video>` 标签的 `src` attribute, 改为在 content 中加入多个 `<source>` 标签.
		- 每个 `<source>` 标签用 `src` attribute 表明不同的媒体格式.
		- 浏览器会遍历所有 `<source>` 标签, 直到找到第一个自己支持的格式.
		- `mp4` 格式 和 `webm` 格式 已经可以满足大部分情况.
	- `<source>` 的 `type` attribute 最好加上, 浏览器可以通过 `type` 来快速判断自己支不支持.
		- 否则, 浏览器需要加载并试着播放媒体文件, 才能知道支不支持.
	-