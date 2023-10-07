是指[数据库管理系统](https://zh.wikipedia.org/wiki/%E6%95%B0%E6%8D%AE%E5%BA%93%E7%AE%A1%E7%90%86%E7%B3%BB%E7%BB%9F "数据库管理系统")（DBMS）在写入或更新资料的过程中，为保证[交易](https://zh.wikipedia.org/wiki/%E6%95%B0%E6%8D%AE%E5%BA%93%E4%BA%8B%E5%8A%A1 "数据库事务")（transaction）是正确可靠的，所必须具备的四个特性：[原子性](https://zh.wikipedia.org/w/index.php?title=%E5%8E%9F%E5%AD%90%E6%80%A7&action=edit&redlink=1)（atomicity，或称不可分割性）、[一致性](https://zh.wikipedia.org/wiki/%E4%B8%80%E8%87%B4%E6%80%A7_(%E6%95%B0%E6%8D%AE%E5%BA%93) "一致性 (数据库)")（consistency）、[隔离性](https://zh.wikipedia.org/wiki/%E9%9A%94%E9%9B%A2%E6%80%A7 "隔离性")（isolation，又称独立性）、[持久性](https://zh.wikipedia.org/wiki/%E6%8C%81%E4%B9%85%E6%80%A7 "持久性")（durability）。
## 四大特性
### 原子性（Atomicity）
一个事务（transaction）中的所有操作，或者全部完成，或者全部不完成，不会结束在中间某个环节。事务在执行过程中发生错误，会被[回滚](https://zh.wikipedia.org/wiki/%E5%9B%9E%E6%BB%9A_(%E6%95%B0%E6%8D%AE%E7%AE%A1%E7%90%86) "回滚 (数据管理)")（Rollback）到事务开始前的状态，就像这个事务从来没有执行过一样。即，事务不可分割、不可约简。
### [一致性](https://zh.wikipedia.org/wiki/%E4%B8%80%E8%87%B4%E6%80%A7_(%E6%95%B0%E6%8D%AE%E5%BA%93) "一致性 (数据库)")（Consistency）
在事务开始之前和事务结束以后，数据库的完整性没有被破坏。这表示写入的资料必须完全符合所有的预设[约束](https://zh.wikipedia.org/wiki/%E6%95%B0%E6%8D%AE%E5%AE%8C%E6%95%B4%E6%80%A7 "数据完整性")、[触发器](https://zh.wikipedia.org/wiki/%E8%A7%A6%E5%8F%91%E5%99%A8_(%E6%95%B0%E6%8D%AE%E5%BA%93) "触发器 (数据库)")、[级联回滚](https://zh.wikipedia.org/wiki/%E7%BA%A7%E8%81%94%E5%9B%9E%E6%BB%9A "级联回滚")等。
### [事务隔离](https://zh.wikipedia.org/wiki/%E4%BA%8B%E5%8B%99%E9%9A%94%E9%9B%A2 "事务隔离")（Isolation）
数据库允许多个并发事务同时对其数据进行读写和修改的能力，隔离性可以防止多个事务并发执行时由于交叉执行而导致数据的不一致。事务隔离分为不同级别，包括未提交读（Read uncommitted）、提交读（read committed）、可重复读（repeatable read）和串行化（Serializable）。
### [持久性](https://zh.wikipedia.org/wiki/%E6%8C%81%E4%B9%85%E6%80%A7 "持久性")（Durability）
事务处理结束后，对数据的修改就是永久的，即便系统故障也不会丢失