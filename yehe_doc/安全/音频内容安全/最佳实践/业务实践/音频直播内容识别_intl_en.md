After activating [AMS](https://console.cloud.tencent.com/cms/audio/package), you can directly call **AMS** APIs to recognize audio stream content (such as game live streaming, radio, and voice chat).

>?
>- Before calling the API, make sure that the current account **has at least the access permission of AMS**. For more information on how to configure the permission, see [CAM Authorization Guide](https://intl.cloud.tencent.com/document/product/1139/44945).
>- If you cannot access the service, you will need to activate the service/check the billing information (for root account) or request the corresponding permission from the admin or root account (for sub-account/collaborator).

## Step 1. Configure a policy (optional)

We recommend you configure a recognition policy based on your business needs for a personalized user experience.

>?
>- You can skip this step if you use the preset default policy of Tencent Cloud CMS.
>- The default policy is developed by TenDI based on models for multiple industries. It is suitable for most content security requirements.

1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/audio/overview) and select **AMS** > **Policy Management** on the left sidebar.

2. On the **Policy Management** page, click **Create Policy** to enter the **Create Policy** page.
   <img src="https://qcloudimg.tencent-cloud.cn/raw/170ecda3857b431040ea5442702f09dc.png" alt="image-20220119095904646" style="zoom:100%;" />

3. On the **Policy Configuration** page, enter the relevant information of the policy and click **Next**.

   ![](https://qcloudimg.tencent-cloud.cn/raw/472e060a38aec28aa068b09f68893e25.png)

   Parameter description:

   | Parameter | Description |
   | :----------- | :----------------------------------------------------------- |
   | Policy Name     | Text description of the policy, which can contain up to 30 letters, digits, and underscores. |
   | Biztype Name  | Specific policy number used for API calls, which can contain 3–32 letters, digits, and underscores and must be unique. |
   | Associate Service Template | Currently, only the default template can be used for configuration. |
   | Industry Category     | Category of the industry scenario involved in the policy.                                       |
   | Use Industry Template | It will be displayed only when **Industry Category** is set. You can select whether to use Tencent Cloud's preset industry templates for recognition. |

4. On the **Recognition Policy Configuration** page, select whether to recognize different types of content based on your business needs and click **Next**.

5. On the **Custom Library Configuration** page, select a custom dictionary for content recognition in the **Custom Dictionary** drop-down list. If there are no custom libraries, you can click **Next** or save the current policy and go to [Step 3. Configure a custom dictionary](https://intl.cloud.tencent.com/document/product/1139/44952#step3).
   ![](https://qcloudimg.tencent-cloud.cn/raw/c65e9fe2383a77f80576e30904cbbbcf.png)

6. On the **Creation Completion** page, you can view the policy configuration information. After confirming it, click **Complete**.

7. The policy just created will be displayed in the list on the right of the **Policy Management** page.
   ![](https://qcloudimg.tencent-cloud.cn/raw/2e8928c0c5c612d62b039973d795eae4.png)

## Step 2. Configure a global task template (optional)

Task templates are used to manage how files are processed for recognition tasks.

>? You can skip this step if the default template is used.

1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/audio/overview) and select **AMS** > **Service Management** on the left sidebar.

2. On the service management page, click **View Details** to enter the template details page.

   >? Currently, only the default template can be edited for template configuration.

   ![](https://qcloudimg.tencent-cloud.cn/raw/a9522962d24822a73745c684fce971bf.png)

3. On the template details page, click **Edit** in the top-right corner to modify parameters.

   ![](https://qcloudimg.tencent-cloud.cn/raw/a530cd081bf816aa6cd788334f73fc3c.png)

   Parameter description:

   | Parameter | Description |
   | :--------------------- | :----------------------------------------------------------- |
   | Template Name     | Text description of the template, which can contain up to 30 letters, digits, and underscores. |
   | Audio Stream or Large File Segment Duration | Set the time length for audio stream or large file segmentation, which can be 15s, 30s (default), or 60s. |
   | Callback Address | The risky content can be returned to this optional address (if entered). |
   | Enable Full Callback for Live Streaming | Set whether to enable full callback for live streaming. **Enable**: both normal and non-compliant audio content will be returned to the callback address. **Disable**: only the non-compliant audio content will be returned to the callback address. |

4. Click **Save** to save the current template, which will take effect immediately for all AMS services under the account.

## Step 3. Configure a custom dictionary (optional)

You can configure a custom dictionary.

>? You can skip this step if you don't need to configure a custom dictionary.

1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/audio/lib) and select **AMS** > **Custom Library Management** > **Custom Dictionary** on the left sidebar.

2. On the **Custom Dictionary** page, click **Add Dictionary** to pop up the **Create Dictionary** window.
   <img src="https://qcloudimg.tencent-cloud.cn/raw/dc9857444a5805e9aadfcee2cf018396.png" alt="image-20220119102250545" style="zoom:100%;" />

3. In the **Create Dictionary** pop-up window, configure a custom library based on your business needs.

   <img src="https://qcloudimg.tencent-cloud.cn/raw/a7714daf0a1f515c0ed8647c0169cb80.png" alt="image-20220119102418549" style="zoom:100%;" />

   Parameter description:

   | **Parameter** | **Description**                                                     |
   | :----------- | :----------------------------------------------------------- |
   | Dictionary Name     | Text description of the dictionary, which can contain up to 32 letters, digits, and underscores. |
   | Handling Suggestion     | You can select **Non-compliant** or **Suspected**. **Non-compliant**: the information is identified as non-compliant information. **Suspected**: the information may be non-compliant and requires manual recognition. |
   | Match Mode     | You can select **Exact match** or **Fuzzy match**. **Exact match**: it **exactly matches** the entered text. **Fuzzy match**: it detects variants of the entered keyword to fuzzily match similar words such as split words, homographs, homophones, upper and lower cases, and numbers in words. |

4. Click **OK**.

5. The dictionary just created will be displayed in the list below the **Custom Dictionary** tab.

   >? Different colors in a custom dictionary represent different blocking logics, where red represents "non-compliant", and orange represents "suspected".

   ![](https://qcloudimg.tencent-cloud.cn/raw/a40e5270343364590503d61c74f88b3b.png)

6. On the **Custom Dictionary** page, select the dictionary just created and click **Manage** in the **Operation** column to enter the dictionary management page.
   ![](https://qcloudimg.tencent-cloud.cn/raw/74829f9fcd5190d69671293cc3e726f3.png)

7. On the dictionary management page, click **Add Sample** to pop up the **Add Sample** window.

8. In the **Add Sample** pop-up window, select the handling suggestion, enter keywords, and click **OK**.

   <img src="https://qcloudimg.tencent-cloud.cn/raw/83f19abaf6ecb7549f3cd4fdefd3faa0.png" alt="image-20220119110310839" style="zoom:50%;" />

   Parameter description:

   | **Parameter** | **Description**                                                     |
   | :----------- | :----------------------------------------------------------- |
   | Handling Suggestion     | Violation type that corresponds to the recognition model.                                       |
   | Keyword       | Keywords are separated by line breaks, and each keyword can contain up to 20 letters. You can add up to 500 keywords at a time. You can add up to 2,000 keywords in total. |

9. On the **Custom Dictionary** page, select the target dictionary and click ![img](https://main.qcloudimg.com/raw/541944ccb7722e47db44524e6174a176.png) in the **Operation** column to enable or disable it.

   >?
   >- After the custom dictionary is enabled, custom violation results will be returned in preference to the default dictionary.
   >- After the dictionary is disabled, samples in it will not be used to match and recognize audio content.

10. After configuring the custom dictionary, you can associate it with the policy created in [Step 1. Configure a policy](https://intl.cloud.tencent.com/document/product/1139/44952#step1).

## Step 4. Create an AMS task

After completing the above steps, you can call the **CreateAudioModerationTask** API to create an audio stream recognition task as instructed below:

- Make sure that the audio meets the [file format requirements](https://intl.cloud.tencent.com/document/product/1139/46101#1.-.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0) of the API.
- Enter the input parameters as instructed in the [API documentation](https://intl.cloud.tencent.com/document/product/1139/46101#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0).
- If the task is created successfully, you can use the task query API to query task details, and you can refer to the [example of creating audio moderation task](https://intl.cloud.tencent.com/document/product/1139/46101#.E7.A4.BA.E4.BE.8B1-.E5.88.9B.E5.BB.BA.E9.9F.B3.E9.A2.91.E5.AE.A1.E6.A0.B8.E4.BB.BB.E5.8A.A1) for more information on sample response parameters. If task creation fails, the API will return an error code, and you can refer to [Business Error Codes](https://intl.cloud.tencent.com/document/product/1139/46101#6.-.E9.94.99.E8.AF.AF.E7.A0.81) and [Common Error Codes](https://intl.cloud.tencent.com/document/product/1139/46099#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81) for troubleshooting.

>? When connecting to the service, you can use API Explorer for online debugging.

## Step 5. Get the AMS task result

After creating the audio recognition task, you can call the **DescribeTaskDetail** API to query the details of the task as instructed below:

- Enter the input parameters as instructed in the [API documentation](https://intl.cloud.tencent.com/document/product/1139/46100).
- If the API call is successful, you will receive the response output from the API, including the task details. You can refer to the [example of viewing task details](https://intl.cloud.tencent.com/document/product/1139/46100#4.-.E7.A4.BA.E4.BE.8B) for more information on sample response parameters.
