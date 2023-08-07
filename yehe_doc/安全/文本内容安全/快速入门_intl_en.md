## Step 1. Sign up

Sign up for a Tencent Cloud account as instructed in [Signing up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985).

>?  You can skip this step if you already have a Tencent Cloud account.

## Step 2. Create a sub-account (optional)

The account created when you [sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) is the root account, which has the management permissions of all resources under it. If you need your team members to assist you in managing resources under your account, you can use the CAM feature to create one or more sub-accounts, bind permission policies to them, and then assign them to team members. For detailed directions, see [Creating Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).

A newly created sub-account has no permissions by default and requires the root account or admin to bind a policy to it before it can have the operation permissions of certain resources. You can configure access to TMS with CAM for sub-accounts as instructed in [CAM Authorization Guide](https://intl.cloud.tencent.com/document/product/1122/43795).

## Step 3. Activate the service

#### Prerequisites

- You already have a Tencent Cloud root account or sub-account.
- The logged-in account already has the read/write permissions of TMS.

#### Directions

   Log in to the [CMS console](https://console.cloud.tencent.com/cms/text/overview) and select any menu under **TMS** on the left sidebar.

## Step 4. Configure a policy (optional)

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
   ![img](https://qcloudimg.tencent-cloud.cn/raw/f5062b405a596d1b84d91a8077a5afd6.png)
3. On the **Policy Configuration** page, enter the relevant information of the policy and click **Next**.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/76c0f812e3773f720ffadf020a67e4be.png)

Parameter description:

| Parameter | Description |
| :----------- | :----------------------------------------------------------- |
| Policy Name     | Text description of the policy, which can contain up to 30 letters, digits, and underscores. |
| Biztype Name  | Specific policy number used for API calls, which can contain 3–32 letters, digits, and underscores and must be unique. |
| Industry Category     | Category of the industry scenario involved in the policy.                                       |
| Use Industry Template | It will be displayed only when **Industry Category** is set. You can select whether to use Tencent Cloud's preset industry templates for moderation. |

4. On the **Recognition Policy Configuration** page, select whether to moderate different types of content based on your business needs and click **Next**.

5. On the **Custom Library Configuration** page, select a custom dictionary for content moderation in the **Custom Dictionary** drop-down list. If there are no custom libraries, you can click **Next** or save the current policy and go to [Step 5. Configure a custom dictionary](https://intl.cloud.tencent.com/document/product/1121/43753#step5).
   ![img](https://qcloudimg.tencent-cloud.cn/raw/e75d7dd06b8db0c5757267837c1a72aa.png)

6. On the **Creation Completion** page, you can view the policy configuration information. After confirming it, click **Complete**.

7. The policy just created will be displayed in the list on the right of the **Policy Management** page.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/4cdd6eedb8c5f0ceb8d660de78970bde.png)

## Step 5. Configure a custom dictionary (optional)

You can configure a custom dictionary to recognize whether images contain non-compliant text.

>?  You can skip this step if you don't need to configure a custom dictionary.

#### Prerequisites

- You already have a Tencent Cloud root account or sub-account.
- The logged-in account already has the read/write permissions of TMS.
- The logged-in account has activated TMS.

#### Directions

1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/image) and select **TMS** > **Custom Library Management** > **Custom Dictionary** on the left sidebar.
2. On the **Custom Dictionary** page, click **Add Dictionary** to pop up the **Create Dictionary** window.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/9c787cef81a30a169fa039abc959ca7f.png)
3. In the **Create Dictionary** pop-up window, configure a custom library based on your business needs.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/8daf8b3a269c9817c59b4f491e23ae24.png)

Parameter description:

| **Parameter** | **Description**                                                     |
| :----------- | :----------------------------------------------------------- |
| Dictionary Name     | Text description of the dictionary, which can contain up to 32 letters, digits, and underscores. |
| Handling Suggestion     | You can select **Non-compliant** or **Suspected**.<li>Non-compliant: the information is identified as non-compliant information</li><li>Suspected: the information may be non-compliant and requires manual moderation</li> |
| Match Mode     |For Chinese characters, both exact matching and fuzzy matching are supported. For alphabet letters, only fuzzy matching is supported.<li>Exact match: it exactly matches the entered text</li><li>Fuzzy match: it detects variants of the entered keyword to fuzzily match similar words such as split words, homographs, homophones, upper and lower cases, and numbers in words</li> |

4. Click **OK**.

5. The dictionary just created will be displayed in the list below the **Custom Dictionary** tab.

>? Different colors in a custom dictionary represent different blocking logics, where red represents "non-compliant", and orange represents "suspected".

![img](https://qcloudimg.tencent-cloud.cn/raw/b7eb411122609367313fc70174d42204.png)

6. On the **Custom Dictionary** page, select the dictionary just created and click **Manage** in the **Operation** column to enter the dictionary management page.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/45a32cb176110515b134c00f1a1c7541.png)

7. On the dictionary management page, click **Add Sample** to pop up the **Add Sample** window.

8. In the **Add Sample** pop-up window, select the handling suggestion, enter keywords, and click **OK**.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/c07a83e48bebeca88c0a8057a779e94e.png)

Parameter description:

| **Parameter** | **Description**                                                     |
| :----------- | :----------------------------------------------------------- |
| Handling Suggestion     | Violation type that corresponds to the recognition model.                                       |
| Keyword       | <li>Keywords are separated by line breaks, and each keyword can contain up to 20 letters.</li><li>You can add up to 500 keywords at a time.</li><li>You can add up to 2,000 keywords in total.</li> |

>? After configuring the custom dictionary, you can associate it with the policy created in [Step 4. Configure a policy](https://intl.cloud.tencent.com/document/product/1121/43753#step4).

## Step 6. Try out the service

After completing the above steps, you can select the created moderation policy and moderate text to try out the TMS service.

#### Prerequisites

- You already have a Tencent Cloud root account or sub-account.
- The logged-in account already has the read/write permissions of TMS.
- The logged-in account has activated TMS.

#### Directions

1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/image) and select **TMS** > **Demo** on the left sidebar to enter the **Demo** page.

2. On the **Demo** page, select the desired moderation policy and enter the text to be moderated.

   >? The text must meet the following requirements:
   >- **Text Content Size**: the text length cannot exceed 10,000, calculated based on Unicode encoding.
   >- **Supported Language**: Chinese.

3. Click **Moderate Now**, and the moderation result of the text will be displayed below the moderated content.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/25ed1c79570608fc343e07ba04ba52cb.png)

## Step 7. Connect the service

To connect to TMS, you need to call APIs. For detailed directions, see [API Connection Guide](https://intl.cloud.tencent.com/document/product/1121/43763).

>?
>Before calling APIs, you need to get the Tencent Cloud API access key in the following steps. Tencent Cloud uses `SecretId` and `SecretKey` to verify your identity and permissions.
>Go to the [TencentCloud API key management](https://console.cloud.tencent.com/cam/capi) page, select **CAM** > **API Key Management** on the left sidebar, click **Create Key** to create a key, and save the `SecretId` and `SecretKey` for subsequent API calls.
