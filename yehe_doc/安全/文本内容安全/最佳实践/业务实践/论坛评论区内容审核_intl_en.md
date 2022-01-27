You can directly call the **TextModeration** API to recognize forum comments (such as shopping website reviews, community replies, and video comments).

>?
>- Before calling the API, make sure that the current account **has at least the access permission of TMS**. For more information on how to configure the permission, see [CAM Authorization Guide](https://intl.cloud.tencent.com/document/product/1121/43756).
>- If you cannot access the TMS service, you will need to activate the service/check the billing information (for root account) or request the corresponding permission from the admin or root account (for sub-account/collaborator).

## Step 1. Configure a task policy (optional)

We recommend you configure a task policy based on your business needs for a personalized user experience.

>?
>- You can skip this step if you use the preset default policy of Tencent Cloud TMS.
>- The default policy is developed by TenDI based on models for multiple industries. It is suitable for most content security requirements.

#### Prerequisites

- You already have a Tencent Cloud root account or sub-account.
- The logged-in account already has the read/write permissions of TMS.
- The logged-in account has activated TMS.

#### Directions

1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/image) and select **TMS** > **Policy Management** on the left sidebar.
2. On the **Policy Management** page, click **Create Policy** to enter the **Create Policy** page.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/bf768fcb23b0bb4cfb4ce42d4fbd5c7f.png)
3. On the **Policy Configuration** page, enter the relevant information of the policy and click **Next**.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/0d7dbf027682929c8d9b2bf3d8903461.png)

Parameter description:

| Parameter | Description |
| :----------- | :----------------------------------------------------------- |
| Policy Name     | Text description of the policy, which can contain up to 30 letters, digits, and underscores. |
| Biztype Name  | Specific policy number used for API calls, which can contain 3–32 letters, digits, and underscores and must be unique. |
| Industry Category     | Category of the industry scenario involved in the policy.                                       |
| Use Industry Template | It will be displayed only when **Industry Category** is set. You can select whether to use Tencent Cloud's preset industry templates for moderation. |

4. On the **Recognition Policy Configuration** page, select whether to moderate different types of content based on your business needs and click **Next**.

5. On the **Custom Library Configuration** page, select a custom dictionary for content moderation in the **Custom Dictionary** drop-down list. If there are no custom libraries, you can click **Next** or save the current policy and go to [Step 2. Configure a custom dictionary](https://intl.cloud.tencent.com/document/product/1121/43774#step2).
   ![img](https://qcloudimg.tencent-cloud.cn/raw/c4336b2548bf3ff13c8a336fadf5aee0.png)

6. On the **Creation Completion** page, you can view the policy configuration information. After confirming it, click **Complete**.

7. The policy just created will be displayed in the list on the right of the **Policy Management** page.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/a435f05c655bbc86953bb2b9127bdb1c.png)

## Step 2. Configure a custom dictionary (optional)

You can configure a custom dictionary to recognize whether images contain non-compliant text.

>? You can skip this step if you don't need to configure a custom dictionary.

#### Prerequisites

- You already have a Tencent Cloud root account or sub-account.
- The logged-in account already has the read/write permissions of TMS.
- The logged-in account has activated TMS.

#### Directions

1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/image) and select **TMS** > **Custom Library Management** > **Custom Dictionary** on the left sidebar.
2. On the **Custom Dictionary** page, click **Add Dictionary** to pop up the **Create Dictionary** window.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/455b516f6a3d18cc5214ae0dce0f8e61.png)
3. In the **Create Dictionary** pop-up window, configure a custom library based on your business needs.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/6e8ccc3a67bf82f29f9c1a525f673069.png)

Parameter description:

| **Parameter** | **Description**                                                     |
| :----------- | :----------------------------------------------------------- |
| Dictionary Name     | Text description of the dictionary, which can contain up to 32 letters, digits, and underscores. |
| Handling Suggestion     | You can select **Non-compliant** or **Suspected**.<li>Non-compliant: the information is identified as non-compliant information</li><li>Suspected: the information may be non-compliant and requires manual moderation</li> |
| Match Mode     | You can select **Exact match** or **Fuzzy match**.<li>Exact match: it exactly matches the entered text</li><li>Fuzzy match: it detects variants of the entered keyword to fuzzily match similar words such as split words, homographs, homophones, upper and lower cases, and numbers in words</li> |

4. Click **OK**.

5. The dictionary just created will be displayed in the list below the **Custom Dictionary** tab.

>? Different colors in a custom dictionary represent different blocking logics, where red represents "non-compliant", and orange represents "suspected".

![img](https://qcloudimg.tencent-cloud.cn/raw/0c5824665f35641a9d41ae01ec9fa005.png)

6. On the **Custom Dictionary** page, select the dictionary just created and click **Manage** in the **Operation** column to enter the dictionary management page.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/3e001665c7f532a2393636ba25cc0fda.png)
7. On the dictionary management page, click **Add Sample** to pop up the **Add Sample** window.
8. In the **Add Sample** pop-up window, select the handling suggestion, enter keywords, and click **OK**.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/bec6d9b5fe274edc95a622c0e5ededd4.png)

Parameter description:

| **Parameter** | **Description**                                                     |
| :----------- | :----------------------------------------------------------- |
| Handling Suggestion     | Violation type that corresponds to the recognition model.                                       |
| Keyword       | <li>Keywords are separated by line breaks, and each keyword can contain up to 20 letters.</li><li>You can add up to 500 keywords at a time.</li><li>You can add up to 2,000 keywords in total.</li> |

>? After configuring the custom dictionary, you can associate it with the policy created in [Step 1. Configure a task policy](https://intl.cloud.tencent.com/document/product/1121/43774#step1).

## Step 3. Create a task and get the recognition result

After completing the above steps, you can call the **TextModeration** API to create a comment moderation task as instructed below:

- Make sure that the text to be moderated meets the [file format requirements](https://cloud.tencent.com/document/product/1124/51860#1.-.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0) of the API.
- Enter the input parameters as instructed in the [API documentation](https://cloud.tencent.com/document/product/1124/51860#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0).
- If the task is created successfully, the API will return the detailed recognition result, and you can refer to [Text Content Recognition Sample](https://cloud.tencent.com/document/product/1124/51860#.E7.A4.BA.E4.BE.8B1-.E6.96.87.E6.9C.AC.E5.86.85.E5.AE.B9.E5.AE.89.E5.85.A8) for more information on sample response parameters. If task creation failed, the API will return an error code, and you can refer to [Business Error Codes](https://cloud.tencent.com/document/product/1124/51860#6.-.E9.94.99.E8.AF.AF.E7.A0.81) and [Common Error Codes](https://cloud.tencent.com/document/api/1124/51867#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81) for troubleshooting.

>? When connecting to the service, you can use API Explorer for online debugging.