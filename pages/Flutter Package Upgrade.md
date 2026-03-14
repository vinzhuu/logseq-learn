tags:: [[Flutter Package]]
---

- ## Upgrade Apps' packages
	- 参考: [Upgrade packages](https://docs.flutter.dev/install/upgrade#upgrade-packages)
	- 更新 `pubspec.yaml` 中的所有依赖, 至 **最新兼容版本 (latest compatible version)**
		- ``` sh
		  flutter pub upgrade
		  ```
	- 更新 `pubspec.yaml` 中的所有依赖, 至 **最新可用版本 (latest possible version)**
		- ``` sh
		  flutter pub upgrade --major-versions
		  ```
	- 对应地, `pubspec.yaml` 中的内容也会被修改.
	- 另外, 执行 `flutter pub outdated` 可以得到 `pubspec.yaml` 中过时的依赖的信息.
-