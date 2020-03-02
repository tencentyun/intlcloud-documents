## Overview
A [tag](https://intl.cloud.tencent.com/document/product/651/32582) is a key-value pair provided by Tencent Cloud EMR to identify a cluster or node resource.

You can manage clusters or node resources in a categorized manner by using tags in various dimensions such as business, purpose, and person-in-charge, or use tags to easily identify them. Tag key-value pairs have no semantic meaning for EMR and are parsed and matched strictly based on strings.

## Use Limits
A tag is a key-value pair. You can set tags for EMR clusters or node resources to manage them in a categorized manner. Then, you can easily view and identify clusters and node resources under the corresponding tags. Currently, you can edit tags in the EMR Console.

When editing tags, please pay attention to the following use limits:
- Quantity limit: each cluster or node can have up to 50 tags (**up to 5 tags can be added at a time**).
- Tag key limit:
 - You cannot use "qcloud", "tencent", or "project" at the beginning of a tag key as they are reserved by the system.
 - A tag key can contain up to 255 digits, letters, and special characters (+ = . @ -).
- Tag value limit: a tag value can contain up to 127 digits, letters, and special characters (+ = . @ -) or be an empty string.

## Prerequisites

You have logged in to the [EMR Console](https://console.cloud.tencent.com/emr).

## Editing Tags

### Editing cluster tags

1. On the **Cluster List** page, select the cluster for which to edit tags and click **More** > **Edit Tag** at the top as shown below:                                                  
![](https://main.qcloudimg.com/raw/7e41add1edd67201f6527044a8456a77.png)
2. In the "You have selected 1 Tencent Cloud resource" window that pops up, add, modify, or delete tags based on your actual needs.   
![](https://main.qcloudimg.com/raw/90b51e1625136bf34c8eb6df4a8eada5.png)
>You can edit tags in batches for up to 20 clusters at a time.

### Editing node tags

1. On the **Cloud Hardware Management** page, select the node resource for which to edit tags and click **More** > **Edit Tag** at the top as shown below:
![](https://main.qcloudimg.com/raw/2e2b1507f769c977aef797b62d0c5f84.png)
2. In the "You have selected 1 Tencent Cloud resource" window that pops up, add, modify, or delete tags based on your actual needs.   
![](https://main.qcloudimg.com/raw/90b51e1625136bf34c8eb6df4a8eada5.png)
>You can edit tags in batches for up to 20 node resources at a time.
