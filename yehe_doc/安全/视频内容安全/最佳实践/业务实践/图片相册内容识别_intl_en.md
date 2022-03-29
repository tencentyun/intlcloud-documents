For image content, after [activating IMS](https://console.cloud.tencent.com/cms/image/package), you can directly call the **ImageModeration** API to batch recognize images in albums (such as Qzone album).
>?
>- Before calling the API, make sure that the current account **has at least the access permission of IMS**. For more information on how to configure the permission, see [CAM Authorization Guide](https://intl.cloud.tencent.com/document/product/1140/44981).
>- If you cannot access the service, you will need to activate the service/check the billing information (for root account) or request the corresponding permission from the admin or root account (for sub-account/collaborator).

## Step 1. Configure a custom dictionary (optional)  
The custom dictionary is used to configure the personalized recognition content. You can skip this step if you don't need to configure a custom library.
1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/image/lib) and select **IMS** > **Custom Library Management** > **Custom Dictionary** on the left sidebar to enter the **Custom Dictionary** page.
2. On the **Custom Dictionary** page, click **Add Dictionary** in the top-left corner to pop up the **Create Dictionary** window.
![](https://qcloudimg.tencent-cloud.cn/raw/455b516f6a3d18cc5214ae0dce0f8e61.png)
3. In the **Create Dictionary** pop-up window, configure a custom library based on your business needs.
![](https://qcloudimg.tencent-cloud.cn/raw/6e8ccc3a67bf82f29f9c1a525f673069.png)
4. Click **OK**.
5. On the **Custom Dictionary** page, select the target dictionary and click **Manage** in the **Operation** column to enter the dictionary content management page.
![](https://qcloudimg.tencent-cloud.cn/raw/3e001665c7f532a2393636ba25cc0fda.png)
6. On the dictionary content management page, click **Add Sample** in the top-left corner to pop up the **Add Sample** window.
7. In the **Add Sample** pop-up window, select the recognition details, enter keywords, and click **OK**.
>?
>- Recognition Details: violation type that corresponds to the recognition model.
>- Keywords: each keyword can contain **up to 20 characters**, and **a maximum of 500 keywords separated by line breaks can be batch submitted** at a time.

![](https://qcloudimg.tencent-cloud.cn/raw/bec6d9b5fe274edc95a622c0e5ededd4.png)
8. On the **Custom Dictionary** page, select the target dictionary and click ![](https://main.qcloudimg.com/raw/541944ccb7722e47db44524e6174a176.png) in the **Operation** column to enable or disable it.
>? After the dictionary is disabled, samples in it will not be used to match and recognize image content.
9. After configuring the custom dictionary, you can associate it with the policy created in [Configure a task policy](#PZCL).


## Step 2. Configure a task policy (optional)[](id:PZCL)
You can skip this step if you use the preset default policy. The default policy is developed by TenDI based on models for multiple industries. It is suitable for most content security requirements.
1. Log in to the [IMS console](https://console.cloud.tencent.com/cms/image/strategy) and select **IMS** > **Policy Management** on the left sidebar to enter the **Policy Management** page.
2. On the **Policy Management** page, click **Create Policy** in the top-left corner to enter the **Create Policy** page.
![](https://qcloudimg.tencent-cloud.cn/raw/1c4ada21db2a93461900539c8d578ea7.png)
3. On the **Create Policy** page, set the relevant policy information, including the policy name, Biztype name, associated service template (**not required currently**), and industry category (select whether to use TenDI's preset industry templates for recognition), and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/0d7dbf027682929c8d9b2bf3d8903461.png)
4. Configure the recognition policy, select whether to recognize different types of risky content based on your business needs, and click **Next**.
5. Configure the custom library, select whether to configure the custom dictionary, and click **Next**.
6. After the creation is completed, you can view the policy configuration information on this page. After confirming it, click **Complete**.

## Step 3. Create a task and get the recognition result
After completing the above steps, you can call the **ImageModeration** API to create an album recognition task as instructed below: <br>
- Make sure that the images meet the [file format requirements](https://intl.cloud.tencent.com/document/product/1122/46084#1.-.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0) of the API.
- Enter the input parameters as instructed in the [API documentation](https://intl.cloud.tencent.com/document/product/1122/46084#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0).
- If the task is created successfully, the API will return the detailed recognition result, and you can refer to [Image Content Recognition Sample](https://intl.cloud.tencent.com/document/product/1122/46084#.E7.A4.BA.E4.BE.8B1-.E5.9B.BE.E7.89.87.E5.86.85.E5.AE.B9.E8.AF.86.E5.88.AB) for more information on sample response parameters. If task creation failed, the API will return an error code, and you can refer to [Business Error Codes](https://intl.cloud.tencent.com/document/product/1122/46084#6.-.E9.94.99.E8.AF.AF.E7.A0.81) and [Common Error Codes](https://intl.cloud.tencent.com/document/product/1122/46081#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81) for troubleshooting.

>? When connecting to the service, you can use API Explorer for online debugging.
