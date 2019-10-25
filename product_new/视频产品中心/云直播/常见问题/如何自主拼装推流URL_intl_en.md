
### Push URL 
You can use the [URL Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator) in the LVB Console to generate push and playback addresses. If there are many live rooms, you can splice such addresses on the server. Any URL that meets Tencent Cloud standards can be used for push. A standard push URL consists of four parts as shown below:
![](https://main.qcloudimg.com/raw/0d66d6410c84794f1795da847b8f7ec2.png)
- **Domain**
Push domain name, which can be the default push domain name provided by Tencent Cloud LVB or your own push domain name.
- **AppName**
Application name, which is "live" by default. If you want to customize it, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for configuration.
- **StreamName (stream ID)**
Custom stream name, which is used to identify a live stream. You are recommended to use an authentication key containing random digits or a combination of digits and letters. It has two parts: txSecret and txTime. If push authentication is enabled, the URL used for push should contain the authentication key; otherwise, it does not need to contain the "?" and the content behind.
- **txTime (address validity period)** 
The time when the URL expires, which is expressed as a hexadecimal UNIX timestamp; for example, 5867D600 indicates that the URL will expire at 00:00:00 AM on January 1, 2017. Generally, txTime is set to a time 24 hours after the current time. The expiration time should be neither too short nor too long. If it is too short, when the host encounters network jitters during a live broadcast, the push cannot be resumed because the push URL expires.
- **txSecret (hotlink protection signature)**
This is used to prevent attackers from forging your backend for push URL generation. For more information on the calculation method, see [Best Practices - Hotlink Protection URL Calculation](https://intl.cloud.tencent.com/document/product/267/31560).
- **Sample code**
Go to the [**LVB Console**](https://console.cloud.tencent.com/) > **Domain Management**, select a pre-configured push domain name, and click **Manage** > **Push Configuration** to display the **Sample Code** (for PHP and Java) that demonstrates how to generate a hotlink protection address.


