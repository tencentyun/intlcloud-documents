
### MongoDB 连接断开怎么操作？
请参见 [连接实例](https://intl.cloud.tencent.com/document/product/240/7092) 排除认证问题。

### MongoDB 出现“Remote server has closed the connection”信息？
首先参见 [连接实例](https://intl.cloud.tencent.com/document/product/240/7092) 排除认证问题 ，如果能连上但是依然会出现这个问题，可能需要实现一个重连机制，详情参见 [重连示例](https://intl.cloud.tencent.com/document/product/240/4980)。

### WiredTiger 3.2 存在锁表问题，云版本 MongoDB 是否存在类似问题？
需要根据具体问题分析，例如默认建索引肯定会加全局锁，以及用户执行 fsynclock 命令也是会加锁的。
锁是数据库的一个功能，处理并发访问的一系列问题，正常的加锁是必须的，只要不影响业务正常运行就可以。

### MongoDB 应该选哪个版本的驱动程序？
推荐使用最新版本，例如 PHP 可以选择 mongo-1.6 及以上。
 
### MongoDB 提供哪些语言连接方式？
云数据库 MongoDB 提供多种语言连接方式，例如 Shell、PHP、Node.js、Java、Python，详情请参见 [连接实例](https://intl.cloud.tencent.com/document/product/240/7092)。

### 云数据库 MongoDB 版支持哪些语言的客户端进行连接？
云数据库 MongoDB 版针对客户端连接完全兼容 MongoDB，只要是官方 MongoDB 版支持的客户端，云数据库全部支持。例如 C、C++、C#、Java、Node.js、Python、PHP、Perl 等，详情请参见 [MongoDB 官方文档](https://docs.mongodb.org/ecosystem/drivers/)。

### 在 shell 里怎么连接腾讯云 MongoDB？
详情请参见 [Shell 连接实例](https://intl.cloud.tencent.com/zh/document/product/240/3978)。

### 业务程序里连接 MongoDB 的 URI 是什么样的？
详情请参见 [连接实例](https://intl.cloud.tencent.com/document/product/240/7092)。

### 用 meteor 等各类框架、类库无法连接腾讯云 MongoDB，如何处理？
一般来说都是连接方式、URI 拼接错误，请先检查核实。

### 在 PHP 中，如何设置 MongoDB 最大连接数？
MongoDB 驱动（[PHP 官网文档](http://php.net/manual/en/set.mongodb.php)）可以通过在连接 URL 中配置 maxPoolSize 参数控制连接数。
MongoDB 驱动（[PHP 官网文档](http://php.net/manual/en/set.mongodb.php)）可以通过 Mongo::setPoolSize() 方法设置连接数。
### MongoDB 连接数限制是多少？
请参见 [连接数限制](https://intl.cloud.tencent.com/document/product/240/31183)。


### 手动重连 MongoDB 怎么操作？
腾讯云 MongoDB 数据库服务提供的不是简单的 mongod 访问，给到用户访问的是一个负载均衡 IP，此 IP 后面是连接到一系列类似 mongos 一样存在的路由接入层。
客户端驱动会透过负载均衡 IP 与接入机建立一个长连接，当此连接处于长期间活跃状态时，腾讯云不会对其做任何干预，但是当长连接闲置时间超过1天时（此时间会随着版本优化而调整），路由接入层会剔除该连接。
一般来说，客户端驱动会实现一个自动重连的过程，但是也有部分语言的驱动并没有实现。对于没有实现自动重连的语言驱动，当用户使用一个已经被剔除的连接来尝试与腾讯云 MongoDB 服务通信时可能会得到 “Remote server has closed the connection” 之类的错误信息，所以需要手动进行重连，这里给出一个 PHP 重连的 demo。

**基于 PHP mongo 驱动的重连实现** 
![](https://main.qcloudimg.com/raw/0fcb5ee5ace2c301c2c9061403986d07.png)


### 如何使用 mongoose 连接云数据库 MongoDB？
mongoose 连接腾讯云 MongoDB 参数如下：

``` 
var dbUri = " mongodb:// " + user + " : " +password + " @ " +host + ":" +port + " / " + dbName;

var opts = {
　　auth：｛
　　　　authMechanism : ' MONDODB-CR'
      ｝
}；
var connection = mongodb.createConnection(dbUri, opts);
```

### MongoDB 支持外网连接吗？
MongoDB 目前只支持内网连接，连接方式参见 [连接实例](https://intl.cloud.tencent.com/document/product/240/7092) 。
目前暂不支持开通外网访问，如果您要在本地连接 MongoDB，可以使用与 MongoDB 同一账号同一内网下的服务器做端口转发实现。
 
