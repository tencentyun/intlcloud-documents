
If you are unable to push streams despite having followed the steps in [Best Practice - LVB Push](https://intl.cloud.tencent.com/document/product/267/31558), try troubleshooting the issue by checking the common reasons for push failure listed in this document.

### 1. Have you created a CNAME record that points to a Tencent Cloud address for your domain name?
Your push can succeed only if your domain name has a CNAME record that points to a Tencent Cloud address. You can check whether a push domain name created has a CNAME record in the “CNAME” column of **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**. The domain names in the figure below have CNAME records.
If your domain name does not have a CNAME record, you can add one for it by following the steps in [Configuring CNAME for Domain Name](https://intl.cloud.tencent.com/document/product/267/31057).
	

### 2. Is the network normal?
RTMP push uses the **1935** port by default. If the port is not open in the firewall of the network you use for testing, you will be unable to connect to the server. You can check whether this is what causes your push failure by switching to another network, for example, 4G.

### 3. Is the validity period of the push URL set too short?
Some clients may be too cautious when setting `txTime`. For example, they may set `txTime` 5 minutes from the current time to prevent their traffic from being stolen. As a matter of fact, this is not necessary given the presence of the `txSercet` signature. If the validity period is set too short, after a host is disconnected due to network problems during a live broadcast, it may be impossible to resume the push due to expiration of the push URL.
You are recommended to set `txTime` to a point 12 or 24 hours from the current time, longer than the duration of a typical LVB.

### 4. Is `txSecret` correct?
To ensure security, Tencent Cloud requires hotlink protection for all push URLs and **rejects** expired URLs and those with miscalculated hotlink protection keys. When push is rejected, the LVB SDK throws a **PUSH_WARNING_SERVER_DISCONNECT** event, and the LVB SDK demo acts as follows:
See [Best Practice > LVB Push](https://intl.cloud.tencent.com/document/product/267/31558) for how to get reliable push URLs.

#### 5. Is the push URL occupied?
A push URL can have only one push client at a time. A second client trying to push with it will be rejected by Tencent Cloud. You can log in to the LVB console and check whether the stream is already being pushed in **[Streaming Management](https://console.cloud.tencent.com/live/streammanage)** > **Live Stream**. You can also check whether the stream is forbidden in **Forbidden Streams**.

 

