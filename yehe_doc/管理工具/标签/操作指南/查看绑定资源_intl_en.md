## Overview
After binding tags to Tencent Cloud resources, you can use tags to quickly query resources.

This document describes three methods to query resources by tag.

## Prerequisites
You have created a tag and bound it to a resource. For detailed instructions, please see [Creating Tags](https://intl.cloud.tencent.com/document/product/651/41684) and [Tagging Resources](https://intl.cloud.tencent.com/document/product/651/41685).

## Directions
>?Click the tabs below to view different querying methods.

<dx-tabs>
::: Tag Console > Tag List
1. Log in to the [Tag console](https://console.cloud.tencent.com/tag).
2. Click **Tag List** on the left sidebar.
3. In the tag list, find the target tag and click the digit in the **Count of Resources** column to view the tagged resources.
![](https://main.qcloudimg.com/raw/366552d20e7a7c5c1c721152843b9d9f.png)
The resources will be displayed as below:
![](https://main.qcloudimg.com/raw/c4fd0d759c45db2705d40b6555f6f3b7.png)
:::
::: Tag Console > Resource Tag
1. Log in to the [Tag console](https://console.cloud.tencent.com/tag).
2. Click **Resource Tag** on the left sidebar.
3. Set the filter criteria as follows.
	- Region: Choose the region of the resources to query.             
	- Resource Type: Choose the type of the resources to query. You can query only the resources of [tagging-enabled services](https://intl.cloud.tencent.com/document/product/651/32577).
	- Tag: Select the tag key-value pair whose resources you want to query. This field can be left empty. You can also query the resources of multiple tags by clicking **Add** to select multiple key-value pairs.
	- Project: Click **More** to show the project filter criterion and select a project. This criterion is available for only services that support project management.
4. Click **Query resource**, and the resources will be listed as below.
![](https://main.qcloudimg.com/raw/bb15cb86716d7861f39affc638068081.png)
:::
::: Console of Tencent Cloud Service
You can log in to the console of a Tencent Cloud service that supports tagging and query resources under the service by tag.
<dx-alert infotype="explain" title="">
The directions below use CVM as an example.
</dx-alert>
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm).
2. On the left sidebar, click **Instances**.
3. Click the search box and select **Tag key**.
![](https://main.qcloudimg.com/raw/f8c645ff03f2e85485ed1c361288f158.png)
4. Type a tag key and value to query the CVM instances bound to the tag.
:::
</dx-tabs>












