## Message Push Tool
You can use this tool to query issues about the failure to receive offline messages.

1. Log in to [IM Console](https://console.cloud.tencent.com/im) and click the target app card.
2. In the left sidebar, choose **Development Tools** > **Message Push Tool**.
3. Select the offline certificate and enter the UserID.
4. Click **Start sending** to view the sending result.
  If the sending fails, you can check the cause of failure and view the corresponding solution.
  ![](https://main.qcloudimg.com/raw/8331b306bc248fcbedc27aa54d6c14c5.png)
	
## UserSig Tool
### Signature (UserSig) generation tool
The system automatically obtains the key of the current app. Therefore, you only need to enter the username (UserID) to use this tool to quickly generate a signature (UserSig) for local demos and feature testing and debugging. To use the UserSig in actual services, follow the method of [Generating a UserSig on the Server](https://cloud.tencent.com/document/product/269/32688#GeneratingdynamicUserSig).

1. Log in to [IM Console](https://console.cloud.tencent.com/im) and click the target app card.
2. In the left sidebar, choose **Development Tools** > **UserSig Tool**.
3. In the "UserSig Generation Tool" area, enter the username.
4. Click **Generate UserSig** to generate a signature, which expires after 180 days.
5. Click **Copy UserSig** to paste and save the signature.
 ![](https://main.qcloudimg.com/raw/83a24d72ec8914e8c1fa308457677e9f.png)

### UserSig verification tool
The system automatically obtains the key of the current app. Therefore, you only need to enter the UserID and UserSig to use the tool to quickly verify the UserSig.

1. Log in to [IM Console](https://console.cloud.tencent.com/im) and click the target app card.
2. In the left sidebar, choose **Development Tools** > **UserSig Tool**.
3. In the "UserSig Verification Tool" area, enter the UserID and UserSig.
   ![](https://main.qcloudimg.com/raw/6a304f8709fe4d91c2358daf667def24.png)
4. Click **Start verifying** to see the verification result.
 - If the verification succeeds, you can view the SDKAppID, UserID, creation time, valid period, and expiration time of the UserSig.
  ![](https://main.qcloudimg.com/raw/2882d65f9f28df99fe0c911db197fcce.png)
 - If the verification fails, you can check the cause of failure and view the corresponding solution.
  ![](https://main.qcloudimg.com/raw/f9cd08fb30d5ef24633e64bbb97e093d.png)
 
