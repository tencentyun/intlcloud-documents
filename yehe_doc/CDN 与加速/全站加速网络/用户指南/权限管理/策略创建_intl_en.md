To make it easier for you to configure domain name queries and manage permissions in a more refined manner, the ECDN permission policies have been completely upgraded, so that you can grant permissions at the domain name level through custom policy statements.
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/overview) and click **Policy** to enter the policy management page. Then, click **Create Custom Policy**:
![](https://main.qcloudimg.com/raw/cd17fa629afe272d53b84c1a17d044e8.png)
2. Select **Create by Policy Builder**:
![](https://main.qcloudimg.com/raw/6c6fdbed40dfcc561680299678feee43.png)
3. Select **ECDN** in the product drop-down list and select features to be authorized. If you want to grant full read/write permission, check **All** to select all services. For mappings between features and console elements, please see [Action Mapping Table](https://intl.cloud.tencent.com/document/product/570/35819).
![](https://main.qcloudimg.com/raw/19ca1a9ed6d5f89d49562e026c29a1b4.png)
4. Enter the domain name that needs to be authorized as the "resource" in the format of `qcs::ecdn::uin/xxxxxxxxxx:domain/xxx.com`, where `xxxxxxxxxx` after `uin/` needs to be replaced with your account ID, and `xxx.com` needs to be replaced with the specific domain name to be authorized. You can directly enter `*` to represent all domain names. After the configuration is completed, click **Add Statement** and **Next** to create a policy. Then, associate the created policy with existing users and user groups for further authorization:
![](https://main.qcloudimg.com/raw/243ebba2827f93c1aed48fc6a8a33ab6.png)

