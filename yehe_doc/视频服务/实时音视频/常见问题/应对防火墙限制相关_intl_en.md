### What ports and domain names should I add to the allowlist of my firewall for a native SDK?

Add the following ports to the allowlist:

|  TRTC SDK (Native) | Ports |
|---------|---------|
| TCP | 443, 20166, 10443, 10444, 10445, 10446, 10447, 10448, 10449, 10450, 10451, 13275, 23275, 33000, 37528 |
| UDP | 8000, 8080, 8001, 8002, 8003, 8004, 8005, 8006, 8007, 8008, 8009, 16285, 9000 |

Add the following domain names to the allowlist:

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

 
### What ports and domain names should I add to the allowlist of my firewall for WebRTC?

Add the following ports to the allowlist:

| WebRTC (H5) | Ports |
|---------|---------|
| TCP | 8687 |
| UDP | 8000, 8080, 8800, 843, 443, 16285 |

Add the following domain names to the allowlist:

```
intl-signaling.rtc.qq.com
intl-signaling.rtc.qcloud.com
intl-schedule.rtc.qq.com
intl-schedule.rtc.qcloud.com
videoapi-sgp.im.qcloud.com
```

### How do I configure proxies for clients to access the TRTC SDK for web from a private network?
You can use the Nginx + Coturn scheme. For detailed directions, see [Proxy Configuration for Corporate Private Networks](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-34-advanced-proxy.html).

| Solution | Application Scenario                             | Network Requirements                          |
| :----- | :----------------------------------- | :-------------------------------- |
| Solution 1 | Allow clients to access specific proxy servers in the public network      | Allow clients to access the proxy servers configured in the public network |
| Solution 2 | Allow clients to access the public network via proxy servers configured in the private network | Allow the proxy servers to access the public network        |


