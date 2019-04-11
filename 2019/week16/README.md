## ARTS(week16)

### 算法题(Algorithm)

[验证回文串](https://github.com/geekwho11/learn.leetcode.xbcme/tree/master/php/src/125.valid-palindrome)

### 阅读点评(Review)

#### [Efficient data structures for PHP 7](https://medium.com/@rtheunissen/efficient-data-structures-for-php-7-9dda7af674cd)

#### 阅读笔记

新版PHP7对比下来，大约有2倍的性能提升。

| 名称            | 优点                                   | 缺点                               | 备注                    |
| ------------- | ------------------------------------ | -------------------------------- | --------------------- |
| Collection    | --                                   | --                               | 集合、接口                 |
| Sequence/List | 类似增量整数键的数组                           | 索引范围为[0,size-1]                  | 列表、接口                 |
| Hashable      |                                      |                                  | 哈希表、接口                |
| Vector        | get/set/push/pop O(1)                | insert/remove/shift/unshift O(n) |                       |
| Deque         | get/set/push/pop/shift/unshift  O(1) | insert/remove O(n)               |                       |
| Map           | get/set/remove/hasKey  O(1)          |                                  | 键值对的有序集合，键是唯一的，任意类型的键 |
| Set           | add/remove/contains  O(1)            | 不支持push pop insert shift unshift | 唯一值的集合。任意类型的值         |
| Stack         |                                      |                                  | 栈，后进先出                |
| Queue         |                                      |                                  | 队列，先进先出               |
| PriorityQueue | 最大堆实现                                |                                  | 优先队列                  |
| Pair          |                                      |                                  |                       |

Vector是可自动增大和缩小，连续缓冲区的值序列。它有这最有效的顺序结构，缓冲区的值与索引是直接映射的，增长因子不绑定倍数或者指数。

Deque是双端队列，采用2个指针跟踪头部和尾部。从头移除，从头移入，都非常快。索引访问对应位置的公式为：((head + position) % capacity)

Discontiguous data structures are the root of all performance evil. Specifically, please say no to linked lists.

非连续的数据结构是万恶之源，具体来说，请尽量不使用链表。

Efficient code reduces the load on our servers, reduces the response time of our APIs and web pages, and reduces the runtime of our development tools. **Performance is important**, but maintainable code should come first.

高效的代码可以减轻我们服务器的压力，缩短API和网页的响应时间，并缩短开发工具的运行时间。性能很重要，但可维护的代码应该是第一位。

### 技术技巧(Tip)

Docker的常用指令技巧：

1. RUN 执行命令并创建新的镜像层，RUN 经常用于安装软件包。
2. CMD 设置容器启动后默认执行的命令及其参数，但 CMD 能够被 `docker run` 后面跟的命令行参数替换。
3. ENTRYPOINT 配置容器启动时运行的命令。

Shell格式，底层调用/bin/sh -c command

```shell
RUN apt-get install python3  

CMD echo "Hello world"  

ENTRYPOINT echo "Hello world" 
```

exec格式

```shell
RUN ["apt-get", "install", "python3"]  

CMD ["/bin/echo", "Hello world"]  

ENTRYPOINT ["/bin/echo", "Hello world"]
```

#### 参考链接
1. [每天5分钟玩转 OpenStack](https://www.ibm.com/developerworks/community/blogs/132cfa78-44b0-4376-85d0-d3096cd30d3f/entry/RUN_vs_CMD_vs_ENTRYPOINT_%E6%AF%8F%E5%A4%A95%E5%88%86%E9%92%9F%E7%8E%A9%E8%BD%AC_Docker_%E5%AE%B9%E5%99%A8%E6%8A%80%E6%9C%AF_17?lang=en)

### 分享(Share)

#### [如何成为一名优秀的架构师](https://mp.weixin.qq.com/s?__biz=Mzg4NjAwMTQzNA==&mid=2247484022&idx=1&sn=e17816a0d24012e88538372705e7f656&chksm=cfa11803f8d691157e4f41f200e863b65765366060acda36aab8821756c865c632184115b28d&mpshare=1&scene=1&srcid=0404oNKfvZFlaiq4P5pGYQ1z#rd)

#### 阅读笔记

总结几点重要的方法论：

1. 开发项目的规模是能让你的技术有所成长关键点，一个亿级用户币千万级用户的项目复杂度是10倍以上。
2. 从简单的小需求开始做起，谁也不想一辈子做CRUD工程师。假如给你一个机会，让你重新设计系统，你会怎么做？
3. 刻意练习思考能力，功能需求都刻意去实现，那么安全需求，性能需求，可靠性，稳定性呢？这些才是系统设计的核心。
4. 技术复盘。高速发展的业务都会遇到很多问题故障。定期复盘处理的过程，一起讨论出现问题的根本原因以及改进措施。
5. 对外分享，总结。项目完成后一定要尝试去总结和分享。对自身来讲，可以发现问题以及可改进的方案。对外，可以提升自身的印象力。
