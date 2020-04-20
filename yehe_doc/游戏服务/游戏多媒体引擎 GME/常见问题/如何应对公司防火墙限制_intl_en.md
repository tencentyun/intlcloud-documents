If your organization has restrictions placed on public network access, you need to configure the firewall whitelist accordingly before you can get access. The following describes the relevant rules:

## Client Native SDK (v2.2 or Above)

Firewall port:

| Port Type | Whitelist Item |
|---------|---------|
| TCP port | 443 |
| UDP port | 8000 |


Domain name whitelist:
```
tcloud.tim.qq.com
gmeconf.qcloud.com
yun.tim.qq.com
```

> 
- Tencent Cloud server IP addresses are dynamically updated, so we cannot provide you with a list of fixed IPs.
- To use the GME SDK on Windows XP, you need to add the following items to the firewall whitelist:

| Port Type | Whitelist Item |
|---------|---------|
| TCP port | 15000 |

Domain name whitelist:

```
cloud.tim.qq.com
openmsf.3g.qq.com
```


## Using the SDK for HTML5

Firewall port:

| Port Type | Whitelist Item |
|---------|---------|
| TCP port | 443, 8687 |
| UDP port | 8000, 8800, 843, 443 |

Domain name whitelist:

```
qcloud.rtc.qq.com
rtc.qcloud.qq.com
```


## Using Voice Messaging and Speech-to-Text Conversion Service

Firewall port:

| Port Type | Whitelist Item |
|---------|---------|
| TCP port | 80, 443 |

Domain name whitelist:

```
gmespeech.qcloud.com
yun.tim.qq.com
gmeconf.qcloud.com
```
