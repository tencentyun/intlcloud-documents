## Feature Overview
[Tags](https://intl.cloud.tencent.com/document/product/651/32582) are key-value pairs provided by Tencent Cloud EMR to identify cluster types or node resources.

You can manage clusters or node resources in a categorized manner by using tags in various dimensions such as business, purpose, and responsible person, or use tags to easily identify them. Tag key-value pairs have no semantic meaning for EMR and are parsed and matched strictly based on strings.

## Use Limits
A tag is a key-value pair. You can set tags for EMR clusters or node resources to manage them in a categorized manner. Then, you can easily view and identify clusters and node resources under the corresponding tags. You can edit tags in the EMR console.

There are several limits on editing tags:
- Quantity limit: each cluster or node can have up to 50 tags. (**Up to five tags can be added at a time**.)
- Tag key limits:
 - You cannot use "qcloud", "tencent", or "project" at the beginning of a tag key because they are reserved by the system.
 - A tag key can contain up to 255 characters. Only numbers, letters, and the + = . @ - symbols are allowed.
- Tag value limit: a tag value can contain up to 127 characters. Only numbers, letters, the + = . @ - symbols, and an empty string are allowed.

## Directions
### Editing cluster tags
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr), select a cluster to edit tags on the **Cluster List** page and click **More** > **Edit Tag** as shown below:
![](https://main.qcloudimg.com/raw/7e41add1edd67201f6527044a8456a77.png)
2. Add, modify or delete tags as needed in the pop-up dialog box.
>?You can edit tags for up to 20 clusters at a time.
>
![](https://main.qcloudimg.com/raw/90b51e1625136bf34c8eb6df4a8eada5.png)

### Editing node tags
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click a cluster ID/name to go to the cluster details page. Select **Cluster Resource** > **Resource Management**, select the node resource for which to edit tags, and click **More** > **Edit Tag** as shown below:
![](https://main.qcloudimg.com/raw/2e2b1507f769c977aef797b62d0c5f84.png)
2. Add, modify or delete tags as needed in the pop-up dialog box.
>?You can edit tags for up to 20 clusters at a time.
>
![](https://main.qcloudimg.com/raw/90b51e1625136bf34c8eb6df4a8eada5.png)
