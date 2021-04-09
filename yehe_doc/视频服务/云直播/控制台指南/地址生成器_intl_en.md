
## Operation Scenarios
With the address generator, you can select an added push/playback domain name to quickly generate the corresponding push/playback address.

## Prerequisites
There should be at least one available domain name in [Domain Management](https://intl.cloud.tencent.com/document/product/267/31056) in the [CSS console](https://console.cloud.tencent.com/live).

## Directions
1. Log in to the CSS console, select **Auxiliary Tools** > **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)** to open the Address Generator.
3. Configure as follows on the Address Generator page:
	1. Select the type, such as **push domain** or **playback domain**.
	2. Select a domain name you have already added on the Domain Management page.
	3. `AppName` is the address path used to differentiate multiple applications under the same domain name, which is `live` by default.
>`AppName` can be customized and can contain only letters, digits, and symbols.
	4. Enter a custom `StreamName`, such as `liveteststream`.
	5. Select the expiration time of the address, such as `2019-11-30 23:59:59`.
3. Click **Generate Address** to generate the corresponding domain name address.
![](https://main.qcloudimg.com/raw/1d9741fe544d1c850ab89b22134f6dc8.png)

>
>- The generated push/playback address consists of the following four parts:
![](https://main.qcloudimg.com/raw/9094e537a4ae7cecc7feb9c88fb83a55.png)
>- The generated playback address supports RTMP, FLV, and HLS protocols. You can click the QR code after the address and scan it with the Lite Demo to view the address:
![](https://main.qcloudimg.com/raw/d91fe5d373cfc03df2c87562f3984858.png)
