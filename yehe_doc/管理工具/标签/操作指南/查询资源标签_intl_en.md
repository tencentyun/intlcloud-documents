## Overview
After binding tags to Tencent Cloud resources, you can use tags to quickly query resources.


## Prerequisites
You have created a tag and bound it to a resource. For detailed instructions, please see [Creating Tags](https://intl.cloud.tencent.com/document/product/651/41684) and [Tagging Resources](https://intl.cloud.tencent.com/document/product/651/41685).

## Directions


1. Log in to the [Tag console](https://console.cloud.tencent.com/tag).
2. Click **Resource Tag** on the left sidebar.
3. Set the filter criteria as follows.
	- Region (required): You can select all or multiple regions.             
	- Resource type (required): You can select all or multiple resource types from the drop-down list, which includes Tencent Cloud services and resources that support tagging. For details, please see [Tagging-enabled Services](https://intl.cloud.tencent.com/document/product/651/32577).
	- Tag: Select one or multiple tag keys and values. If multiple key-value pairs are selected, the results will be a union of the resources each selected tag is bound to.
	- Project: Click **More** to show the project filter criterion and select a project. This criterion is available for only services that support project management.
4. Click **Query resource**, and the resources will be listed as below.
![](https://main.qcloudimg.com/raw/bb15cb86716d7861f39affc638068081.png)
