
### 使用游戏多媒体引擎实时语音，流量消耗是多少？
如果使用流畅音质，码率为30kbps，标准音质和高清音质码率为64kbps。流量和码率有关，也和房间内通话人数有关，计算公式为： 码率 x 人数 / 8 = 字节。

### 进房时出现7004错误码，提示网络错误，如何解决？
问题排查的步骤如下：
1. 查看并确认进房 API 中的参数，例如 AppId， UIN， AuthBuffer 的合法性（详情请参见各平台 [接口文档](https://intl.cloud.tencent.com/zh/document/product/607/18522)）。
2. 检查开发者测试设备是在开发者内网环境还是外网环境，如果是内网环境，请参见 [如何应对公司防火墙限制](https://intl.cloud.tencent.com/document/product/607/35232)。
3. 根据下面网络问题排查方法进行排查。

### 出现网络问题，该如何排查？

- **网络诊断**
	- [单击检查域名 tcloud.tim.qq.com](https://ping.huatuo.qq.com/tcloud.tim.qq.com)
	- [单击检测域名 gmeconf.qcloud.com](https://ping.huatuo.qq.com/gmeconf.qcloud.com)
	- [单击检测域名 yun.tim.qq.com](https://ping.huatuo.qq.com/yun.tim.qq.com )

请在出现网络问题的机器上，使用浏览器分别打开以上三个链接，等待检测执行完毕（预计5 - 10秒），单击**复制结果 URL 分享**，并 [提交工单](https://console.cloud.tencent.com/workorder/category) 联系专业工作人员进行处理。
![](https://main.qcloudimg.com/raw/0b540f4bf6222c6b9548b148496a15bb.png)

- **诊断 SSO**
请在出现网络问题的机器上，[单击检查域名 tcloud.tim.qq.com](https://tcloud.tim.qq.com)，查看显示内容，截图或者将显示内容拷贝下来，并 [提交工单](https://console.cloud.tencent.com/workorder/category) 联系专业工作人员进行处理。
示例代码如下：
```
{"ActionStatus":"FAIL","ErrorCode":60002,"ErrorInfo":"HTTP parse Error"}
```
