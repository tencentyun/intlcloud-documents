CI is a data processing platform based on COS. You can use CI features only after binding or creating a COS bucket.

The bucket management page provides the **bucket binding**, **bucket creation**, **bucket unbinding**, and **bucket search** features.


## Prerequisites

You need to log in to the CI Console and click **Bucket Management** on the left sidebar to enter the bucket list page.

## Binding Bucket

You can bind an existing COS bucket in the following steps:

1. Click **Bind Bucket** to pop up the bucket binding dialog box.
>?During the binding, you need to create a preset service role, grant it CI-related permissions, and complete service authorization as prompted.

2. Click the COS bucket to be bound and select whether to enable CDN acceleration.
   
>?Binding a COS bucket is essentially to enable the image processing service for it.

## Creating Bucket



You can create a bucket in the following steps:

1. Click **Bind Bucket** to pop up the bucket binding dialog box.
2. Select **Create** as the adding method, enter the custom bucket name, select the bucket region, access permission, and whether to enable CDN acceleration, and click **OK** to quickly create a bucket. The configuration items are as detailed below:
>?
>
>-  The new bucket can also be queried in the COS Console. If you want to configure the bucket in a more detailed manner, please go to the [COS Console](https://console.cloud.tencent.com/cos5/bucket#).
>-  There can be up to 200 buckets in total in all regions under one account, but the numbers of directories and files in a bucket are not limited.

 - **Bucket Name**
   - A bucket name can contain up to 50 digits, lowercase letters, and hyphens.
   - The bucket name must be unique in all projects under the same `APPID`.
 - **Region**
   The storage service can be used in multiple regions. For the available regions, please see [Regions and Domain Names](https://intl.cloud.tencent.com/document/product/1045/33423). You can select the bucket region when creating a bucket, and once selected, it cannot be changed. To make access faster, we recommend you select an available region near your users.
 - **Access Permission**
   Three types of bucket access permissions are available by default, i.e., "Private Read/Write", "Public Read/Private Write", and "Public Read/Write". If needed, you can modify the access permission in the [COS Console](https://console.cloud.tencent.com/cos5) subsequently.
    - Private Read/Write: only the creator of the bucket and authorized accounts can read/write the objects in the bucket, while others cannot.
    - Public Read/Private Write: anyone (including anonymous visitors) has read permission to the objects in the bucket, but only the bucket creator and authorized accounts have write permission to them.
    - Public Read/Write: anyone (including anonymous visitors) has read/write permission to the objects in the bucket, which is not recommended.
 - **CDN Acceleration**
   CDN acceleration is disabled by default. You can enable/disable it as needed. After it is enabled, you can relay files on Tencent Cloud CDN nodes to make the access faster.



## Unbinding Bucket

If you no longer use a bucket, you can unbind it.

Click **Unbind** in the "Operation" column on the right of the target bucket to pop up the bucket unbinding dialog box. Click **OK** to unbind it.

>!Currently, CI **does not allow** you to delete buckets. Once unbound, a bucket will be deleted from the CI's bucket list, but it and all its contents will be retained in COS. You can go to the [COS Console](https://console.cloud.tencent.com/cos5) to view it in the bucket list.

## Searching for Bucket

If you want to query a bucket bound to CI, you can select **Bucket name** or **Bucket tag** in the drop-down list on the right for filtering.

   
