For resellers, their root account admins need to go to the **Cloud Access Management (CAM)** console to manage sub-users.

## Directions
1. Go to the [Tencent Cloud website](https://www.tencentcloud.com/account/login).
2. Click **Log In** at the top-right corner to enter the login page.
![](https://qcloudimg.tencent-cloud.cn/raw/10c090874aecd9a31b99cb07637d2356.png)
3. Enter the root account login information and click **Log In**.
4. Click the profile photo at the top-right corner and click **Access Management**.
![](https://qcloudimg.tencent-cloud.cn/raw/74b4a3f495300e35d3591f48262695a4.png)
5. Set sub-user permissions in the CAM console.
(1) Create a sub-user.
![](https://qcloudimg.tencent-cloud.cn/raw/23f427991f34da7bcf066c54a9affcd2.jpg)
(2) Grant default full read-write access and full read-only access permissions to the sub-user.
![](https://qcloudimg.tencent-cloud.cn/raw/367e211a9cf6456560e3623fc7a2383c.jpg)
![](https://qcloudimg.tencent-cloud.cn/raw/e5c05ba9e6c1be3798ebd339ceb6d0c3.png)
6. (Optional) If you require more refined permission management, you can create a custom policy in the CAM console.
(1) Create a custom permissions policy.
![](https://qcloudimg.tencent-cloud.cn/raw/151f291a13868ae4a869ab0db75b436f.png)
(2) Click **Create by Policy Generator**.
![](https://qcloudimg.tencent-cloud.cn/raw/c4ec1fce786259b96813e7db4c0a27e5.png)
(3) On the policy creation page, select **International Partners Management (intlpartnersmgt)** for the **Service** field and select the API actions you want to configure for the policy, click **Next** and complete the following policy creation process.
![](https://qcloudimg.tencent-cloud.cn/raw/5badb5b441f47560d32b2bbd496f6675.png)
7. Provide the sub-user login URL, account ID, and initial password for the sub-user for login.
![](https://qcloudimg.tencent-cloud.cn/raw/bf019b1331f7612d176670c0ff35fcaa.png)

>？
>- For more CAM capabilities, see [CAM Documentation](https://www.tencentcloud.com/document/product/598).
>- If you have any questions, [submit a ticket](https://console.cloud.tencent.com/workorder/category).

