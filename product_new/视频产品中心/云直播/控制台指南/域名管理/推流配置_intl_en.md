## Scenario
The push configuration can be used to generate a push address under the corresponding push domain name. By pushing a live stream to the push address, the live stream can be transmitted (uploaded) to LVB.

## Prerequisites
 You have logged in to the [LVB Console](https://console.cloud.tencent.com/live).

## Steps
1. Select **Manage Domain** in the left sidebar, click the push domain name to be configured or click **Manage** in the operation column to enter the domain name management page.
 ![](https://main.qcloudimg.com/raw/88a070c73b1bcd6a04195da768ace0c7.png)
2. In the **Push Configuration** tab, you can find a push address generator. You only need to enter the StreamName (stream ID) and click **Generate a Push Address**, and the system will generate an RTMP push address containing the StreamName. The format of the address is `rtmp://domain/live/StreamName?txSecret=xxx&txTime=xxx` in which `domain` is the live push domain name, `AppName` is the application name (which is "live" by default; to customize it, submit a ticket), `StreamName` is the user-defined stream name used to label the live stream, `txSecret`is the authentication string generated after push authentication is enabled, and `txTime` is the timestamp set for the push address which represents the validity period of the address in the console. The generated push address can be tested, disabled, and deleted in [Stream Management](https://intl.cloud.tencent.com/document/product/267/31068).
 ![](https://main.qcloudimg.com/raw/29e4a0af31d1b37d91f6618453b6cc81.png)
We also provide sample PHP and Java codes for push address for your reference.
![](https://main.qcloudimg.com/raw/39c4e8aaa0975458dd153c29cd9148ce.png)

>The generated push address is valid before the set expiration time. You can generate a new address after the old one expires.
