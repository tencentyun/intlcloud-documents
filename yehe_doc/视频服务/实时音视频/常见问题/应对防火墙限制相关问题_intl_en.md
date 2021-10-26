### What ports and domain names should I add to the allowlist of my firewall for a native SDK?

Allowlist the following ports:

|  TRTC SDK (Native) | Ports |
|---------|---------|
| TCP port | 443, 20166 |
| UDP port | 8000, 8080, 16285, 9000 |

Allowlist the following domain names:

```
cloud.tim.qq.com
gz.file.myqcloud.com
avc.qcloud.com
yun.tim.qq.com
dldir1.qq.com
mlvbdc.live.qcloud.com
query.tencent-cloud.com
```


### What ports and domain names should I add to the allowlist of my firewall for WebRTC?

Allowlist the following ports:

| WebRTC (H5) | Ports |
|---------|---------|
| TCP port | 8687 |
| UDP port | 8000, 8080, 8800, 843, 443, 16285 |

Allowlist the following domain names:

```
qcloud.rtc.qq.com
```

### How do I configure proxies for clients to access the TRTC SDK for web from a private network?
You can use the Nginx + Coturn solutions.

| Solution | Application Scenario                             | Network Requirements                          |
| :----- | :----------------------------------- | :-------------------------------- |
| Solution 1 | Allow clients to access specific proxy servers in the public network      | Allow clients to access proxy servers in the public network |
| Solution 2 | Allow clients to access the public network via proxy servers in their private network | Allow proxy servers to access the public network        |




### What domain names should I add to the allowlist of my firewall for WeChat Mini Program?

Allowlist the following &lt;trtc-room&gt; domain names:

```
https://official.opensso.tencent-cloud.com
https://yun.tim.qq.com
https://cloud.tencent.com
https://webim.tim.qq.com
https://query.tencent-cloud.com
```


>!Tencent Cloud updates its server IP addresses dynamically and therefore cannot offer you a list of fixed IP addresses.
