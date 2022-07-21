## Overview
If there are resources for multiple business units or projects under your account, you can use tags to manage access to different resources and allocate your costs. You can also set quotas for a tag (key-value pair) in the Tag console.

A tag quota is the maximum number of resources a key-value pair can be bound to.
For example, suppose you set the CVM instance quota for the tag `Application:Official Application` to 100 (the highest quota you can set is the total number of CVM instances under your account). When you try to bind the 101st CVM instance to the tag, an error will occur saying that the limit has been reached.

>? Currently, the tag quota feature is only available to beta users. If you want to try it, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).

## Prerequisites
You have created a tag. For detailed directions, see [Creating Tags](https://intl.cloud.tencent.com/document/product/651/41684).

## Directions

### Creating a tag quota
1. Log in to the Tag console with a root account or an account with sub-account management permission. Select [Tag Quota](https://console.cloud.tencent.com/tag/quota) on the left sidebar.
2. Click **New**.
3. In step 1, select a tag key and tag value.
4. In step 2, select the resource type and region and enter a quota.
	- You can configure quotas for the same resource type in different regions (by clicking **Add +**).
	- You can also configure tag quotas for different resource types (by clicking **Add +**).
	

![](https://qcloudimg.tencent-cloud.cn/raw/0819d2c79b50b973c884e60ecbc9e230.png)
>?
>- You can configure quotas for only one tag at a time on the quota creation page.
>- You cannot configure two quotas for the same resource type in the same region.
>- The quota you set for a tag must be higher than the number of resources already bound to the tag.
>- Currently, you can only set tag quotas for CVM instances.
>
5. Click **Create**. The quota created will appear in the quota list.



### Viewing and modifying tag quotas
#### Viewing tag quotas
1. Log in to the Tag console and select [Tag Quota](https://console.cloud.tencent.com/tag/quota) on the left sidebar.
2. In the quota list, find the tag whose quota information you want to view, and click **View** to go to the details page.
![](https://qcloudimg.tencent-cloud.cn/raw/47aecbabe5db375cd18bd88263ac7939.png)
On the details page, you will see the quota information of the tag, including the resource type, the quota configured, and the number of resources already bound.


#### Modifying tag quotas
1. You can change the quotas configured for a tag on the quota details page.
2. You can also click **Add +** to add quotas for different resource types or in new regions.
3. Click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/5ec6a5f2808ed1ee94e4599315314f3f.png)

### Deleting quotas by resource type[](id:1)
1. Log in to the Tag console and select [Tag Quota](https://console.cloud.tencent.com/tag/quota) on the left sidebar.
2. In the quota list, find the target tag, and click **View** to go to the details page.
3. On the quota details page, find the quota you want to delete, and click **Delete** on the right.
You can also select multiple quotas and click **Delete** above the list to delete multiple quotas at a time.
![](https://qcloudimg.tencent-cloud.cn/raw/437fade80774f9e284473f9d6a5e0b7d.png)

### Removing tags from the quota list
>! If a tag is configured with quotas, you need to [delete the quotas](#1) first before you can remove the tag from the quota list.

1. Log in to the Tag console and select [Tag Quota](https://console.cloud.tencent.com/tag/quota) on the left sidebar.
2. In the quota list, find the tag you want to remove, and click **Delete** on the right.
You can also select multiple tags and click **Delete** above the list to remove multiple tags at a time.
![](https://qcloudimg.tencent-cloud.cn/raw/3d189ba11764512b42386d4bb5841bbd.png)


## Application
Tags, combined with CAM, are a common tool to manage employee permissions. You can create roles for employees, bind them with tags, and configure quotas for the tags so that your employees can create only as many resources as you specify.



