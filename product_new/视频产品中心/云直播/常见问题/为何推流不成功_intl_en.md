
If you follow the steps in [Best Practice - LVB Push](https://cloud.tencent.com/document/product/267/32732) but still find that push is not successful, please troubleshoot common push issues as instructed in this document.

### Why does a push fail?
#### 1. Is the CNAME record of your domain name resolved to a Tencent Cloud address?
 Only when the CNAME record of your push domain name is resolved to a Tencent Cloud address can a push succeed. You can check whether the created push domain name has a CNAME record in **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**. There is a CNAME title bar that can be used to check whether a CNAME record is present, and if yes, a screen like the one below will appear:
![](https://main.qcloudimg.com/raw/925d5353b6080cb724b0dbca07fec7d3.png)
If you don't have a CNAME record, you can configure one as instructed in [CNAME Configuration](https://cloud.tencent.com/document/product/267/30560).

#### 2. Is the network normal?
The default port used by RTMP push is **1935**. If the firewall of your network does not open port 1935 during test, you will encounter a problem connecting to the server. In this case, you can check whether the problem is caused by this reason by switching to another network (such as 4G).

#### 3. Has `txTime` expired?
Some users are worried that their live broadcasting traffic will be compromised, so they set `txTime` to a very small value such as 5 minutes after the current time. In fact, as there is a `txSercet` signature, the validity period of `txTime` need not be too short. Instead, if the validity period is too short, when a host encounters network jitters during a live broadcast, the push cannot be resumed because the push URL expires.
You are recommended to set `txTime` to 12 or 24 hours after the current time, i.e., longer than the duration of a normal live broadcast.

#### 4. Is `txSecret` correct?
Tencent Cloud currently requires that hotlink protection be enabled for all push URLs and will **kick out** those with incorrect or expired hotlink protection settings. In this case, the LVB SDK will throw a **PUSH_WARNING_SERVER_DISCONNECT** event.
For more information on how to get a reliable push URL, please see [Best Practice - LVB Push](https://intl.cloud.tencent.com/document/product/267/31558).

#### 5. Is the push URL occupied?
One push URL can have only one push client at a time, and a second client that tries to push with it will be rejected by Tencent Cloud. In this case, you can log in to the LVB Console and check whether the stream is already being pushed in **[Stream Management](https://console.cloud.tencent.com/live/streammanage)** > **Online Stream**. You can also check whether the stream is forbidden in **Forbidden Stream**.


