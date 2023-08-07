## Step 1. Sign up and log in

Sign up as instructed in [Signing up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/10496).

>? You can skip this step if you already have a Tencent Cloud account.

## Step 2. Create a sub-account (optional)

The account created when you [sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) is the root account, which has the management permissions of all resources under it. If you need your team members to assist you in managing resources under your account, you can use the CAM feature to create one or more sub-accounts, bind permission policies to them, and then assign them to team members. For detailed directions, see [Creating Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).

A newly created sub-account has no permissions by default and requires the root account or admin to bind a policy to it before it can have the operation permissions of certain resources. You can configure access to CMS with CAM for sub-accounts as instructed in [CAM Authorization Guide](https://intl.cloud.tencent.com/document/product/1139/44945).

## Step 3. Activate the service

#### Prerequisites

You already have a Tencent Cloud root account or sub-account.

#### Directions

1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/audio/overview) and select any menu under **AMS** on the left sidebar.

2. Click **Activate Now** on the right of the page.

   After the service is activated, the console will pop up a window to ask for resource authorization. Click **Authorize** to enter the role management page.

3. On the role management page, click **Agree**. After completing authentication, you can authorize COS resources and then test or use the AMS service normally.

## Step 4. Configure a policy (optional)

We recommend you configure a recognition policy based on your business needs for a personalized user experience.

>?
>- You can skip this step if you use the preset default policy of Tencent Cloud CMS.
>- The default policy is developed by TenDI based on models for multiple industries. It is suitable for most content security requirements.

#### Prerequisites

- You already have a Tencent Cloud root account or sub-account.
- The logged-in account has activated AMS.

#### Directions

1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/audio/overview) and select **AMS** > **Policy Management** on the left sidebar.

2. On the **Policy Management** page, click **Create Policy** to enter the **Create Policy** page.
   <img src="https://qcloudimg.tencent-cloud.cn/raw/170ecda3857b431040ea5442702f09dc.png" alt="image-20220119095904646" style="zoom:100%;" />

