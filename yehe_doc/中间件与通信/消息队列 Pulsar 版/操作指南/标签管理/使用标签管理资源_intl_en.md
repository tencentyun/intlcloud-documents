## Overview

**Tag** is a key-value pair provided by Tencent Cloud to identify a resource in the cloud. It can help you easily categorize and manage TDMQ for Pulsar resources in many dimensions such as business, purpose, and owner.
>?Tencent Cloud will not use the tags you set, and they will only be used for your management of TDMQ for Pulsar resources.

## Use Limits

You need to pay attention to the following use limits of tags:

| Limit | Description | 
|---------|---------|
| Quantity | One Tencent Cloud resource can have up to 50 tags. |
| Tag key | <li>You cannot place `qcloud`, `tencent`, or `project` at the beginning of a tag key as they are reserved by the system.</li><li>A tag key can contain up to 255 digits, letters, and special symbols (`+=.@-`).</li>|
| Tag value | It can contain up to 127 digits, letters, and special symbols (`+=.@-`) or be an empty string. |

## Directions and Use Cases

### Use case

A company has 6 TDMQ for Pulsar clusters, with the department, business scope, and owner information as described below:

| Cluster ID             | Department | Business Scope | Owner |
| ------------------- | -------- | -------- | ------ |
| pulsar-rgxj35jgo3d1 | Ecommerce     | Marketing | John   |
| pulsar-rgxj35jgo3d2 | Ecommerce     | Marketing | Harry   |
| pulsar-rgxj35jgo3d3 | Gaming     | Game A   | Jane   |
| pulsar-rgxj35jgo3d4 | Gaming    | Game B   | Harry   |
| pulsar-rgxj35jgo3d5 | Entertainment     | Post-production | Harry   |
| pulsar-rgxj35jgo3d6 | Entertainment     | Post-production | John   |

You can add the following three tags to the `pulsar-rgxj35jgo3d1` cluster:

<table id="table02">
	<tr><th>Tag Key</th><th>Tag Value</th></tr>
	<tr><td>dept</td><td>ecommerce</td></tr>
	<tr><td>business</td><td>mkt</td></tr>
	<tr><td>owner</td><td>zhangsan</td></tr>
</table>


Similarly, you can also set appropriate tags for other resources based on their department, business scope, and owner information.

### Setting tag in TDMQ for Pulsar console

After designing the tag keys and values as detailed above, you can log in to the TDMQ for Pulsar console to set tags.

1. Log in to the [TDMQ for Pulsar console](https://console.cloud.tencent.com/tdmq/cluster).
2. On the **Cluster Management** page, select the target region and cluster and click **Edit Resource Tag** at the top of the page.
   ![](https://main.qcloudimg.com/raw/be5261338d0b21c0e20a3bdb5bf80e31.png)
3. Set tags in the **Edit Tag** pop-up window.
   For example, add three tags for the `pulsar-rgxj35jgo3d1` cluster.
   ![](https://main.qcloudimg.com/raw/11381698a0bbbc24f9f3ec7e4e8701e5.png)
>?If existing tags cannot meet your needs, go to [Tag Management](https://console.cloud.tencent.com/tag/taglist) to create more.
>
4. Click **OK**, and you will be prompted that the tags have been modified successfully. You can view the tags bound to a cluster in its **Resource Tag** column.
   ![](https://main.qcloudimg.com/raw/b832eade18b1f1cefd62b434e4411630.png)


### Filtering resource by tag key

You can filter out clusters bound to a specific tag in the following steps:

1. Select **Tag** in the search box at the top-right corner of the page.
2. In the window that pops up, select the tag you want to search for and click **OK**.
   For example, if you select `Tag: owner:zhangsan`, you can filter out clusters bound to the tag key `owner:zhangsan`.
   ![](https://main.qcloudimg.com/raw/9fe795ffd667918d721e0da75369d126.png)
