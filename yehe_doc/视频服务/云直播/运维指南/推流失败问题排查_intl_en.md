
If you follow the steps in [Best Practice - Live Push](https://intl.cloud.tencent.com/document/product/267/31558) but still find that the push is not successful, please troubleshoot common push issues as instructed in this document.

### 1. Check whether a CNAME record that points to a Tencent Cloud address has been configured for your domain name.
Your push can succeed only if your domain name has a CNAME record that points to a Tencent Cloud address. You can check whether an added push domain name has a CNAME record in the **CNAME** column of **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**. You will see a green check if the CNAME record is configured, as shown below:
![](https://main.qcloudimg.com/raw/ebb055071447bc55c2f17e60ab8d0b75.png)
If your domain name does not have a CNAME record, you can [configure one](https://intl.cloud.tencent.com/zh/document/product/267/31057).
	

### 2. Check whether the network is normal.
RTMP push uses the **1935** port by default. If the port is not enabled on the firewall of the network for testing, you will be unable to connect to the server. You can check whether this issue caused the push failure by switching to another network (a 4G network for example).

### 3. Check whether the validity period of the push URL is too short.
To prevent the traffic from being stolen, some clients may set `txTime` (the validity period of the push URL) to a very short period, such as 5 minutes from the current time. This is unnecessary as the `txSercet` signature guarantees security. If the validity period is too short, the push URL may expire after a live stream is interrupted due to network disconnection, and consequently the push cannot be resumed.
You are advised to set `txTime` to 12 or 24 hours from the current time, longer than a common live streaming session.

### 4. Check whether `txSecret` is correct.
To ensure security, Tencent Cloud requires configuring hotlink protection for all push URLs and **rejects** all hotlink protection URLs that have expired or are miscalculated. If a push is rejected, the CSS SDK will throw a **PUSH_WARNING_SERVER_DISCONNECT** event.
![](https://main.qcloudimg.com/raw/00c846dda473ee0dd241ffe89554849b.jpg)
See [Best Practice > Live Push](https://intl.cloud.tencent.com/document/product/267/31558) for how to get reliable push URLs.

### 5. Check whether the push URL is occupied.
A push URL can be used by only one client at a time. A second client trying to push using the URL will be rejected by Tencent Cloud. You can log in to the CSS console and check whether a stream is already being pushed in **[Stream Management](https://console.cloud.tencent.com/live/streammanage)** > **Live Streams**. You can also check whether a stream is disabled in **Disabled Streams**.

 