3. On the **Policy Configuration** page, enter the relevant information of the policy and click **Next**.

   ![](https://qcloudimg.tencent-cloud.cn/raw/280b7855724b5f4b980d8f589265293f.png)

   Parameter description:

   | Parameter | Description |
   | :----------- | :----------------------------------------------------------- |
   | Policy Name     | Text description of the policy, which can contain up to 30 letters, digits, and underscores. |
   | Biztype Name  | Specific policy number used for API calls, which can contain 3–32 letters, digits, and underscores and must be unique. |
   | Associate Service Template | Currently, only the default template can be used for configuration. |
   | Industry Category     | Category of the industry scenario involved in the policy.                                       |
   | Use Industry Template | It will be displayed only when **Industry Category** is set. You can select whether to use Tencent Cloud's preset industry templates for recognition. |

4. On the **Recognition Policy Configuration** page, select whether to recognize different types of content based on your business needs and click **Next**.

5. On the **Custom Library Configuration** page, select a custom dictionary for content recognition in the **Custom Dictionary** drop-down list. If there are no custom libraries, you can click **Next** or save the current policy and go to [Step 6. Configure a custom dictionary](https://intl.cloud.tencent.com/document/product/1139/44942#step6).
   ![](https://qcloudimg.tencent-cloud.cn/raw/eaf3d550bbce1a6a2e2a1e67112f764e.png)

6. On the **Creation Completion** page, you can view the policy configuration information. After confirming it, click **Complete**.

7. The policy just created will be displayed in the list on the right of the **Policy Management** page.
   ![](https://qcloudimg.tencent-cloud.cn/raw/9e81cf03e5b67eb9392807001b1c9f58.png)

## Step 5. Configure a global task template (optional)

Task templates are used to manage how files are processed for recognition tasks.

>? You can skip this step if the default template is used.

#### Prerequisites

- You already have a Tencent Cloud root account or sub-account.
- The logged-in account has activated AMS.

#### Directions

1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/audio/overview) and select **AMS** > **Service Management** on the left sidebar.

2. On the service management page, click **View Details** to enter the template details page.

   >? Currently, only the default template can be edited for template configuration.

   ![](https://qcloudimg.tencent-cloud.cn/raw/845406571f83aa9189c13627dd826d89.png)

3. On the template details page, click **Edit** in the top-right corner to modify parameters.

   ![](https://qcloudimg.tencent-cloud.cn/raw/85ff392280e541710463887442af5244.png)

   Parameter description:

   | Parameter | Description |
   | :--------------------- | :----------------------------------------------------------- |
   | Template Name     | Text description of the template, which can contain up to 30 letters, digits, and underscores. |
   | Audio Stream or Large File Segment Duration | Set the time length for audio stream or large file segmentation, which can be 15s, 30s (default), or 60s. |
   | Callback Address | The risky content can be returned to this optional address (if entered). |
   | Enable Full Callback for Live Streaming | Set whether to enable full callback for live streaming. **Enable**: both normal and non-compliant audio content will be returned to the callback address. **Disable**: only the non-compliant audio content will be returned to the callback address. |

4. Click **Save** to save the current template, which will take effect immediately for all AMS services under the account.

## Step 6. Configure a custom dictionary (optional)

You can configure a custom dictionary.

>? You can skip this step if you don't need to configure a custom dictionary.

#### Prerequisites

- You already have a Tencent Cloud root account or sub-account.
- The logged-in account has activated AMS.

#### Directions

1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/audio/lib) and select **AMS** > **Custom Library Management** > **Custom Dictionary** on the left sidebar.

2. On the **Custom Dictionary** page, click **Add Dictionary** to pop up the **Create Dictionary** window.
   <img src="https://qcloudimg.tencent-cloud.cn/raw/94ca57968d09c77fdf6af3e273bf7b16.png" alt="image-20220119102250545" style="zoom:100%;" />

3. In the **Create Dictionary** pop-up window, configure a custom library based on your business needs.

   <img src="https://qcloudimg.tencent-cloud.cn/raw/e05cc82e9a10efec343985fcb13d1424.png" alt="image-20220119102418549" style="zoom:100%;" />

   Parameter description:

   | **Parameter** | **Description**                                                     |
   | :----------- | :----------------------------------------------------------- |
   | Dictionary Name     | Text description of the dictionary, which can contain up to 32 letters, digits, and underscores. |
   | Handling Suggestion     | You can select **Non-compliant** or **Suspected**. **Non-compliant**: the information is identified as non-compliant information. **Suspected**: the information may be non-compliant and requires manual recognition. |
   | Match Mode     | For Chinese characters, both exact matching and fuzzy matching are supported. For alphabet letters, only fuzzy matching is supported.<li>Exact match: it exactly matches the entered text</li><li>Fuzzy match: it detects variants of the entered keyword to fuzzily match similar words such as split words, homographs, homophones, upper and lower cases, and numbers in words</li> |

4. Click **OK**.

5. The dictionary just created will be displayed in the list below the **Custom Dictionary** tab.

   >? Different colors in a custom dictionary represent different blocking logics, where red represents "non-compliant", and orange represents "suspected".

   ![](https://qcloudimg.tencent-cloud.cn/raw/f91b8844df1a0800df3dc6ced9e9dc18.png)

6. On the **Custom Dictionary** page, select the dictionary just created and click **Manage** in the **Operation** column to enter the dictionary management page.
   ![](https://qcloudimg.tencent-cloud.cn/raw/cbbc81103c2add0d1b8ae63a87d70da2.png)

7. On the dictionary management page, click **Add Sample** to pop up the **Add Sample** window.

8. In the **Add Sample** pop-up window, select the handling suggestion, enter keywords, and click **OK**.

   <img src="https://qcloudimg.tencent-cloud.cn/raw/f26e811e9874b1519f600a1a12d31236.png" alt="image-20220119110310839" style="zoom:80%;" />

   Parameter description:

   | **Parameter** | **Description**                                                     |
   | :----------- | :----------------------------------------------------------- |
   | Handling Suggestion     | Violation type that corresponds to the recognition model.                                       |
   | Keyword       | Keywords are separated by line breaks, and each keyword can contain up to 20 letters. You can add up to 500 keywords at a time. You can add up to 2,000 keywords in total. |

   >? After configuring the custom dictionary, you can associate it with the policy created in [Step 4. Configure a policy](https://intl.cloud.tencent.com/document/product/1139/44942#step4).

## Step 7. Try out the service

After completing the above steps, you can select the created recognition policy and recognize audio to try out the AMS service.

#### Prerequisites

- You already have a Tencent Cloud root account or sub-account.
- The logged-in account has activated AMS.

#### Directions

1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/image) and select **AMS** > **Demo** on the left sidebar to enter the **Demo** page.

2. On the **Demo** page, select the desired policy and specify the audio to be recognized in any of the following ways:

   - Local Upload: click **Click to Upload** and select the local file to be uploaded.

   - URL Upload: enter the URL or COS storage address of the content to be recognized in the input box.

     >? The audio file must meet the following requirements:
     >- Audio file size: below 50 MB.
     >- Audio file duration: below 3 minutes.
     >- Audio bitrate: 128–256 Kbps.
     >- Audio file format: WAV, MP3, AAC, FLAC, AMR, 3GP, M4A, WMA, OGG, or APE.

3. Click **Recognize Now**, and the recognition result will be displayed at the bottom of the page after the system recognizes the audio.

## Step 8. Connect the service

To connect to AMS, you need to call APIs. 
>? 
>- Before calling APIs, you need to get the Tencent Cloud API access key in the following steps. Tencent Cloud uses `SecretId` and `SecretKey` to verify your identity and permissions.
>- Go to the [TencentCloud API key management](https://console.cloud.tencent.com/cam/capi) page, select **CAM** > **API Key Management** on the left sidebar, click **Create Key** to create a key, and save the `SecretId` and `SecretKey` for subsequent API calls.
