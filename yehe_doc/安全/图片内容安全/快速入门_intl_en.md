## Step 1. Sign up

Sign up for a Tencent Cloud account as instructed in [Signing up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985).

>? You can skip this step if you already have a Tencent Cloud account.

## Step 2. Create a sub-account (optional)

The account created when you [sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) is the root account, which has the management permissions of all resources under it. If you need your team members to assist you in managing resources under your account, you can use the CAM feature to create one or more sub-accounts, bind permission policies to them, and then assign them to team members. For detailed directions, see [Creating Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).

A newly created sub-account has no permissions by default and requires the root account or admin to bind a policy to it before it can have the operation permissions of certain resources. You can configure access to IMS with CAM for sub-accounts as instructed in [CAM Authorization Guide](https://intl.cloud.tencent.com/document/product/1122/43794).

## Step 3. Activate the service

#### Prerequisites

- You already have a Tencent Cloud root account or sub-account.
- The logged-in account already has the read/write permissions of IMS.

#### Directions

1. Log in to the [IMS console](https://console.cloud.tencent.com/cms/image) and select any menu under **IMS** on the left sidebar.

2. Click **Activate Now** on the right of the page.


## Step 4. Configure a policy (optional)

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
   ![img](https://qcloudimg.tencent-cloud.cn/raw/08c9d8b08ed25233fec969e32b9a4275.png)
3. On the **Policy Configuration** page, enter the relevant information of the policy and click **Next**.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/1bb959f65b6337413108e36be00e95c8.png)

Parameter description:

| Parameter | Description |
| :----------- | :----------------------------------------------------------- |
| Policy Name     | Text description of the policy, which can contain up to 30 letters, digits, and underscores. |
| Biztype Name  | Specific policy number used for API calls, which can contain 3–32 letters, digits, and underscores and must be unique. |
| Associated Service Template | Not required currently.                                               |
| Industry Category     | Category of the industry scenario involved in the policy.                                       |
| Use Industry Template | It will be displayed only when **Industry Category** is set. You can select whether to use Tencent Cloud's preset industry templates for moderation. |

4. On the **Recognition Policy Configuration** page, select whether to moderate different types of content based on your business needs and click **Next**.

5. On the **Custom Library Configuration** page, select a custom dictionary for content moderation in the **Custom Dictionary** drop-down list. If there are no custom libraries, you can click **Next** or save the current policy and go to [Step 5. Configure a custom dictionary](https://intl.cloud.tencent.com/document/product/1122/43811#step5).
   ![img](https://qcloudimg.tencent-cloud.cn/raw/1743e53d597a1b9c15711ba9e9ceaf03.png)

6. On the **Creation Completion** page, you can view the policy configuration information. After confirming it, click **Complete**.

7. The policy just created will be displayed in the list on the right of the **Policy Management** page.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/90df409180a6f957022b657f9bf254ff.png)

## Step 5. Configure a custom dictionary (optional)

You can configure a custom dictionary to recognize whether images contain non-compliant text.

>! You can skip this step if you don't need to configure a custom dictionary.

#### Prerequisites

- You already have a Tencent Cloud root account or sub-account.
- The logged-in account already has the read/write permissions of IMS.
- The logged-in account has activated IMS.

#### Directions

1. Log in to the [IMS console](https://console.cloud.tencent.com/cms/image) and select **IMS** > **Custom Library Management** > **Custom Dictionary** on the left sidebar.
2. On the **Custom Dictionary** page, click **Add Dictionary** to pop up the **Create Dictionary** window.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/2d87bbe2889b6826be05900467448873.png)
3. In the **Create Dictionary** pop-up window, configure a custom library based on your business needs.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/2d100424d2ed06f95212e9b9829838e3.png)

Parameter description:

| **Parameter** | **Description**                                                     |
| :----------- | :----------------------------------------------------------- |
| Dictionary Name     | Text description of the dictionary, which can contain up to 32 letters, digits, and underscores. |
| Handling Suggestion     | You can select **Non-compliant** or **Suspected**.<li>Non-compliant: the information is identified as non-compliant information</li><li>Suspected: the information may be non-compliant and requires manual moderation</li> |
| Match Mode     | For Chinese characters, both exact matching and fuzzy matching are supported. For alphabet letters, only fuzzy matching is supported. <li>Exact match: it exactly matches the entered text</li><li>Fuzzy match: it detects variants of the entered keyword to fuzzily match similar words such as split words, homographs, homophones, upper and lower cases, and numbers in words</li> |

4. Click **OK**.

5. The dictionary just created will be displayed in the list below the **Custom Dictionary** tab.

>? Different colors in a custom dictionary represent different blocking logics, where red represents "non-compliant", and orange represents "suspected".

![img](https://qcloudimg.tencent-cloud.cn/raw/8282589c23b7164a77cf2ecb658454d0.png)

6. On the **Custom Dictionary** page, select the dictionary just created and click **Manage** in the **Operation** column to enter the dictionary management page.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/8b26fdc5b929aa1f1e153b3ff88a95fa.png)

7. On the dictionary management page, click **Add Sample**, select the handling suggestion, enter keywords, and click **OK**.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/a25ae4c541e27dc0bea7e362cfa2c4d2.png)

Parameter description:

| **Parameter** | **Description**                                                     |
| :----------- | :----------------------------------------------------------- |
| Handling Suggestion     | Violation type that corresponds to the recognition model.                                       |
| Keyword       | <li>Keywords are separated by line breaks, and each keyword can contain up to 20 letters.</li><li>You can add up to 500 keywords at a time.</li><li>You can add up to 2,000 keywords in total.</li> |

>? After configuring the custom dictionary, you can associate it with the policy created in [Step 4. Configure a policy](https://intl.cloud.tencent.com/document/product/1122/43811#step4).

## Step 6. Try out the service

After completing the above steps, you can select the created moderation policy and moderate an image to try out the IMS service.

#### Prerequisites

- You already have a Tencent Cloud root account or sub-account.
- The logged-in account already has the read/write permissions of IMS.
- The logged-in account has activated IMS.

#### Directions

1. Log in to the [IMS console](https://console.cloud.tencent.com/cms/image) and select **IMS** > **Demo** on the left sidebar.
2. On the **Demo** page, select the desired policy and specify the image to be moderated in any of the following ways:
   - Enter the URL or COS access address of the image to be moderated in the **Content** input box and click **Add Online Image**.
   - Click **Select File** to directly upload a local image.

![img](https://qcloudimg.tencent-cloud.cn/raw/788ff5b13037b4e24dc1e1fcd2c996c1.png)

>? The image file must meet the following requirements:
>- Image file format: PNG, JPG, JPEG, BMP, GIF, or WEBP.
>- Image file size: below 5 MB.
>- Image resolution: a resolution above 256×256 is recommended; otherwise, the recognition effect may be affected.
>- Supported image URL transfer protocols: HTTP and HTTPS.

3. Click **Moderate Now**, and the moderation result of the image will be displayed below the image.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/86bf895945f9b8b3694c3eb74af3b2ba.png)

## Step 7. Connect the service

To connect to IMS, you need to call APIs. For detailed directions, see [API Connection Guide](https://intl.cloud.tencent.com/document/product/1122/43821).

>?
> Before calling APIs, you need to get the Tencent Cloud API access key in the following steps. Tencent Cloud uses `SecretId` and `SecretKey` to verify your identity and permissions.
> Go to the [TencentCloud API key management](https://console.cloud.tencent.com/cam/capi) page, select **CAM** > **API Key Management** on the left sidebar, click **Create Key** to create a key, and save the `SecretId` and `SecretKey` for subsequent API calls.
