## Overview

**Tag** is a key-value pair provided by Tencent Cloud to identify a resource in the cloud. It can help you easily categorize and manage TDMQ for CMQ resources in many dimensions such as business, purpose, and owner.
>?Tencent Cloud will not use the tags you set, and they are only used for your management of TDMQ for CMQ resources.

## Use Limits

You need to pay attention to the following use limits of tags:

| Limit | Description | 
|---------|---------|
| Quantity | One Tencent Cloud resource can have up to 50 tags. |
| Tag key | <li>You cannot place `qcloud`, `tencent`, or `project` at the beginning of a tag key as they are reserved by the system.</li><li>A tag key can contain up to 255 digits, letters, and special symbols (`+=.@-`).</li>|
| Tag value | It can contain up to 127 digits, letters, and special symbols (`+=.@-`) or be an empty string. |

## Directions and Use Cases

### Use case

A company has 6 TDMQ for CMQ queues, with the department, business scope, and owner information as described below:

| Queue ID | Department | Business Scope | Owner |
| ----------------- | -------- | -------- | ------ |
| cmqq-372ovdpw8ob1 | Ecommerce | Marketing | John   |
| cmqq-372ovdpw8ob2 | Ecommerce | Marketing | Harry |
| cmqq-372ovdpw8ob3 | Gaming | Game A | Jane |
| cmqq-372ovdpw8ob4 | Gaming | Game B | Harry |
| cmqq-372ovdpw8ob5 | Entertainment | Post-production | Harry |
| cmqq-372ovdpw8ob6 | Entertainment | Post-production | John |

You can add the following three tags to the `cmqq-372ovdpw8ob1` queue:

<table id="table02">
	<tr><th>Tag Key</th><th>Tag Value</th></tr>
	<tr><td>dept</td><td>ecommerce</td></tr>
	<tr><td>business</td><td>mkt</td></tr>
	<tr><td>owner</td><td>zhangsan</td></tr>
</table>


Similarly, you can also set appropriate tags for other resources based on their department, business scope, and owner information.

### Setting tag in TDMQ for CMQ console

After designing the tag keys and values as detailed above, you can log in to the TDMQ for CMQ console to set tags.

1. Log in to the [TDMQ for CMQ console](https://console.cloud.tencent.com/tdmq/cmq-queue).
2. On the **Queue Service** page, select the target region and queue and click **Edit Resource Tag** at the top of the page.
   ![](https://main.qcloudimg.com/raw/98091abb3b806a2fc0a3656b949c1470.png)
3. Set tags in the **Edit Tag** pop-up window.
   For example, add three tags for the `cmqq-372ovdpw8ob1` queue.
   ![](https://main.qcloudimg.com/raw/11381698a0bbbc24f9f3ec7e4e8701e5.png)
>?If existing tags cannot meet your needs, go to [Tag Management](https://console.cloud.tencent.com/tag/taglist) to create more.
4. Click **OK**, and you will be prompted that the tags have been modified successfully. You can view the tags bound to a queue in its **Resource Tag** column.
 ![](https://main.qcloudimg.com/raw/cd1a0daca2d94503ec9062030e1075e5.png)


### Filtering resource by tag key

You can filter out queues bound to a specific tag in the following steps:

1. Select **Tag** in the search box at the top-right corner of the [Queue Service](https://console.cloud.tencent.com/tdmq/cmq-queue?rid=1) page.
2. In the window that pops up, select the tag you want to search for and click **OK**.
   For example, if you select `Tag: owner:zhangsan`, you can filter out queues bound to the tag key `owner:zhangsan`.
   ![](https://main.qcloudimg.com/raw/75fa474269963006d44710f07e3b8ecf.png)
