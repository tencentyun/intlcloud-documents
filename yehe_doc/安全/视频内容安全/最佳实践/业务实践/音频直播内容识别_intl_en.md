After activating [AMS](https://console.cloud.tencent.com/cms/audio/package), you can directly call **AMS** APIs to recognize audio stream content (such as game live streaming, radio, and voice chat).
>?
>- Before calling the API, make sure that the current account **has at least the access permission of AMS**. For more information on how to configure the permission, see [CAM Authorization Guide](https://intl.cloud.tencent.com/document/product/1140/44981).
>- If you cannot access the service, you will need to activate the service/check the billing information (for root account) or request the corresponding permission from the admin or root account (for sub-account/collaborator).

## Step 1. Configure a global task template (optional)
Task templates are used to manage how files are processed for recognition tasks. You can skip this step if the default template is used.
>?Currently, only the default template can be edited for template configuration.

1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/audio/srvconfig) and select **AMS** > **Service Management** on the left sidebar to enter the **Service Management** page.
2. On the service management page, click **View Details**, and the details of the default template will be displayed on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/a9522962d24822a73745c684fce971bf.png)
3. On the specific information page, click **Edit** in the top-right corner to enter the template editing page.
![](https://qcloudimg.tencent-cloud.cn/raw/3f02606eadd9d27b941899c3bca03c47.png)
4. On the template editing page, set the configuration information, including template name, audio stream or large file segment duration (15s, 30s, or 60s), optional callback address (to which risky content can be returned), and full callback for live streaming switch (on/off). You can customize the template configuration based on your business and storage needs.
![](https://qcloudimg.tencent-cloud.cn/raw/efa2956eff8dd0b39d44966dbdd6923c.png)
5. Click **Save** to save the current template, **which will take effect immediately for all AMS services under the account**.

## Step 2. Configure a custom library (optional)
The custom library is used to configure the personalized recognition content. You can skip this step if you don't need to configure a custom library.
1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/audio/lib) and select **AMS** > **Custom Library Management** > **Custom Dictionary** on the left sidebar to enter the **Custom Dictionary** page.
2. On the **Custom Dictionary** page, click **Add Dictionary** to pop up the **Create Dictionary** window.
![](https://qcloudimg.tencent-cloud.cn/raw/dc9857444a5805e9aadfcee2cf018396.png)
3. In the **Create Dictionary** pop-up window, configure a custom library based on your business needs.
![](https://qcloudimg.tencent-cloud.cn/raw/a7714daf0a1f515c0ed8647c0169cb80.png)
4. Click **OK**.
5. On the **Custom Dictionary** page, select the target dictionary and click **Manage** in the **Operation** column to enter the dictionary content management page.
![](https://qcloudimg.tencent-cloud.cn/raw/74829f9fcd5190d69671293cc3e726f3.png)
6. On the dictionary content management page, click **Add Sample** in the top-left corner to pop up the **Add Sample** window.
7. In the **Add Sample** pop-up window, select the recognition details, enter keywords, and click **OK**.
>?
>- Recognition Details: violation type that corresponds to the recognition model.
>- Keywords: each keyword can contain up to 20 characters, and a maximum of 500 keywords separated by line breaks can be batch submitted at a time.

![](https://qcloudimg.tencent-cloud.cn/raw/83f19abaf6ecb7549f3cd4fdefd3faa0.png)
8. On the **Custom Dictionary** page, select the target dictionary and click ![](https://main.qcloudimg.com/raw/541944ccb7722e47db44524e6174a176.png) in the **Operation** column to enable or disable it.
>?
>- After the custom dictionary is enabled, custom violation results will be returned in preference to the default dictionary.
>- After the dictionary is disabled, samples in it will not be used to match and recognize image content.

9. After configuring the custom dictionary, you can associate it with the policy created in [Configure a task policy](#PZCL).


## Step 3. Configure a task policy (optional)[](id:PZCL)
You can skip this step if you use the preset default policy. The default policy is developed by TenDI based on models for multiple industries. It is suitable for most content security requirements.
1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/audio/strategy) and select **AMS** > **Policy Management** on the left sidebar to enter the **Policy Management** page.
2. On the **Policy Management** page, click **Create Policy** in the top-left corner to enter the **Create Policy** page.
![](https://qcloudimg.tencent-cloud.cn/raw/170ecda3857b431040ea5442702f09dc.png)
3. On the **Create Policy** page, set the relevant policy information, including the policy name, Biztype name, associated service template (not required currently), and industry category (select whether to use TenDI's preset industry templates for recognition), and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/472e060a38aec28aa068b09f68893e25.png)
4. Configure the recognition policy, select whether to recognize different types of risky content based on your business needs, and click **Next**.
5. Configure the custom library and select whether to configure the custom dictionary you set. If there is no custom library, you can click **Next** to save the current policy and go to the **Configure a custom dictionary** step.
6. After the creation is completed, you can view the policy configuration information on this page. After confirming it, click **Complete**, and then the policy can be used in API calls.

## Step 4. Create an AMS task 
After completing the above steps, you can call the **CreateAudioModerationTask** API to create an audio stream recognition task as instructed below:
- Make sure that the audio meets the [file format requirements](https://intl.cloud.tencent.com/document/product/1139/46101#1.-.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0) of the API.
- Enter the input parameters as instructed in the [API documentation](https://intl.cloud.tencent.com/document/product/1139/46101#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0).
- If the task is created successfully, you can use the task query API to query task details, and you can refer to the [example of creating audio recognition task](https://intl.cloud.tencent.com/document/product/1139/46101#.E7.A4.BA.E4.BE.8B1-.E5.88.9B.E5.BB.BA.E9.9F.B3.E9.A2.91.E5.AE.A1.E6.A0.B8.E4.BB.BB.E5.8A.A1) for more information on sample response parameters. If task creation fails, the API will return an error code, and you can refer to [Business Error Codes](https://intl.cloud.tencent.com/document/product/1139/46101#6.-.E9.94.99.E8.AF.AF.E7.A0.81) and [Common Error Codes](https://intl.cloud.tencent.com/document/product/1139/46099#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81) for troubleshooting.

>? When connecting to the service, you can use API Explorer for online debugging.

## Step 5. Get the AMS task result
After creating the audio recognition task, you can call the **DescribeTaskDetail** API to query the details of the task as instructed below:
- Enter the input parameters as instructed in the [API documentation](https://intl.cloud.tencent.com/document/product/1139/46100).
- If the API call is successful, you will receive the response output from the API, including the task details. You can refer to the [example of viewing task details](https://intl.cloud.tencent.com/document/product/1139/46100#4.-.E7.A4.BA.E4.BE.8B) for more information on sample response parameters.
