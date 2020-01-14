
You can efficiently and comprehensively protect against layer 4 CC attacks such as masquerading and replay attacks by accessing watermark protection. By sharing the watermark algorithm and key between the business side and the Aegis protection system, watermark protection embeds a watermark in every message sent by the client. As the attack messages have no watermark, the protection system can easily identify and discard them. For more information on the configuration, see [Custom Advanced Security Policy](https://intl.cloud.tencent.com/document/product/685/18800#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AE.89.E5.85.A8.E7.AD.96.E7.95.A5).
## Flowchart
![](https://main.qcloudimg.com/raw/8b83ba4ab8b1bdee1d0e1da446d53e3e.png)

## How to Enable
1. **Enable watermarking in the "Business Domain Name List"**
Go to the [Aegis Anti-DDoS Console](https://console.cloud.tencent.com/gamesec), click **Business Domain Name List* in the left pane, and click **Enable watermark**.
![1](https://main.qcloudimg.com/raw/6c53776a2a1f72da1aab2e4cbeb7b67e.png)
2. **Copy the key**
a. After watermarking is successfully enabled, select "Copy the key" in the "Enabled successfully" pop-up and click **Add Protection Policy**.
![2](https://main.qcloudimg.com/raw/42134fa35b315e4c57981963f73e40e0.png)
b. Go to the "Add Protection Policy" page and select "Protected IP".
![3](https://main.qcloudimg.com/raw/c15bc6e8aefa1b7a711bb4b187a9f2cf.png)
c. Add the TCP protection port, UDP protection port and whitelist and then click **Confirm to add**.
![4](https://main.qcloudimg.com/raw/bb5b8a2c9394a19720ba92aa5c2b5682.png)
3. **Offline configuration**
In the "Enabled successfully" pop-up, click **Client connection file** to download the file for connecting the client and the server.
4. **Enable the policy**
a. After the policy is created successfully, under **Watermark Protection**, click **Add Policy** to modify it and then click **Enable policy**.
![](https://main.qcloudimg.com/raw/8fe6f6bd3b004821f8e2c4e06515bebd.png)
b. Wait a few seconds before the protection status is changed to "protection active", and watermarking is successfully enabled.
![](https://main.qcloudimg.com/raw/5156b27493055304f1a940b4d9acebe3.png)
