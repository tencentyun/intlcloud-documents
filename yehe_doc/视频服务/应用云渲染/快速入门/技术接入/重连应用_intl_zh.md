## 重连应用
本节主要介绍如何重连应用。当用户直接关闭客户端而未主动调用关闭应用功能时，业务可以通过再次调用申请并发和创建会话接口实现重连应用功能。
### 时序图
![](https://qcloudimg.tencent-cloud.cn/raw/01990988def83c87a9e35693ebcf857e.jpg)

### 步骤说明
1. 业务客户端关闭后会断开与业务云端应用的连接，若非主动调用接口关闭云端应用，则默认保持 90s 的重连时间等待重连。
2. 业务客户端重新打开后，通过传入相同的 UserId 向业务后台请求启动应用，若 UserId 不同则不能实现重连功能。
3. 业务后台通过云渲染 API 调用 [ApplyConcurrent()](https://intl.cloud.tencent.com/document/product/1158/49969) 申请锁定并发，根据并发状态进行如下处理：
	- 用户上次连接并发还未回收，返回上一次连接并发资源。
	- 用户上次连接并发已回收，返回新并发资源。
4. 业务后台通过云渲染 API 调用 [CreateSession()](https://intl.cloud.tencent.com/document/product/1158/49968)  创建会话，将返回的服务端 ServerSession 回传给业务客户端，重新启动应用。
