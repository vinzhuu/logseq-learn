tags:: [[Redis]]
---

- ## 批量删除Key
	- ```sh
	  redis-cli -h IP -p PORT -a PASSWORD -n DBIndex keys 'key*' | xargs redis-cli -h IP -p PORT -a PASSWORD -n DBIndex del
	  ```
- ## Sorted Set
	- ``` sh
	  // 查看所有带元素 并且带分数 (按分数从小到大排)
	  zrange ${myZset} 0 -1 withscores
	  
	   1) "0001"
	   2) "1"
	   3) "0002"
	   4) "2"
	  ```
-
-