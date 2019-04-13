## ARTS(week18)

### 算法题(Algorithm)

[实现strStr()](https://github.com/geekwho11/learn.leetcode.xbcme/tree/master/php/src/28.implement-strstr)

### 阅读点评(Review)

[Lua 5.3 Reference Manual Modules](https://www.lua.org/manual/5.3/manual.html#6.3)

#### 阅读笔记
require在lua最初的实现，见下面第一个链接。

lua利用require这类高级函数来加载和运行库。require与dofile函数的作用一样，区别有2点：

1. require在路径中搜索文件
2. require会检查文件是否已经加载，避免重复加载。

如果一个搜索路径如下：

```
?;?.lua;c:\windows\?;/usr/local/lua/?/?.lua
```

假设你执行下面的函数加载

```
require('lili')
```

那么lua会尝试按照下面的文件去执行：

```
lili
lili.lua
c:\windows\lili
/usr/local/lua/lili/lili.lua
```

由于lua加载时，会检查传入的modname，也就是virtual names。举例：

```
require"foo"
require"foo.lua"
```

由于路径中存在```?;?.lua``` ，所以foo.lua会被加载2次。lua还将所有已加载的文件保存在一个全局的变量里_LOADED。

如果你在路径末尾，固定一个文件，类似/usr/local/default.lua。那么在每次require都会尝试去加载该文件。

在lua5.3中改进了这个设计。

require函数首先会查看package.loaded表，检查搞modename是否已经加载，如果已加载，就直接返回存储在package.loaded的值。

require会按照package.serachers预定的表中查找加载对应的模块。4个搜索器分别为：

1. package.preload[modname]
2. package.path
3. package.cpath
4. all-in-one loader

#### 参考链接

1. [Chapter 8. Compilation, Execution, and Errors](https://www.lua.org/pil/8.1.html)

### 技术技巧(Tip)

tcpdump的命令格式

```
tcpdump [options] [not] proto dir type
```

按照表格的方式排列：

| tcpdump | options | not  | proto | dir         | type      |
| ------- | ------- | ---- | ----- | ----------- | --------- |
|         | -nn     |      | tcp   | src         | host      |
|         | -vvv    |      | udp   | dst         | net       |
|         | -XX     |      | arp   | src and dst | port      |
|         | -i      |      | ip    | src or dst  | portrange |
|         | -c      |      | ether |             |           |
|         | -e      |      | icmp  |             |           |

- 关于 proto：可选有 ip、arp、rarp、tcp、udp、icmp、ether 等，默认是所有协议的包
- 关于 dir：可选有 src、dst、src or dst、src and dst，默认为 src or dst
- 关于 type：可选有 host、net、port、portrange（端口范围，比如 21-42），默认为 host
- 关于options：-nn表示不解析主机名和端口，直接用端口号显示，默认显示是端口号对应的服务名
- -vvv输出详细信息（比如 tos、ttl、checksum等）
- -X同时用 hex 和 ascii 显示报文内容
- -XX 同 -X，但同时显示以太网头部
- -i 指定监听的网卡， `-i any` 显示所有网卡
- -c 指定要抓取包的数量
- -e 打印链接级别的标题，例如以太网的mac地址。

主要关注3个过滤器，分别为协议proto、传输方向 dir、类型type。

抓取主机 192.168.1.4上所有收到dst_ip和src_ip的所有数据包

```
sudo tcpdump host 192.168.1.4
```

抓取所有端口，显示IP地址

```
sudo tcpdump -nS
```

抓取经过指定interface，并且dst_net或src_net是172.18.82

```
sudo tcpdump -i eth0 net 172.18.82
```

抓取某协议的数据包

```
tcpdump -i eth0 tcp
```

#### 参考链接

1. [Linux 网络命令必知必会之 tcpdump，一份完整的抓包指南请查收！](https://app.yinxiang.com/Home.action#n=69987a39-378e-494c-8948-f3e9a978568e&s=s59&ses=4&sh=2&sds=5&)

### 分享(Share)

####[从概念到底层技术，一文看懂区块链架构设计](https://www.8btc.com/article/106022) 

#### 阅读笔记

文章非常详细的介绍了区块链架构设计。可以简单分为三层：

| 层级   | 功能点             | 备注   |
| ---- | --------------- | ---- |
| 应用层  | 钱包客户端           |      |
|      | 交易网站            |      |
|      | 第三方扩展           |      |
|      | OTC买卖           |      |
| 扩展层  | 智能合约            |      |
|      | 各种测链应用          |      |
|      | 文档，图片，视频等用户数据存储 |      |
| 协议层  | 网络层             | 共识算法 |
|      | 存储层             | 区块   |

常用编程语言

| 区块链            | 特点                                      | 备注   |
| -------------- | --------------------------------------- | ---- |
| 比特币            | 开发语言C++                                 |      |
|                | 源码 https://github.com/bitcoin           |      |
| 以太坊            | 开发语言Go                                  |      |
|                | 源码 https://github.com/ethereum/pyethapp |      |
| 超级账本HyperLeger | 开发语言Go                                  |      |
|                | 源码 https://github.com/hyperledger       |      |

#### 参考链接

1. [区块链架构设计和知识图谱](https://github.com/imfly/bitcoin-on-nodejs/blob/master/1-%E4%BA%86%E8%A7%A3%E5%8C%BA%E5%9D%97%E9%93%BE/8-%E5%8C%BA%E5%9D%97%E9%93%BE%E6%9E%B6%E6%9E%84%E8%AE%BE%E8%AE%A1%E5%92%8C%E7%9F%A5%E8%AF%86%E5%9B%BE%E8%B0%B1.md)