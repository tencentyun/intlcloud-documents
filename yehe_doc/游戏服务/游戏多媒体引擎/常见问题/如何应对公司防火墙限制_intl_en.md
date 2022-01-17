If your organization has restrictions placed on public network access, you need to configure the firewall allowlist accordingly before you can get access. The following describes the relevant rules:

### Client Native SDK (v2.2 or Above)

**Firewall port:**

| Port Type | Allowed Item |
|---------|---------|
| TCP port | 443 |
| UDP port | 8000 |


**Domain name allowlist:**
```
tcloud.tim.qq.com
gmeconf.qcloud.com
yun.tim.qq.com
```

>!
> - Tencent Cloud server IP addresses are dynamically updated, so we cannot provide you with a list of fixed IPs.
> - To use the GME SDK on Windows XP, you need to add the following items to the firewall allowlist:

**Firewall port:**

| Port Type | Allowed Item |
|---------|---------|
| TCP port | 15000 |

**Domain name allowlist:**

```
cloud.tim.qq.com
openmsf.3g.qq.com
```


### Using the SDK for HTML5

**Firewall port:**

| Port Type | Allowed Item |
|---------|---------|
| TCP port | 443, 8687 |
| UDP port | 8000, 8800, 843, 443 |

**Domain name allowlist:**

```
qcloud.rtc.qq.com
rtc.qcloud.qq.com
```


### Using Voice Messaging and Speech-to-Text Conversion Service

**Firewall port:**

| Port Type | Allowed Item |
|---------|---------|
| TCP port | 80, 443 |

**Domain name allowlist:**

```
gmespeech.qcloud.com
yun.tim.qq.com
gmeconf.qcloud.com
```
