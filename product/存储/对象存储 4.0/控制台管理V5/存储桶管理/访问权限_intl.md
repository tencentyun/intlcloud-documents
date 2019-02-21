## Product Introduction

Users can modify bucket access permissions in the console or through APIs. The COS Console by default supports two types of access permissions: Public Read/Private Write, and Private Read/Write.

- Public Read/Private Write: Anyone (including anonymous visitors) has read permission to the objects in the bucket, but only the bucket creator and accounts with the appropriate permissions have write permission to the objects in the bucket. 
- Private Read/Write: Only the creator of the bucket and accounts with the appropriate permissions have read and write permissions to the files in the bucket.

## Procedure

Users can select the access permission to a bucket when [creating a bucket](https://cloud.tencent.com/document/product/436/6232). Users can also modify the access permission to a bucket in Basic Configuration by following the steps below:

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos4/index) , click **Bucket List** on the left navigation pane, and click the bucket (such as example) for which you want to modify the access permission to enter the bucket details page.
   ![](//mc.qcloudimg.com/static/img/b51d5a77d53c3416324ea3eb283c788c/image.png)
2. Click **Basic Configuration**, find **Access Permissions** under **Basic Information**, and click the **Edit** button to edit the access permission to the bucket.
   ![](//mc.qcloudimg.com/static/img/2c3e0f2bae1c673ef507ddd642c50fd5/image.png)
3. Modify the access permission (for example, changing the bucket access permission from Public Read/Private Write to Private Read/Write), and click **Save** to complete the modification.
   ![](//mc.qcloudimg.com/static/img/f266c0326c89ee1c9d8f545be0504b4d/image.png)
