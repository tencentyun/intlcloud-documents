### Why do security baseline alerts disappear?
The number following an alert type indicates the number of alerts not processed. (BOT Attack displays the number of all alerts.) If the security baseline alert feature is not enabled, the console will not display the security baseline option.
### Why is an IP address banned after interception?
Intrusion defense detects network attacks for sessions. Only when an IP is banned (added to the blocklist), all its access operations will be blocked.
### How can I modify a blocked or ignored event?
Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/warncenter), enter the [Intrusion Protection System](https://console.cloud.tencent.com/cfw/ips) module, and then you can remove an event from the "Blocklist" or "Ignored list".
![](https://qcloudimg.tencent-cloud.cn/raw/67d0377695b5ecc716a2f971f596460c.png)

### How can I view the threat profile of a specified IP address?
 - For a security event alert, you can view the threat profile in [Security event alert - Event details](https://intl.cloud.tencent.com/document/product/1160/49816#keshihua).
![](https://qcloudimg.tencent-cloud.cn/raw/b775ea6a1adda66810059eb879f833da.png)
 - In "Blocked statistics", you can directly click the **IP address** to redirect to details.
![](https://qcloudimg.tencent-cloud.cn/raw/423da91d0ac27dcae05375c029d2e141.png)

### Why is an IP address following a red exclamation mark?
It means that this IP address may be a Tencent Cloud CDN address, which is not advised to be manually blocked or banned. If you have enabled the Block mode of IPS, CFW will automatically block attacks from this address. Normal traffic will not be affected.

### How frequently will data in Alert Management be updated?
Data in Alert Management will be updated every 10 minutes.

### What should I do to display the traffic trend chart in Alert Management?
1. On the [Firewall toggle](https://console.cloud.tencent.com/cfw/switch) page, select an instance, click **Firewall toggle** -> **OK** to enable the firewall toggle.
2. After the firewall toggle is enabled, CFW ACL is in "All-pass" mode and intrusion defense is "Observe" mode by default. There is no impact on your service system.

### Why is there no blocking data in Alert Management?
1. Check whether you have enabled the firewall toggle and set it to block or interception mode.
2. Select all policies for blocking data, and then check whether you can view corresponding events.
3. If you still fail to view corresponding events, [contact us](https://intl.cloud.tencent.com/contact-us) for help.

### Can I receive bandwidth alerts if primary account and sub-account are not configured as alert objects in Alert Management?
If no primary account or sub-account is selected for receiving alerts, you will not be notified via SMS from Alert Management, or Message Center. However, alerts will still be displayed on the console.
