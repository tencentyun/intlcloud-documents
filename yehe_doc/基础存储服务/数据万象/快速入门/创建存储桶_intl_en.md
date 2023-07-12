CI provides the storage feature based on [Cloud Object Storage (COS)](https://intl.cloud.tencent.com/document/product/436). A bucket is a carrier that stores images in COS. You can use the Tencent Cloud console, API, or SDK to create and manage buckets. A bucket can store multiple objects.


## Directions

You can bind or create a bucket in the CI console and customize it after the creation.
1. Log in to the [CI console](https://console.cloud.tencent.com/ci/index) and click **Bucket Management** in the left sidebar to go to the **Bucket Management** page.
2. Click **Bind Bucket**. The **Bind Bucket** dialog box appears.
2. Select **Bind an existing COS bucket** or **Create**.
 - If you select **Bind an existing COS bucket**, specify the bucket name.
 - If you select **Create**, enter a custom name for the bucket, select a region and access permission, and set whether to enable CDN acceleration. Then, click **OK** to create the bucket. For more information on the configuration items, see "Notes".
![](https://main.qcloudimg.com/raw/16d7ddb899019e6f17c7f179dc614903.png)

## Notes
### Methods of adding a bucket
There are two methods to add a bucket:
- Create a bucket. Since the storage feature of CI is based on COS, you can query the newly created bucket in the [COS console](https://console.cloud.tencent.com/cos4/index).
- Select an existing COS bucket. If you choose to use this method, you are actually activating the image processing service for an existing bucket in COS.

> You can bind up to 200 buckets across regions, but the numbers of directories and files in a bucket are unlimited.


### Project
A bucket is created under a project and belongs to only one project. The project cannot be changed once it is selected.

### Name
a. The bucket name is a string with up to 50 characters and contains only digits, lowercase letters, and hyphens (-).
b. The bucket name must be unique across all projects under the same APPID.

### Region

CI supports multi-region storage. For more information on regions where this feature is available, see [Regions and Domain Names](https://intl.cloud.tencent.com/document/product/1045/33423). When creating a bucket, you can select a region for the bucket. The region cannot be changed once selected. To improve the access speed, we recommend that you select a region close to your location.



### Access permissions
The following three access permissions are granted for a bucket by default:
-. Private Read/Write: only the bucket creator and authorized accounts have permission to read and write objects in the bucket.
- Public Read/Private Write: anyone, including anonymous visitors, can read objects in the bucket. However, only the bucket creator and authorized accounts can write objects in the bucket.
- Public Read/Write: anyone, including anonymous visitors, can read and write objects in the bucket. We recommend that you do not select this access permission.

> You can modify the access permission in the [COS console](https://console.cloud.tencent.com/cos5) later when needed.

### CDN acceleration
CDN acceleration is disabled by default. You can enable or disable it as needed. When CDN acceleration is enabled, users can accelerate access by transferring files through Tencent CDN nodes.
