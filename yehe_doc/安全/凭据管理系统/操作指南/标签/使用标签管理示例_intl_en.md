### Overview

* Tags are used to manage resource classification and permissions from different dimensions.
* For [SSM](https://console.cloud.tencent.com/ssm), tags are used for **User Credentials**.
* By adding tags to a secret, you can classify, track, and manage secrets more easily. Also, you can summarize the usage of secrets according to the tags.



### Use Limits

There are some limits on the usage of tags (tag key and tag value). For more information, please see [Use Limits](https://intl.cloud.tencent.com/document/product/651/13354).

### Directions

#### Setting tags in the SSM Console

1. Log in to the [SSM Console](https://console.cloud.tencent.com/ssm).
2. Select the region where the secret to be edited is located.
3. Find the secret whose tags need to be edited and click **Edit Tag** on the right. 

![](https://main.qcloudimg.com/raw/adb1764eb082e54e282b0148cad120ff.png)

4. In the "1 resource selected" area in the pop-up window, set the tags.

   The following figure shows how to add two sets of tags.

   ![](https://main.qcloudimg.com/raw/64831a56619eb1a9fbc80ba2f040f826.png)

   5. Click **OK**. A message indicating the editing success will be prompted.   

      

#### Filtering keys with tags

1. Log in to the [SSM Console](https://console.cloud.tencent.com/ssm).

2. Select the region where the secret to be edited is located.

3. In the **Credential List** of the selected region, use **tags** as the filter criteria, enter the filter content, and press Enter, as shown in the following figure.

   For example, if you want to filter keys whose owner is alex, you can enter the "owner:alex" tag.![](https://main.qcloudimg.com/raw/d2d91d47fad9dd2465094aece1aa4a2b.png)