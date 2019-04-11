## ARTS(week17)

### 算法题(Algorithm)

[字符串转换整数 (atoi)](https://github.com/geekwho11/learn.leetcode.xbcme/tree/master/php/src/8.string-to-integer-atoi)

### 阅读点评(Review)

#### [PHP Test Driven Development Part 1: Introduction](https://medium.com/@sameernyaupane/php-test-driven-development-part-1-introduction-5483362d79b5)

#### 阅读笔记

TDD = Test Driven Development = 测试驱动开发

测试驱动开发是一种编码实践，通常是先编写测试，然后编写代码通过该测试。

基本步骤如下：

1. 写一个测试
2. 运行该测试，看到它失败
3. 编写实现代码
4. 再次运行测试，直到它通过测试。
5. 重复步骤1

采用TDD的好处有：

1. 你可以非常清楚的了解到可以工作和不能工作的代码。
2. 最小程度减少重构代码所花费的时间。
3. 它使添加新功能变得非常简单
4. 它让程序员充满信心
5. 它可以将软件开发拆分为可以胜任的模块。
6. 它减少了软件变化的增长的成本。

测试的类型

1. 单元测试，通常是测试一个类中的一个方法。
2. 集成测试，测试类之间的依赖，会涉及到多个类
3. 功能测试，测试整个功能是否可用
4. 验收测试，验证开发的功能是否通过

### 技术技巧(Tip)

在PHP中有着保留关键词的列表。所谓保留关键字，就是在PHP解释器看来是有特殊意义的。

| 关键字  | PHP5 | PHP7 | 备注       |
| ---- | ---- | ---- | -------- |
| 常量   | 不允许  | 允许   | 除了class外 |
| 方法名  | 不允许  | 允许   |          |
| 类名   | 不允许  | 允许   |          |
| 变量名  | 允许   | 允许   |          |
| 类属性  | --   | 允许   |          |
|      | --   | 允许   |          |
|      | --   | 允许   |          |

比如，我踩到的坑是

```PHP
function default(){} // PHP5报错 Parse error: syntax error, unexpected T_DEFAULT, expecting T_STRING
function default(){} // PHP7正常
```

#### 参考链接

1. [关键词列表](https://www.php.net/manual/zh/reserved.keywords.php)
2. [Can't have function named default in php](https://stackoverflow.com/questions/10395930/cant-have-function-named-default-in-php)

### 分享(Share)

#### [自学架构设计的一个好方法]([https://mp.weixin.qq.com/s?__biz=Mzg4NjAwMTQzNA==&mid=2247483999&idx=1&sn=c2b3fc86c4c150e1ed6f0824bd7ff8a7&chksm=cfa1182af8d6913cced3d849682adcb1bad3705d043f45925c70348a7e99ad7ad48ac9466a84&mpshare=1&scene=1&srcid=0404AWtsymOXHEQQXgEthQ7Z#rd](https://mp.weixin.qq.com/s?__biz=Mzg4NjAwMTQzNA==&mid=2247483999&idx=1&sn=c2b3fc86c4c150e1ed6f0824bd7ff8a7&chksm=cfa1182af8d6913cced3d849682adcb1bad3705d043f45925c70348a7e99ad7ad48ac9466a84&mpshare=1&scene=1&srcid=0404AWtsymOXHEQQXgEthQ7Z#rd))

#### 阅读笔记

作者给出了一个0基础学习架构的方法：阅读思考开源项目的源代码。

当然，阅读源代码也是有方法论的：

1. 写代码是工程实践，架构师依赖于经验和直觉。
2. 通过文档或书籍了解系统整体架构，然后从一个小的点开始看起。这就像人体的骨骼一样，先了解骨头的分布，作用，原理，然后再去看具体实现。这就好比，王者荣耀的小地图，一般开团前，都会查看小地图，敌方的分布，我方的位置，带着你的蓝图去参战，肯定是事半功倍。不然，你就摸瞎开团。
3. 关注系统的整体设计，比如分层，每一层的组成部分。
4. 层次之间的交互方式，一般是接口，也有队列，共享内存
5. 每个模块接口的设计，接口类型，入口参数和输出类型
6. 系统的核心的数据结构，代码层面的设计模式。
7. 代码里精巧设计的部分，linux内核的红黑树实现，C宏实现的泛型链表操作。
8. 异常处理流程
9. 最好是带着问题和思考去看。
10. 阅读源代码，不能贪心，要以谦卑的心态去学习，刻意练习自己的阅读理解能力。如果可以做笔记的话，就更好了。
11. 工作中，可以尝试与自己工作相关的开源项目。可以学习架构和设计，学到的知识还可以应用到工作中。