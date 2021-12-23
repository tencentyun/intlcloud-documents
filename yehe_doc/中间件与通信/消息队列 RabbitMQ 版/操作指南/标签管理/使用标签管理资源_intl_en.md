## Overview

**Tag** is a key-value pair provided by Tencent Cloud to identify a resource in the cloud. It can help you easily categorize and manage TDMQ for RabbitMQ resources in many dimensions such as business, purpose, and owner.
>?Tencent Cloud will not use the tags you set, and they are only used for your management of TDMQ for RabbitMQ resources.

## Use Limits

You need to pay attention to the following use limits of tags:

| Limit | Description | 
|---------|---------|
| Quantity | One Tencent Cloud resource can have up to 50 tags. |
| Tag key | <li>You cannot place `qcloud`, `tencent`, or `project` at the beginning of a tag key as they are reserved by the system.</li><li>A tag key can contain up to 255 digits, letters, and special symbols (`+=.@-`).</li>|
| Tag value | It can contain up to 127 digits, letters, and special symbols (`+=.@-`) or be an empty string. |


## Directions and Use Cases

### Use case

A company has 6 TDMQ for RabbitMQ clusters, with the department, business scope, and owner information as described below:

| Cluster ID | Department | Business Scope | Owner |
| ----------------- | -------- | -------- | ------ |
| amqp-78383dp8p8w1 | Ecommerce | Marketing | John   |
| amqp-78383dp8p8w2 | Ecommerce | Marketing | Harry |
| amqp-78383dp8p8w3 | Gaming | Game A | Jane |
| amqp-78383dp8p8w4 | Gaming | Game B | Harry |
| amqp-78383dp8p8w5 | Entertainment | Post-production | Harry |
| amqp-78383dp8p8w6 | Entertainment | Post-production | John |

You can add the following three tags to the `amqp-78383dp8p8w1` cluster:

<table id="table02">
	<tr><th>Tag Key</th><th>Tag Value</th></tr>
	<tr><td>dept</td><td>ecommerce</td></tr>
	<tr><td>business</td><td>mkt</td></tr>
	<tr><td>owner</td><td>zhangsan</td></tr>
</table>


Similarly, you can also set appropriate tags for other resources based on their department, business scope, and owner information.

### Setting tag in TDMQ for RabbitMQ console

After designing the tag keys and values as detailed above, you can log in to the TDMQ for RabbitMQ console to set tags.

1. Log in to the [TDMQ for RabbitMQ console](https://console.cloud.tencent.com/tdmq/rabbit-cluster).
2. On the **Cluster Management** page, select the target region and cluster and click **Edit Resource Tag** at the top of the page.
  ![](https://qcloudimg.tencent-cloud.cn/raw/89d60a0c12688b43ed62e7843417147a.png)
3. Set tags in the **Edit Tag** pop-up window.
   For example, add three tags for the `amqp-78383dp8p8w1` cluster.
   ![](https://qcloudimg.tencent-cloud.cn/raw/ebd1df5b15e58c5583f8a126747b83b8.png)
>?If existing tags cannot meet your needs, go to [Tag Management](https://console.cloud.tencent.com/tag/taglist) to create more.
4. Click **OK**, and you will be prompted that the tags have been modified successfully. You can view the tags bound to a cluster in its **Resource Tag** column.
   ![](https://qcloudimg.tencent-cloud.cn/raw/c94c4873523953c096ff3e9510821274.png)


### Filtering resource by tag key

You can filter out clusters bound to a specific tag in the following steps:

1. Select **Tag** in the search box at the top-right corner of the page.
2. In the window that pops up, select the tag you want to search for and click **OK**.
   For example, if you select `Tag: owner:zhangsan`, you can filter out clusters bound to the tag key `owner:zhangsan`.
   ![](https://qcloudimg.tencent-cloud.cn/raw/657c8d07f097f0a9730d70e5e986f80c.png)
