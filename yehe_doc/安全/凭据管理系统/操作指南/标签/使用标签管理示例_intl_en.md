### Overview

* Tags are used to manage resource classification and permissions from different dimensions.
* For [SSM](https://console.cloud.tencent.com/ssm), tags are used for **User Credentials**.
* By adding tags to a secret, you can classify, track, and manage secrets more easily. Also, you can summarize the usage of secrets according to their tags.



### Use Limits

There are some limits on the usage of tags (tag key and tag value). For more information, please see [Use Limits](https://intl.cloud.tencent.com/document/product/651/13354).

### Directions

#### Setting tags in the SSM console

1. Log in to the [SSM console](https://console.cloud.tencent.com/ssm).
2. Select the region where the secret to be edited is located.
3. Find the secret whose tags need to be edited and click **Edit Tag** on the right. 

![](https://main.qcloudimg.com/raw/adb1764eb082e54e282b0148cad120ff.png)

4. Set the tags in the "1 resource selected" section of the pop-up window.

   The following figure shows you how to add two sets of tags.

   ![](https://main.qcloudimg.com/raw/64831a56619eb1a9fbc80ba2f040f826.png)

   5. Click **OK**. A message indicating the edit was successful will be prompted.   

      

#### Filtering keys with tags

1. Log in to the [SSM console](https://console.cloud.tencent.com/ssm).

2. Select the region where the secret to be edited is located.

3. In the **Credential List** of the selected region, use **tags** as the filter criteria, enter the filter content, and press the Enter key, as shown in the following figure.

   For example, if you want to filter keys whose owner is alex, you can enter the "owner:alex" tag.![](https://main.qcloudimg.com/raw/d2d91d47fad9dd2465094aece1aa4a2b.png)