### 客户端 Native SDK 需要配置哪些端口或域名为白名单？

防火墙端口如下表所示：

|  TRTC SDK（Native） | 白名单项目 |
|---------|---------|
| TCP 端口 | 443、20166、10443、10444、10445、10446、10447、10448、10449、10450、10451、13275、23275、33000、37528 |
| UDP 端口 | 8000、8080、8001、8002、8003、8004、8005、8006、8007、8008、8009、16285、9000 |

域名白名单：

```
intl-query.trtc.tencent-cloud.com
intl-accelerate.trtc.tencent-cloud.com
trtc-client-log-overseas-1258344699.cos.ap-singapore.myqcloud.com
intl-sdklog.trtc.tencent-cloud.com
sdkdc.live.qcloud.com
speedtestint.trtc.tencent-cloud.com
intl-query.trtc.tencent-cloud.com
hwapi.im.qcloud.com
videoapi-sgp.im.qcloud.com
trtc-sdk-config-1258344699.file.myqcloud.com   
```

 
### WebRTC 需要配置哪些端口或域名为白名单？

防火墙端口如下表所示：

| WebRTC（H5） | 白名单项目 |
|---------|---------|
| TCP 端口 | 8687 |
| UDP 端口 | 8000；8080；8800；843；443；16285 |

域名白名单：

```
intl-signaling.rtc.qq.com
intl-signaling.rtc.qcloud.com
intl-schedule.rtc.qq.com
intl-schedule.rtc.qcloud.com
videoapi-sgp.im.qcloud.com
```

### TRTC web 端内网环境怎么设置代理？
可采用 Nginx+coturn 代理方案，详情请参见 [企业内网代理方案](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-34-advanced-proxy.html)。

| 方案名 | 适用场景                             | 网络要求                          |
| :----- | :----------------------------------- | :-------------------------------- |
| 方案一 | 允许客户端访问特定的外网代理服务器   | 允许客户端访问外网的 proxy server |
| 方案二 | 允许客户端通过内网代理服务器访问外网 | 允许 proxy server 访问外网        |


