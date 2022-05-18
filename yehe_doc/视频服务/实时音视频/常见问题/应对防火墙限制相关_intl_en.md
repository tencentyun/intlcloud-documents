### What ports and domain names should I add to the allowlist of my firewall for a native SDK?

Add the following ports to the allowlist:

|  TRTC SDK (Native) | Ports |
|---------|---------|
| TCP | 443, 20166, 10443, 10444, 10445, 10446, 10447, 10448, 10449, 10450, 10451, 13275, 23275, 33000, 37528 |
| UDP | 8000, 8080, 8001, 8002, 8003, 8004, 8005, 8006, 8007, 8008, 8009, 16285, 9000 |

Add the following domain names to the allowlist:

```
cloud.tim.qq.com
gz.file.myqcloud.com
avc.qcloud.com
yun.tim.qq.com
dldir1.qq.com
mlvbdc.live.qcloud.com
query.tencent-cloud.com
*.trtc.tencent-cloud.com        
```

 
### What ports and domain names should I add to the allowlist of my firewall for WebRTC?

Add the following ports to the allowlist:

| WebRTC (H5) | Ports |
|---------|---------|
| TCP | 8687 |
| UDP | 8000, 8080, 8800, 843, 443, 16285 |

Add the following domain names to the allowlist:

```
*.rtc.qcloud.com
*.rtc.qq.com
yun.tim.qq.com
```

### How do I configure proxies for clients to access the TRTC SDK for web from a private network?
You can use the Nginx + Coturn scheme. For detailed directions, see [Proxy Configuration for Corporate Private Networks](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-34-advanced-proxy.html).

| Solution | Application Scenario                             | Network Requirements                          |
| :----- | :----------------------------------- | :-------------------------------- |
| Solution 1 | Allow clients to access specific proxy servers in the public network      | Allow clients to access the proxy servers configured in the public network |
| Solution 2 | Allow clients to access the public network via proxy servers configured in the private network | Allow the proxy servers to access the public network        |


