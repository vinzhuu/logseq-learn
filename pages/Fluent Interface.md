tags:: [[API Design]]
---

- 可翻译为 `流式接口` , 是一种接口的设计模式
- 例如:
	- ``` java
	  Author author = AUTHOR.as("author");
	  create.selectFrom(author)
	        .where(exists(selectOne()
	                     .from(BOOK)
	                     .where(BOOK.STATUS.eq(BOOK_STATUS.SOLD_OUT))
	                     .and(BOOK.AUTHOR_ID.eq(author.ID))));
	  ```
-
- ## 参考
	- [流式接口](https://zh.wikipedia.org/wiki/%E6%B5%81%E5%BC%8F%E6%8E%A5%E5%8F%A3)
	  logseq.order-list-type:: number
-