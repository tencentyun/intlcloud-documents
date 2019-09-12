## Overview

Users can modify bucket access permissions in the console or via APIs. The COS Console by default supports two types of access permissions: Public Read/Private Write, and Private Read/Write.

- Public Read/Private Write: anyone, including anonymous visitors has read permission to objects in the bucket. However, only the bucket creator and authorized accounts have write permission to objects in the bucket.
- Private Read/Write: only the bucket creator and authorized accounts have read and write permissions to bucket files.

>After setting the access permission of the storage bucket, it can be modified in the "permission management" of the storage bucket.

## Setting Up Access Permissions

Users can select the access permission to a bucket when [creating a bucket](https://intl.cloud.tencent.com/document/product/436/6232). Users can also modify the access permission to a bucket in Basic Configuration by following the steps below:

1. Log in to the [COS console], click **Bucket List** from the left side bar, click the bucket (such as example) you want to modify access permission for, and enter the bucket detail page.
   ![](https://main.qcloudimg.com/raw/695c2f7e68ef417a9f1a0809fcd804fc.png)
2. Modify the access permission (for example, changing the bucket access permission from Public Read/Private Write to Private Read/Write), and click **Save** to complete the modification.
   ![](https://main.qcloudimg.com/raw/6fb49a9d5a81e91fd06a56fe69ca7cff.png)
