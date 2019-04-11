## ARTS(week15)

### 算法题(Algorithm)

[有效的字母异位词](https://github.com/geekwho11/learn.leetcode.xbcme/tree/master/php/src/242.valid-anagram)

### 阅读点评(Review)

#### [CI CD Pipeline: Learn How to Setup a CI CD Pipeline From Scratch](https://medium.com/edureka/ci-cd-pipeline-5508227b19ca)

#### 阅读笔记

DevOps=Development+Operations

CI=Continuous Integration

CD=Continuous Delivery+Continuous Deployment

CI/CD流水线实现：

1. 自动构建
2. 自动测试
3. 自动部署

##### 什么是DevOps

DevOps是一种软件开发方法，贯穿于软件的整个生命周期，包括持续开发、持续测试、持续集成、持续部署、持续监控等。

| CI/CD流水线             | 阶段      |      |
| -------------------- | ------- | ---- |
| VERSION CONTROL      | 版本管理    |      |
| BUILD                | 构建      |      |
| UNIT TEST            | 测试      |      |
| DEPLOY               | 部署      |      |
| AUTO TEST            | 自动测试    |      |
| DEPLOY TO PRODUCTION | 部署到生产环境 |      |
| Measure+Validate     | 线上验证验收  |      |

#### 参考链接

1. [如何从零开始搭建 CI/CD 流水线](https://www.infoq.cn/article/WHt0wFMDRrBU-dtkh1Xp)
2. [基于Gitlab CI搭建持续集成环境](https://www.jianshu.com/p/705428ca1410)

### 技术技巧(Tip)

在多平台开发多会遇到Git的换行符问题，现总结整理下：

| 平台         | 换行符                 | 备注                   |
| ---------- | ------------------- | -------------------- |
| Unix/Linux | ```0x0A(LF) ```     |                      |
| Mac OS     | ```0x0A(LF) ```     | 曾经是 ``` 0x0D(CR) ``` |
| Windows    | ```0x0D0A(CRLF) ``` |                      |

Git的autocrlf选项

- **true:** 提交时转换为 LF，检出时转换为 CRLF
- **false:** 提交检出均不转换
- **input:** 提交时转换为LF，检出时不转换

Git的safecrlf选项

- **true:** 拒绝提交包含混合换行符的文件
- **false:** 允许提交包含混合换行符的文件
- **warn:** 提交包含混合换行符的文件时给出警告

建议跨平台最好统一的换行符LF。

```
$ git config --global core.autocrlf input
$ git config --global core.safecrlf true
```

#### 参考链接

1. [Git 多平台换行符问题](http://blog.konghy.cn/2017/03/19/git-lf-or-crlf/)

### 分享(Share)

#### [支付宝架构师眼中的高并发架构](https://mp.weixin.qq.com/s?__biz=MzAxNjk4ODE4OQ==&mid=2247485433&idx=1&sn=88e5531beb0ef862462e448dbdcd01ce&chksm=9bed268bac9aaf9dc7612ebf7b1e4a146d4cf9dd8a7a8dfca3bf59f3414813e0109d99093129&mpshare=1&scene=1&srcid=0404C0YpryJDhxzYiLcrXwWn#rd)

#### 阅读笔记

文章列举常见架构方案，基本可以应对常见的业务场景。总结下来有几点：

1. 采用Redis等缓存集群，缓存绝大部分的日常变动较小的数据。
2. 高并发事实业务，采用消息队列异步化处理落地到数据库。