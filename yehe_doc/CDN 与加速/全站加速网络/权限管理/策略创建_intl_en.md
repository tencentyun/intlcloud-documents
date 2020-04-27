To make it easier for you to configure domain name queries and manage permissions in a more refined manner, the ECDN permission policies have been completely upgraded, so that you can grant permissions at the domain name level through custom policy statements.
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/overview) and click **Policy** to enter the policy management page. Then, click **Create Custom Policy**:
![](https://main.qcloudimg.com/raw/52e43a672f41479128f48022ba8e1145.png)
2. Select **Create by Policy Builder**:
![](https://main.qcloudimg.com/raw/2dfc32b874cc02505d93eac1a279a1c9.png)
3. Select **ECDN** in the product drop-down list and select features to be authorized. If you want to grant full read/write permission, check **All** to select all services. For mappings between features and console elements, please see [Action Mapping Table](https://cloud.tencent.com/document/product/570/42271).
![](https://main.qcloudimg.com/raw/40734ee44969e096134202ad4dae02a8.png)
4. Enter the domain name to be authorized as the resource. You can use `*` to represent all domain names. After the configuration is completed, click **Add Statement** and **Next** to create a policy. Then, associate the created policy with existing users and user groups for further authorization:
![](https://main.qcloudimg.com/raw/fcc532a8f4d666316199153d0b509d6a.png)

