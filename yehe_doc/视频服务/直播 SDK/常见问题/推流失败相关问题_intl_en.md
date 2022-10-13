If you follow the steps in [Best Practice > CSS Push](https://intl.cloud.tencent.com/document/product/267/31558) but fail to publish streams, check the common reasons for publishing failure listed in this document to troubleshoot the issue.

[](id:check1)
### 1. Check whether you have configured for your domain name a CNAME record that points to a Tencent Cloud address
Publishing can succeed only if your domain name has a CNAME record that points to a Tencent Cloud address. You can check whether a publishing domain name created has a CNAME record in the **CNAME** column in **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**.

If your domain name does not have a CNAME record, you can add one for it by following the steps in [Configuring CNAME for Domain Name](https://intl.cloud.tencent.com/document/product/267/31057). 
	 
[](id:check2)

### 2. Check whether the network is normal
RTMP publishing uses the **1935** port by default. If the port is not open in the firewall of the network you use for testing, you will be unable to connect to the server. You can check whether this is what caused your publishing failure by switching to another network, for example, 4G.

[](id:check3)
### 3. Check whether the validity period of the publishing URL is too short.
Some clients may be too cautious about `txTime`. For example, they may set `txTime` to 5 minutes from the current time to prevent traffic theft. This is unnecessary given the presence of the `txSercet` signature. If the validity period is too short, if a host is disconnected during a live stream, he or she may be unable to resume publishing due to the expiration of the publishing URL.
You are advised to set `txTime` to 12 or 24 hours from the current time, longer than an average live streaming session.

[](id:check4)
### 4. Check if `txSecret` is correct
To ensure security, Tencent Cloud requires configuring hotlink protection for all push URLs and **rejects** all hotlink protection URLs that have expired or are miscalculated. If a push is rejected, the LVB SDK will throw a **PUSH_WARNING_SERVER_DISCONNECT** event.
See [Best Practice > CSS Push](https://intl.cloud.tencent.com/document/product/267/31558) for how to get reliable publishing URLs.

[](id:check5)
### 5. Check whether the publishing URL is in use
A publishing URL can be used by only one client at a time. A second client trying to publish using the URL will be rejected by Tencent Cloud. You can log in to the CSS console and check whether a stream is already being published in **[Stream Management](https://console.cloud.tencent.com/live/streammanage)** > **Live Streams**. You can also check whether a stream is disabled in **Disabled Streams**.

[](id:check6)
### 6. Why does a `-2` error occurs when I call `startPush` in `V2TXLivePusher` to publish streams?
A `-2` error may occur in the following cases:
- Using `V2TXLivePusher` to publish `trtc://` streams in LiteAVSDK_Smart. Only LiteAV_All and LiteAV_Enterprise support the TRTC protocol. LiteAVSDK_Smart does not.
- A required parameter is missing from the URL passed in to `startPush`. For how to splice publishing URLs, please see [Publishing/Playback URL](https://intl.cloud.tencent.com/document/product/1071/39359).
- The `V2TXLiveMode_RTC` mode is selected during initialization of the player, but an `rtmp://` URL is passed in.
