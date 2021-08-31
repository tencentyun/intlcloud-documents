## Overview
After binding tags to Tencent Cloud resources, you can use tags to quickly query resources.
This document describes three methods to query resources by tag.

## Prerequisites
You have created a tag and bound resources to it. For detailed instructions, please see [Creating Tags and Binding Resources](https://intl.cloud.tencent.com/document/product/651/41575).

## Directions
>?Click the tabs below to view different querying methods.

<dx-tabs>
::: Via\sag\sConsole\s>\sResource\sTag[](id:resources)
1. Log in to the [Tag console](https://console.cloud.tencent.com/tag).
2. Click **Resource Tag** on the left sidebar.
3. Set the filter criteria as follows.
	- Region (required): You can select all or multiple regions.             
	- Resource type (required): You can select all or multiple resource types from the drop-down list, which includes Tencent Cloud services and resources that support tagging. For details, please see [Tagging-enabled Services](https://intl.cloud.tencent.com/document/product/651/32577).
	- Tag: Select one or multiple tag keys and values. If multiple tag keys and values are selected, the results will be a union of the resources bound to each selected tag.
	- Project: Click **More** to show the project filter criterion and select a project. You can query only services that support project management by this criterion.
4. Click **Query resource**, and the resources will be listed below.
![](https://main.qcloudimg.com/raw/9a7928e597874a861bc1d45d46d8f2ea.png)
:::
::: Via\sTag\sConsole\s>\sTag\sList[](id:list)
1. Log in to the [Tag console](https://console.cloud.tencent.com/tag).
2. Click **Tag List** on the left sidebar.
3. In the tag list, find the target tag, and click the digit in the **Count of Resources** column to view the resources bound to the tag.
![](https://main.qcloudimg.com/raw/922a8ea56894143fa69c671b6b83a380.png)
The resources will be displayed as below:
![](https://main.qcloudimg.com/raw/12c60f41799245ce45a0940221f9a6df.png)
:::
::: Via\sConsole\sof\sTencent\sCloud\sService[](id:product)
You can log in to the console of a Tencent Cloud service that supports tagging and query resources under the service by tag. The directions below use CVM as an example.
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm).
2. On the left sidebar, click **Instances**.
3. Click the search box and select **Tag key**.
4. Type a tag key and value to query the CVM instances bound to the tag.
:::
</dx-tabs>






