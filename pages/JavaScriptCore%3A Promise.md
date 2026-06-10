tags:: [[JavaScriptCore]], [[Promise API]] 
---

- ## 各版本对 Promise 的支持程度
	- ==参考: DeepSeek (或许有误)==
	- | 系统 & 版本 | Promise API 支持 (如 `new Promise`) | 微任务 (Microtask) 队列实现 | 
	  | ---- | ---- | ---- |
	  | **iOS / iPadOS 16.0 及以上** | ✅ 支持 | ✅ 符合规范 (标准微任务) | 
	  | **iOS / iPadOS 13.0 -  15.x** | ✅ 支持 | ❌ 不符合规范 (用 `setTimeout` 模拟, 作为宏任务执行) | 
	  | **iOS/ iPadOS 12.x 及更低** | ❌ 不支持 | 不适用 |
	  | **macOS 11.0 (Big Sur) 及以上** | ✅ 支持 | ✅ 符合规范 (标准微任务) | 
	  | **macOS 10.15 (Catalina)** | ✅ 支持 | ❌ 不符合规范 (用 `setTimeout` 模拟, 作为宏任务执行) | 
	  | **macOS 10.14 (Mojave) 及更低** | ❌ 不支持 | 不适用 |
	- JavaScriptCore 的新版本, 是与 Apple 家的系统一起发布的, 所以这里用 **系统版本** 来说明.
- ## 旧版本使用 setTimeout 模拟 Promise
	- 参考: [Promise 时序差异](https://developers.weixin.qq.com/miniprogram/dev/framework/runtime/js-support.html#Promise-%E6%97%B6%E5%BA%8F%E5%B7%AE%E5%BC%82)
	- 使用 `setTimeout` , 意味着 `Promise` 触发的任务为 **普通任务**  (或称 **宏任务** , 非官方称呼) ，而非 **微任务** .
		- 因此, 旧版本 `Promise` 的执行时序, 会和 **标准** 存在差异.
		- 具体参见: [[JavaScript Async]]
	- 示例:
		- ``` js
		  var arr = []
		  
		  setTimeout(() => arr.push(6), 0)
		  arr.push(1)
		  const p = new Promise(resolve => {
		    arr.push(2)
		    resolve()
		  })
		  arr.push(3)
		  p.then(() => arr.push(5))
		  arr.push(4)
		  setTimeout(() => arr.push(7), 0)
		  
		  setTimeout(() => {
		    // 应该输出 [1,2,3,4,5,6,7]
		    // 在 iOS15 小程序环境，这里会输出 [1,2,3,4,6,5,7]
		    console.log(arr)
		  }, 1000)
		  ```
-