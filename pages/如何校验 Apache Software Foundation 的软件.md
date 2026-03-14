tags:: [[Apache Software Foundation]], [[SHA]] 
---

- ## 1.Checking Hashes (检查文件是否无误)
	- | *compute the checksum of your file ...*| | | | *compare with* |
	  |  | Windows | Linux | Mac |  |
	  | SHA-1 (deprecated) | certUtil -hashfile *file* SHA1 | sha1sum *file* | shasum -a 1 *file* | *file*.sha1 |
	  | SHA-256 | certUtil -hashfile *file* SHA256 | sha256sum *file* | shasum -a 256 *file* | *file*.sha256 |
	  | SHA-512 | certUtil -hashfile *file* SHA512 | sha512sum *file* | shasum -a 512 *file* | *file*.sha512 |
	  | MD5 (deprecated) | certUtil -hashfile *file* MD5 | md5sum *file* | md5 *file* | *file*.md5 |
	- `SHA-1` 和 `MD5` 已被 ASF 弃用, 目前一般都用 `SHA-256` 和 `SHA-512` .
	-
-
- ## 参考
	- [Verifying Apache Software Foundation Releases](https://www.apache.org/info/verification.html)
	  logseq.order-list-type:: number
-