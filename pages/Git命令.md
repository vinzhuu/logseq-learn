tags:: [[Git]]
---

- ## 常用命令
	- ``` sh
	  # 初始化git
	  git init
	  
	  # 展示要删除的文件预览
	  git rm -r -n --cached "bin/"
	  git rm -r -n --cached "*.iml"
	    
	  # 将文件移出版本控制
	  git rm -r --cached  "bin/"
	  git rm -r --cached  "*.iml"
	  
	  # 展示仓库中的所有文件
	  git ls-files
	  ```
- ## 本地分支相关
	- ``` sh
	  # 从当前分支新建分支
	  git checkout -b xxx
	  
	  # 删除分支（带警告）
	  git branch -d xxx
	  # 删除分支（不带警告，强行删除）
	  git branch -D xxx
	  
	  # 分支重命名
	  git branch -m old-name new-name
	  ```
- ## 远程分支相关
	- ```sh
	  # 设置远程分支
	  git remote add origin https://github.com/nigream/learning-notes.git
	  # 修改远程分支地址
	  git remote set-url origin https://github.com/nigream/learning-notes.git
	  git
	  # 刷新分支
	  git remote update origin --prune
	  
	  # 获取远程分支 xxx
	  git fetch origin xxx
	  
	  # 拉取所有分支
	  git fetch
	  
	  # 拉取远程的某个分支到本地
	  git checkout -b xxxx origin/xxxx
	  
	  # 更新远程仓库的分支（会删除远程仓库已删除的分支）
	  git fetch --prune
	  
	  # 将远程分支合并到本地分支
	  git fetch
	  git merge origin/xxxxx
	  ```
- ## 提交相关
	- ```sh
	  # 修改本地上一次提交的信息
	  git commit --amend -m "New commit message."
	  
	  # 将当前暂存区的文件修改，合并到上一次提交
	  git commit --amend
	  
	  # 将合并后的提交推送到远程仓库
	  
	  ```
- ## Config
	- ```sh
	  # 获取用户名
	  git config user.name
	  
	  # 设置用户名
	  git config user.name 'nigream'
	  ```
- ## Credential
	- ``` sh
	  # 去掉 credential.helper 配置
	  git config --system --unset credential.helper
	  
	  # 将账号密码保存
	  git config --global credential.helper store
	  ```
- ## ssh配置
	- ```sh
	  # 生成公钥秘钥
	  ssh-keygen -t rsa -C "xxxx@gmail.com"
	  ```
	- 生成 公钥（`id_rsa`）、私钥（`id_rsa.pub`）两个文件在 `%homepath%/.ssh` 目录下
	- 将 **公钥** 配置到 gitee、github、gitlab等平台即可使用 ssh url 进行 clone。
-