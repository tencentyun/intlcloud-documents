## Offline Push Check
### Offline push issue locator
This tool allows you to query issues related to the failure to receive offline messages.

1. Log in to the [Chat console](https://console.cloud.tencent.com/im) and click the target Chat app section.
2. In the left sidebar, choose **Auxiliary Tools** > **Offline Push Self-Service Check**.
3. In the **Offline Push Issue Locator** area, enter the UserID.
4. Click **Obtain Device Status** to view the uploaded information for the UserID, such as the certificate ID and device token.
>? If no UserID information, such as the certificate ID and device token, has been uploaded, the query ends.
>
5. Select any certificate ID of the UserID, click **Start Checking**, and then view the sending result.
 - If a success prompt is displayed, the certificate information you entered in the console is correct and the token was uploaded by calling the SDK API. You can use the [user client status checking tool](#status) for further troubleshooting. 
 - If a failure prompt is displayed, you can view the cause of the failure and the solution.

![](https://main.qcloudimg.com/raw/5c1930b3079c03fa730aacd6950cea1e.png)

[](id:status)
### User status checker
This tool automatically obtains the user’s client status and checks whether the user is ready to receive offline push messages.

1. Log in to the [Chat console](https://console.cloud.tencent.com/im) and click the target Chat app section.
2. In the left sidebar, choose **Auxiliary Tools** > **Offline Push Self-Service Check**.
3. In the **User Status Checker** area, enter the UserID.
4. Click **Get Status** to view information such as the current status and client type of the UserID.
 If you are prompted that the UserID is ready to receive offline push messages, you can log in with a different UserID on another device to send one-to-one text messages to the current UserID to check whether it can receive the messages.

![](https://main.qcloudimg.com/raw/5674cd90ac892e48882cfc0f3130eeab.png)

## UserSig Generation and Verification
### UserSig generator
The system automatically obtains the key of the current app. After entering the UserID, you can use this tool to quickly generate a signature (UserSig) to run through demos and debug features locally. If you need to generate a UserSig for online services, see [Generating a UserSig on the Server](https://intl.cloud.tencent.com/document/product/1047/34385).

1. Log in to the [Chat console](https://console.cloud.tencent.com/im) and click the target Chat app section.
2. In the left sidebar, choose **Auxiliary Tools** > **UserSig Tools**.
3. In the UserSig Generator area, enter the UserID.
4. Click **Generate UserSig** to generate a UserSig, which expires after 180 days.
5. Click **Copy UserSig** to copy the signature and then paste and save the signature.
 ![](https://main.qcloudimg.com/raw/edc9bb594760b1edcf0366d92ce69d07.png)

### UserSig verification tool
The system automatically obtains the key of the current app. After entering the UserID and UserSig, you can use the tool to quickly check the validity of the UserSig.

1. Log in to the [Chat console](https://console.cloud.tencent.com/im) and click the target Chat app section.
2. In the left sidebar, choose **Auxiliary Tools** > **UserSig Tools**.
3. In the UserSig Verification Tool area, enter the UserID and UserSig.
   ![](https://main.qcloudimg.com/raw/5fcd54faa763ff3bb46b074945bd02ed.png)
4. Click **Verify** to see the verification result.
 - If verification succeeds, you can view the SDKAppID, UserID, generation time, service time, and expiration time of the UserSig in the verification results.
    ![](https://main.qcloudimg.com/raw/383c2f0761eec12124c442683f09de07.png)
 - If verification fails, you can view the cause of failure and solution in the verification results.
    ![](https://main.qcloudimg.com/raw/b320ffc210f5b93ce261d9a3d697aa07.png)

 

 
