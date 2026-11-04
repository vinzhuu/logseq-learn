tags:: [[MySQL Index]]
---

- ## Index Types Per Storage Engine
	- | Storage Engine | Permissible Index Types |
	  | ---- | ---- | ---- |
	  | InnoDB | `BTREE` |
	  | MyISAM | `BTREE` |
	  | MEMORY / HEAP | `HASH`, `BTREE` |
	  | NDB | `HASH`, `BTREE` (see note in text) |
-