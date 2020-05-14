If your organization has restrictions placed on public network access, you need to configure the firewall whitelist accordingly before you can get access. The following describes the relevant rules:

## Native Client SDK

The firewall ports are as follows:

| TRTC SDK (Native) | Whitelisted Item |
|---------|---------|
| TCP port | 443, 20166 |
| UDP port | 8000 |

Domain name whitelist:

```
cloud.tim.qq.com
gz.file.myqcloud.com
avc.qcloud.com
yun.tim.qq.com
dldir1.qq.com
mlvbdc.live.qcloud.com
```

 
## WebRTC

The firewall ports are as follows:

| WebRTC (HTML5) | Whitelisted Item |
|---------|---------|
| TCP port | 8687 |
| UDP port | 8000, 8800, 843, 443 |

Domain name whitelist:

```
qcloud.rtc.qq.com
```


## WeChat Mini Program

&lt;webrtc - room&gt; domain name whitelist:

```
https://official.opensso.tencent-cloud.com

https://yun.tim.qq.com

https://cloud.tencent.com

https://webim.tim.qq.com
```


>Tencent Cloud server IP addresses are dynamically updated, so we cannot provide you with a list of fixed IPs.
