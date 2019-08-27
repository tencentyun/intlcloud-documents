
## Scenario
With the address generator, you can select an added push/playback domain name to quickly generate the corresponding push/playback address.

## Prerequisites
There should be at least one available domain name in [Manage Domain](https://cloud.tencent.com/document/product/267/20381) in the [LVB Console](https://console.cloud.tencent.com/live).

## Steps
1. Select **Auxiliary Tools** > **Address Generator** in the left sidebar to enter the address generator page.
![](https://main.qcloudimg.com/raw/404f832e1bac2d605016f862686be1d1.png)
2. Select a push/playback domain name and select the corresponding domain name that has been added to domain name management. AppName, which is "live" by default, is the address path used to differentiate multiple applications under the same domain name.
>! AppName can be customized but can only contain letters, numbers, and symbols. To customize it, you need to [submit a ticket](https://console.cloud.tencent.com/workorder/category) to enable configuration.
3. Enter the StreamName and select the expiration time to generate the address.
![](https://main.qcloudimg.com/raw/7aad3d258644a4b59872360805bac3eb.png)
>?
>- The generated push address consists of the following four parts:
![](https://main.qcloudimg.com/raw/7a276cbf9250e3c7f7d94a620172e795.png)
>- The generated playback address supports RTMP, FLV, and HLS protocols. 
