## ARTS(week19)

### 算法题(Algorithm)

[最长公共前缀](https://github.com/geekwho11/learn.leetcode.xbcme/tree/master/php/src/14.longest-common-prefix)

### 阅读点评(Review)

#### [多线程简介](https://github.com/xitu/gold-miner/blob/master/TODO1/gentle-introduction-multithreading.md)

#### 阅读笔记

多线程就是指在同一个进程中运行多个线程的技术。 

你可以把操作系统理解为一个包含多个进程的容器，其中的每个进程都是一个包含多个线程的容器。

| 进程A  | 进程B  |
| ---- | ---- |
| 线程1  | 线程1  |
| --   | 线程2  |

多个线程从同一个内存位置读取数据是不会引起问题的。问题在于，多个线程写数据到共享内存中，可能会出现2个问题：

1. 数据竞争，当写线程修改内存的时候，读线程可能在这个时候读取内存。写线程还没有完成操作，读线程就可能会得到无效的数据。
2. 竞争条件，读线程应该在写线程写完之后读取内存。多个线程以不可预知的顺序执行工作。

出现数据竞争的根本原因，绝大部分CPU操作都是非原子的。大部分操作都是由多个原子机器指令组成的。

出现竞争条件的根本原因，多个线程的运行结果会依赖高级调度算法的执行顺序。

并发控制的几个解决方案：

1. 同步。确保同一时间资源只会被一个线程使用。
2. 原子操作。由于操作系统提供了特殊指令，是部分非原子操作可以变成原子操作。
3. 不可变数据。共享数据标识为不可变的，没有什么可以改变它。

#### 参考链接

1. [多线程简介：一步一步来接近多线程的世界](https://mp.weixin.qq.com/s?__biz=Mzg5NjAzMjI0NQ==&mid=2247484508&idx=3&sn=fabe5de355e829cd8978a426ddaf2dfb&chksm=c00608c6f77181d03849ff20e18adcd1963d47bad232d08d4c7c26ece62fea1d90f39de2a94f&mpshare=1&scene=1&srcid=0403wFzSqDtTCYHfGR8q5GBx#rd)

### 技术技巧(Tip)

#### 常用Linux命令

##### 升级ubuntu 到最新版本

```bash
sudo apt update && sudo apt dist-upgrade && sudo apt autoremove

sudo do-release-upgrade
```
##### 设置固定IP地址
有时候设置固定ip地址，你不知道哪个IP地址是可用的。

```
sudo apt-get install nmap
nmap -sP 192.168.1.* #ping扫描，仅仅检查主机是否存活
```
##### 新建文档
Ubuntu右键添加新md文件的模板。

```
在你的主目录，找到模板文件夹，新建一个README.md。后续新建文档会这个文件作为模板。
```
##### 删除文件
为了防止误删除文件，我常常使用命令行trash-cli，这样删除了的文件都会放在回收站里。

```
sudo apt install trash-cli
```

### 分享(Share)

#### [RabbitMQ 消息可靠性、延时队列以及高可用集群](https://mp.weixin.qq.com/s?__biz=MzI0MzQyMTYzOQ==&mid=2247485120&idx=1&sn=6c54d64257a4ac35ba5ac889a343f04a&chksm=e96c1e68de1b977efda136702ef65279795840d97322b29eb5f0f2a066d1ac1cd4370a0e0227&mpshare=1&scene=1&srcid=0422N25Vz9osbJjjpWIbc2Na#rd)

#### 阅读笔记

#### RabbitMQ特性

1. 消息的接受(消费者)
2. 消息的发送者(生产者)
3. 消息的存储(持久化)
4. 延后传递(堆积)
5. 复制(广播)
6. 分发(分类路由)

#### 消息不可靠

1. 网络故障
2. 宕机
3. kill -9

#### 消息可靠

1. Server Deliver后不删除
2. Client收到消息处理后回复ack
3. Server收到ack后删除消息
4. 没收到ack消息　关闭后，重新投递消息
5. ack丢失会导致消息重复处理
6. 去重幂等由业务系统自己实现

#### Auto Ack vs Manual Ack

1. AutoAck投后即删 noack
2. 网络故障，消息丢失
3. 消费慢，投递风暴
4. 缓冲区堆积：Server写不动
5. 链接被Server强制关闭
6. Manual Ack善解人意(照顾客户端)
7. 客户端PrefetchCount　能力参数
8. Deliver有限个消息
9. Ack一个，Deliver一个

#### 生产端消息可靠性

1. 生产的消息也会丢
2. fsync几百毫秒一次
3. Server宕机
4. Redis AOF
5. 用select和commit，包裹publish
6. commit要等到fsync才返回，奇慢
7. 批量publish

##### 生产者确认

1. 等价于 消费者ack(fsync)
2. 生产端需要实现消息重发机制(难)
3. 没有重发机制的confirm　没什么用
4. 存内存会丢
5. 存磁盘需要fsync 无状态变有状态
6. 存Redis还会遇到网络故障(Redis也会丢)
7. ack丢失，重发会导致消息重复

#### 死信队列

1. 延时队列
2. 过期时间比较死，不灵活
3. 不同的过期时间需要不同的过期队列

Retry Later 双重死信

1. 消息处理异常，客户端reject，消息进入死信队列
2. 死信队列里消息过期重新入队列

#### 集群

1. 元信息每个节点都有
2. 队列里的消息只有一份
3. 客户端只会连接一个节点(负载均衡)
4. 服务端转发

#### 镜像队列

1. 镜像队列是默默无闻的



