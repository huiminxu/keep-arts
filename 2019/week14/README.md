## ARTS(week14)

### 算法题(Algorithm)

[字符串中的第一个唯一字符](https://github.com/geekwho11/learn.leetcode.xbcme/tree/master/php/src/387.first-unique-character-in-a-string)

### 阅读点评(Review)

#### [When and Why to use a Least Frequently Used (LFU) cache with an implementation in Golang](https://ieftimov.com/when-why-least-frequently-used-cache-implementation-golang/)

#### 阅读笔记

##### 什么是LFU

所谓的LFU是，最少使用算法，当达到了缓存的固定容量限制，会删除缓存中不常用的内容。

##### 为什么要使用LFU

1. 最简单的性能改进方法是缓存。
2. 缓存的想法非常简单，存储经常需要使用的数据，可以非常快的检索。
3. 缓存必须在2个点要快：尽可能多的命中缓存，而不是通过网络或主内存。使用缓存的代价非常小。

##### 怎么应用LFU

LFU最直接的应用：

1. CDN图片，可以采用LFU算法进行缓存。
2. 比如谷歌的标识Logo，越多人使用，就越应用缓存它。

LFU的实现一般是采用一个固定大小的最小堆或最大堆。还有人用2个链表也实现了。文章中采用一个新的实现方案：双向链表和哈希表。

#### 参考链接

1. [An O(1) algorithm for implementing the LFU cache eviction scheme](http://dhruvbird.com/lfu.pdf)

### 技术技巧(Tip)

#### git diff

```
# 获取两个commit id 之间差异文件,只显示文件名字
git diff --name-only commit_id1 commit_id2
# --diff-filter参数 添加更多的过滤条件，一般用得较多的有AM
# A 添加的
# M 修改的
git diff --name-only commit_id1 commit_id2

# 获取master的commit id
git rev-parse master
```

#### 参考链接
1. [git-diff](https://git-scm.com/docs/git-diff)
2. [git-rev-parse](https://git-scm.com/docs/git-rev-parse)

### 分享(Share)

#### [深入理解 MySQL 事务隔离级别和 MVCC 原理](https://mp.weixin.qq.com/s?__biz=MzI0MzQyMTYzOQ==&mid=2247485064&idx=1&sn=c2adf147fef29ba3cf5f117182998d78&chksm=e96c1e20de1b9736ece479bbed114a564cec6fddb4c93510471ae4bf45e90c0af62a1143ec82&mpshare=1&scene=1&srcid=0405FAD1HZDJPnd2D2Ph3vqs#rd)

#### 阅读笔记

文章很详细介绍了MySQL的四个隔离级别以及特点，我在之前的[文章]([https://xbc.me/mysql/](https://xbc.me/mysql/))整理过相关知识点：

| 隔离级别            | 有点   | 缺点    | 备注        |
| --------------- | ---- | ----- | --------- |
| READ UNCOMMITED | --   | 脏读、幻读 | 读取未提交的事务  |
| READ COMMITED   | --   | 幻读    | 读取提交的事务   |
| REPEATABLE READ | --   | 幻读    | 重复读取已提交事务 |
| SERIALIZABLE    | --   | 并发性能低 | 加锁读取      |

##### 什么是脏读

在两个Seesion中，某个事务读到另一个事务未提交的修改，可能获取到一个不存在的数据，这种现象称为 脏读。

##### 什么是幻读

所谓的幻读就是，2个不同的线程，线程A执行查询操作时，得到结果集1，这时，线程B执行插入数据的操作并提交事务，线程A再次执行查询操作时，得到结果集2，会发现结果集2中出现新的插入的行，新增返回的行，就是所谓的幻影行。

##### 什么是MVCC原理

所谓的MVCC就是Mult Version Concurrency Control。InnoDB通过MVVC的并发控制解决了幻读问题。MySQL的InnoDB类型的存储引擎，通过在表每一行添加3个字段记录相关的回滚操作：

| 字段          | 作用             | 备注   |
| ----------- | -------------- | ---- |
| DB_TRX_ID   | 标识当前最后的一个事务标示符 |      |
| DB_ROLL_PTR | 撤销日志的指针，指向回滚段  |      |
| DB_ROW_ID   | 新增的行标识         |      |



