The storage feature of Cloud Infinite (CI) is based on Cloud Object Storage (COS). A bucket is a carrier of images stored on Tencent Cloud COS. You can create and manage buckets through Tencent Cloud Console, APIs, or SDKs. A bucket can store multiple objects.
## Directions
You can bind or create a bucket in CI Console and customize it after the creation.
1. Log in to [CI Console](https://console.cloud.tencent.com/ci/index). In the left sidebar, click **Bucket Management** to go to the bucket management page. Then, click **Bind Bucket**, and the **Bind Bucket** dialog box appears.
![](https://main.qcloudimg.com/raw/fa3e24e28f40d8d446331ea02c724773.png)

2. Select the **Bind an existing COS bucket** or **Create** checkbox. If you select **Bind an existing COS bucket**, you need to specify the bucket name. If you select **Create**, you need to enter a name for the bucket, select a region and access permission, and set whether to enable CDN acceleration. Then, click **OK** to create the bucket. For information about the configuration items, see Notes.
![Creating a bucket](https://main.qcloudimg.com/raw/16d7ddb899019e6f17c7f179dc614903.png)

### Notes
### Methods of adding a bucket
There are two methods:
a. Create: This creates a bucket. Since the storage of CI is based on COS, you can query the newly created bucket in [COS Console](https://console.cloud.tencent.com/cos5/index).
b. Choose an existing COS bucket. By selecting this option, you actually activate the image processing service for a COS bucket.

>You can bind up to 200 buckets across regions, but the numbers of directories and files in a bucket are unlimited.


### Project
A bucket is created under a project and only belongs to one project. The project cannot be changed once being selected.

### Name
a. The bucket name can only contain numbers, lowercase letters, and dashes (**-**) with a length no greater than 40 characters.
b. The bucket name must be unique across all projects under the same APPID.

### Access permissions
Two access permissions are available for buckets by default: Public Read/Private Write and Private Read/Write.
a. Public Read/Private Write: Anyone including anonymous visitors can read objects in the bucket. However, only the bucket creator and authorized accounts can write to objects in the bucket.
b. Private Read/Write: Only the bucket creator and authorized accounts can read and write to bucket files.
c. You can modify the access permission in COS Console later when needed.

### CDN acceleration
CDN acceleration is disabled by default. You can enable or disable it as needed. When this feature is enabled, you can accelerate access by transferring files through Tencent CDN nodes.
