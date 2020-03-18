Some customers have restrictions placed on public network access by their own companies, so they need to be added to a firewall whitelist before they can get access. The following describes the related rules:

## Client Native SDK

Firewall port:

|  TRTC SDK (Native) | Whitelisted items |
|---------|---------|
| TCP port | 443 |
| UDP port | 8000 |

Domain name whitelist:

```
official.opensso.tencent-cloud.com

query.tencent-cloud.com

yun.tim.qq.com
```

 
## WebRTC

Firewall port:

| WebRTC (H5) | Whitelisted items |
|---------|---------|
| TCP port | 8687 |
| UDP port | 8000; 8800; 843; 443 |

Domain name whitelist:

```
qcloud.rtc.qq.com
```


## WeChat Mini Program

&lt;webrtc - room&gt; domain name whitelist:

```
https://official.opensso.tencent-cloud.com

https://yun.tim.qq.com

https://intl.cloud.tencent.com

https://webim.tim.qq.com
```


>! Tencent Cloud server IP addresses are dynamically updated, with no fixed batch of IP addresses, so we cannot provide you with a list of fixed IPs.
