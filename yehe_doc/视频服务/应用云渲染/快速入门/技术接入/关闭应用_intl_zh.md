## 关闭应用
本节主要介绍如何主动关闭云应用。建议业务及时释放并发资源，更合理利用并发资源。

### 时序图
![](https://qcloudimg.tencent-cloud.cn/raw/403c7649a628776ffdc0b12fbfee85f1.jpg)

### 步骤说明
1. 业务客户端向业务后台主动请求关闭应用。
2. 业务后台通过云渲染 API 调用 [DestroySession](https://intl.cloud.tencent.com/document/product/1158/49967) 销毁会话，业务云端应用将被主动关闭，业务客户端断开与云应用连接。
