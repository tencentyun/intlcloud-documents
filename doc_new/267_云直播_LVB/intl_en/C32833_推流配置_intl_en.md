## Scenario
The push configuration can be used to generate a push address under the corresponding push domain name. By pushing a live stream to the push address, the live stream can be transmitted (i.e., uploaded) to LVB.

## Prerequisites
 You have logged in to the [LVB Console](https://console.cloud.tencent.com/live).

## Directions
1. Select **Domain Name Management** in the left sidebar and click **Manage** or the push domain name to be configured to enter the domain name management page.
 ![](https://main.qcloudimg.com/raw/88a070c73b1bcd6a04195da768ace0c7.png)
2. In the **Push Configuration** tab, a push address generator is provided. You only need to enter the StreamName (stream ID) and click **Generate a Push Address**, and the system will generate an RTMP push address containing the StreamName in the format of `rtmp://domain/live/StreamName?txSecret=xxx&txTime=xxx`, where `domain` is the live streaming push domain name, `AppName` is the application name (which is "live" by default; to customize it, submit a ticket), `StreamName` is the user-defined stream name used to identify the live stream, `txSecret`is the authentication string generated after push authentication is enabled, and `txTime` is the timestamp set for the push address which represents the validity period of the address in the console. The generated push address can be tested, disabled, and deleted in [Stream Management](https://intl.cloud.tencent.com/document/product/267/31068).
 ![](https://main.qcloudimg.com/raw/29e4a0af31d1b37d91f6618453b6cc81.png)
PHP and Java sample code for push address generating is provided for your reference.
![](https://main.qcloudimg.com/raw/39c4e8aaa0975458dd153c29cd9148ce.png)

>The generated push address can be used before the set expiration time. After it expires, a new push address can be regenerated.
