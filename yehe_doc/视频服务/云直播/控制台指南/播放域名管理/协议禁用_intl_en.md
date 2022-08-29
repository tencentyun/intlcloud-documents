You can block playback for a domain by blocking specific protocols. Playback requests that use the blocked protocols will be rejected.

## Prerequisites
- You have activated CSS and logged in to the [CSS console](https://console.cloud.tencent.com/live/livestat).
- You have added a [playback domain name](https://intl.cloud.tencent.com/document/product/267/35970).


## Blocking Protocols
1. Select [Domain Management](https://console.cloud.tencent.com/live/domainmanage) on the left sidebar. Click the name of the target playback domain or click **Manage** on the right to enter the domain management page.
2. Select the **Access Control** tab. In the **Block playback by protocol** area, you can block playback that uses the RTMP, FLV, HLS, or WebRTC protocol.
3. Click **Edit** and toggle on the protocols you want to block.
4. Click **Save**.

![](https://qcloudimg.tencent-cloud.cn/raw/362960a0beaf910fa931fc173b1e8abd.png)

>!
>- It takes a while for the blocking configuration to take effect. After configuring blocked protocols, please wait for the configuration to take effect before you block other protocols.
>- Except for HLS, protocol blocking only takes effect for new live streams. It does not affect ongoing streams.



## Unblocking Protocols
To unblock a blocked protocol, follow the steps below:
1. Select [Domain Management](https://console.cloud.tencent.com/live/domainmanage) on the left sidebar. Click the name of the target playback domain or click **Manage** on the right to enter the domain management page.
2. Select the **Access Control** tab. In the **Block playback by protocol** area, toggle off the protocol you want to unblock.
3. Click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/b3f339756306a55b39ed1acf1743c8c6.png)
