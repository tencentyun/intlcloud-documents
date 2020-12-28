## Offline Push Self-Service Check

This tool allows you to query issues about the failure in receiving offline messages.

1. Log in to the [Instant Messaging Console](https://console.cloud.tencent.com/im), and then click the target Instant Messaging (IM) app card.
2. In the left sidebar, choose **Auxiliary Tools** > **Offline Push Self-Service Check**.
3. Enter the UserID.
4. Click **Get device information** to view the uploaded information of the UserID, such as the certificate ID and device token.
 >?If none of the information such as the certificate ID and device token of the UserID has been uploaded, the self-service query ends.
 >
5. Select any certificate ID of the UserID, and then click **Start testing**. You can view the sending result of the test offline message in the **Test results** field.
 If the offline message failed to be sent, you can view the specific failure cause and solution in the **Test results** field.
 
 ![](https://main.qcloudimg.com/raw/76b40ef61f2034718dc489519d4f7c4d.png)
[](id:status)
## UserSig Tools
### UserSig generator
The system automatically obtains the key of the current app. After entering the UserID, you can use this tool to quickly generate a signature (UserSig) to run through demos and debug features locally. If you need to generate a UserSig for online services, see [Generating a UserSig on the Server](https://intl.cloud.tencent.com/document/product/1047/34385).

1. Log in to the [Instant Messaging Console](https://console.cloud.tencent.com/im), and then click the target IM app card.

2. In the left sidebar, choose **Auxiliary Tools** -> **UserSig Tools**.

3. In the UserSig Generator area, enter the UserID.

4. Click **Generate UserSig** to generate a UserSig, which expires after 180 days.

5. Click **Copy UserSig** to copy the signature and then paste and save the signature.

   ![](https://main.qcloudimg.com/raw/858a4c73c2dd149933fb6133359ece4c.png)

### UserSig verification tool
The system automatically obtains the key of the current app. After entering the UserID and UserSig, you can use the tool to quickly check the validity of the UserSig.

1. Log in to the [Instant Messaging Console](https://console.cloud.tencent.com/im), and then click the target IM app card.
2. In the left sidebar, choose **Auxiliary Tools** -> **UserSig Tools**.
3. In the UserSig Verification Tool area, enter the UserID and UserSig.
4. Click **Verify** to see the verification results.
 - If the verification succeeds, you can view the SDKAppID, UserID, generation time, service time, and expiration time of the UserSig in the verification results.
 - If the verification fails, you can view the failure cause and solution in the verification results.
   

