
If you follow the steps in [Best Practice > CSS Push](https://intl.cloud.tencent.com/document/product/267/31558) but fail to publish streams, check the common reasons for publishing failure listed in this document to troubleshoot the issue.

[](id:check1)
### 1. Check whether you have configured for your domain name a CNAME record that points to a Tencent Cloud address
Publishing can succeed only if your domain name has a CNAME record that points to a Tencent Cloud address. You can check whether a publishing domain name created has a CNAME record in the “CNAME” column in **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**. The domain names in the figure below have CNAME records.

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
To ensure security, Tencent Cloud requires hotlink protection for all publishing URLs and **rejects** expired URLs and those with miscalculated hotlink protection keys. If publishing is rejected, the MLVB SDK throws the **PUSH_WARNING_SERVER_DISCONNECT** event, and you will see the log below in the [demo](https://intl.cloud.tencent.com/document/product/1071/38147).

See [Best Practice > CSS Push](https://intl.cloud.tencent.com/document/product/267/31558) for how to get reliable publishing URLs.

[](id:check5)
### 5. Check whether the publishing URL is in use
A publishing URL can be used by only one client at a time. A second client trying to publish using the URL will be rejected by Tencent Cloud. You can log in to the CSS console and check whether a stream is already being published in **[Stream Management](https://console.cloud.tencent.com/live/streammanage)** > **Live Streams**. You can also check whether a stream is disabled in **Disabled Streams**.

 

