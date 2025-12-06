tags:: [[Alibaba Druid]]
---

- 参考: [com.alibaba.druid.pool.DruidPooledResultSet #1456](https://github.com/alibaba/druid/issues/1456)
- 1.1.9 版本不支持 ResultSet 的 getObject(String column, Class<T> type) 方法
- 此方法用来获取 JDBC ResultSet 中的对象，并将其转成 Java 中的对象。
- 将 Druid 升级到最新版本 (如 1.2.8) 可以解决。