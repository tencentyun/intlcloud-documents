For image content, after [activating IMS](https://console.cloud.tencent.com/cms/image/package), you can directly call the **image moderation** API to batch recognize images in albums (such as Qzone album).

>?
>- Before calling the API, make sure that the current account **has at least the access permission of IMS**. For more information on how to configure the permission, see [CAM Authorization Guide](https://intl.cloud.tencent.com/document/product/1122/43814).
>- If you cannot access the service, you will need to activate the service/check the billing information (for root account) or request the corresponding permission from the admin or root account (for sub-account/collaborator).

## Step 1. Configure a task policy

We recommend you configure a task policy based on your business needs for a personalized user experience.

>?
>- You can skip this step if you use the preset default policy of Tencent Cloud IMS.
>- The default policy is developed by TenDI based on models for multiple industries. It is suitable for most content security requirements.

#### Prerequisites

- You already have a Tencent Cloud root account or sub-account.
- The logged-in account already has the read/write permissions of IMS.
- The logged-in account has activated IMS.

#### Directions

1. Log in to the [IMS console](https://console.cloud.tencent.com/cms/image) and select **IMS** > **Policy Management** on the left sidebar.
2. On the **Policy Management** page, click **Create Policy** to enter the **Create Policy** page.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/7d59494faf27e636bbbda52016cf1e75.png)
3. On the **Policy Configuration** page, enter the relevant information of the policy and click **Next**.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/0018465769af15f4e43fb4fe9666930e.png)

Parameter description:

| Parameter | Description |
| :----------- | :----------------------------------------------------------- |
| Policy Name     | Text description of the policy, which can contain up to 30 letters, digits, and underscores. |
| Biztype Name  | Specific policy number used for API calls, which can contain 3–32 letters, digits, and underscores and must be unique. |
| Associated Service Template | Not required currently.                                               |
| Industry Category     | Category of the industry scenario involved in the policy.                                       |
| Use Industry Template | It will be displayed only when **Industry Category** is set. You can select whether to use Tencent Cloud's preset industry templates for moderation. |

4. On the **Recognition Policy Configuration** page, select whether to moderate different types of content based on your business needs and click **Next**.

5. On the **Custom Library Configuration** page, select a custom dictionary for content moderation in the **Custom Dictionary** drop-down list. If there are no custom libraries, you can click **Next** or save the current policy and go to [Step 2. Configure a custom dictionary](https://intl.cloud.tencent.com/document/product/1122/43831#step2).
   ![img](https://qcloudimg.tencent-cloud.cn/raw/442200e56e4b524618efe12de319a611.png)

6. On the **Creation Completion** page, you can view the policy configuration information. After confirming it, click **Complete**.

7. The policy just created will be displayed in the list on the right of the **Policy Management** page.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/c0206a3d2b24e3831527a11cf3c5fb4b.png)

## Step 2. Configure a custom dictionary

You can configure a custom dictionary to recognize whether images contain non-compliant text.

>! You can skip this step if you don't need to configure a custom dictionary.

#### Prerequisites

- You already have a Tencent Cloud root account or sub-account.
- The logged-in account already has the read/write permissions of IMS.
- The logged-in account has activated IMS.

#### Directions

1. Log in to the [IMS console](https://console.cloud.tencent.com/cms/image) and select **IMS** > **Custom Library Management** > **Custom Dictionary** on the left sidebar.
2. On the **Custom Dictionary** page, click **Add Dictionary** to pop up the **Create Dictionary** window.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/400ea8260bf6f39871da1ec52d81a9a4.png)
3. In the **Create Dictionary** pop-up window, configure a custom library based on your business needs.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/ce393be799fbf17974daff8dafa0d938.png)

Parameter description:

| **Parameter** | **Description**                                                     |
| :----------- | :----------------------------------------------------------- |
| Dictionary Name     | Text description of the dictionary, which can contain up to 32 letters, digits, and underscores. |
| Handling Suggestion     | You can select **Non-compliant** or **Suspected**.<li>Non-compliant: the information is identified as non-compliant information</li><li>Suspected: the information may be non-compliant and requires manual moderation</li> |
| Match Mode     | You can select **Exact match** or **Fuzzy match**.<li>Exact match: it exactly matches the entered text</li><li>Fuzzy match: it detects variants of the entered keyword to fuzzily match similar words such as split words, homographs, homophones, upper and lower cases, and numbers in words</li> |

4. Click **OK**.

5. The dictionary just created will be displayed in the list below the **Custom Dictionary** tab.

>? Different colors in a custom dictionary represent different blocking logics, where red represents "non-compliant", and orange represents "suspected".

![img](https://qcloudimg.tencent-cloud.cn/raw/a4ac07df7985f54f92eb4b44e506f374.png)

6. On the **Custom Dictionary** page, select the dictionary just created and click **Manage** in the **Operation** column to enter the dictionary management page.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/66c45de0cd6949276e0f8f7f2ad155ef.png)

7. On the dictionary management page, click **Add Sample**, select the handling suggestion, enter keywords, and click **OK**.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/3f912867a346429889a9839d6fff6e89.png)

Parameter description:

| **Parameter** | **Description**                                                     |
| :----------- | :----------------------------------------------------------- |
| Handling Suggestion     | Violation type that corresponds to the recognition model.                                       |
| Keyword       | <li>Keywords are separated by line breaks, and each keyword can contain up to 20 letters.</li><li>You can add up to 500 keywords at a time.</li><li>You can add up to 2,000 keywords in total.</li> |
>? After configuring the custom dictionary, you can associate it with the policy created in [Step 1. Configure a task policy](https://intl.cloud.tencent.com/document/product/1122/43831#step1).

## Step 3. Create a task and get the recognition result

After completing the above steps, you can call the **image moderation** API to create an album moderation task as instructed below:

- Make sure that the images meet the **file format requirements** of the API.
- Enter the input parameters as instructed in the **API documentation**.
- If the task is created successfully, the API will return the detailed recognition result, and you can refer to **Image Content Recognition Sample** for more information on sample response parameters. If task creation failed, the API will return an error code, and you can refer to **Business Error Codes** and **Common Error Codes** for troubleshooting.

>? When connecting to the service, you can use **API Explorer** for online debugging.

## Relevant Documents

- Best practices for recognizing audio stream content (such as game live streaming, radio, and voice chat).
- Best practices for batch recognizing video stream content (such as live room and video conferencing).
- Best practices for recognizing forum comments (such as shopping website reviews, community replies, and video comments). For more information, see [Forum Comment Moderation](https://intl.cloud.tencent.com/document/product/1121/43774).