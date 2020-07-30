Some customers have restrictions placed on public network access by their own companies, so they need to be added to a firewall allowlist before they can get access. The following describes the related rules:

### What ports or domain names do I need to add to the allowlist of native SDK for client?

The firewall ports are as follows:

|  TRTC SDK (Native) | Allowed Items |
|---------|---------|
| TCP port | 443; 20166 |
| UDP port | 8000 |

Domain name allowlist:

<pre>
cloud.tim.qq.com
gz.file.myqcloud.com
avc.qcloud.com
yun.tim.qq.com
dldir1.qq.com
mlvbdc.live.qcloud.com
query.tencent-cloud.com
</pre>

 
### What ports or domain names do I need to add to the allowlist of WebRTC?

The firewall ports are as follows:

| WebRTC (H5) | Allowed Items |
|---------|---------|
| TCP port | 8687 |
| UDP port | 8000; 8800; 843; 443 |

Domain name allowlist:

<pre>
qcloud.rtc.qq.com
</pre>


### What domain names do I need to add to the allowlist of WeChat Mini Program?

&lt;trtc-room&gt; domain name allowlist:

<pre>
https://official.opensso.tencent-cloud.com
https://yun.tim.qq.com
https://cloud.tencent.com
https://webim.tim.qq.com
https://query.tencent-cloud.com
</pre>


>Tencent Cloud server IP addresses are dynamically updated, with no fixed batch of IP addresses, so we cannot provide you with a list of fixed IPs.
