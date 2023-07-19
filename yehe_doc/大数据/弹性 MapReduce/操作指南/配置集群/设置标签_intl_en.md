## Overview
[Tags](https://www.tencentcloud.com/document/product/651/32582) are key-value pairs provided by Tencent Cloud EMR to identify cluster types or node resources.

You can manage clusters or node resources in a categorized manner by using tags in various dimensions such as business, purpose, and responsible person, or use tags to easily identify them. Tag key-value pairs have no semantic meaning for EMR and are parsed and matched strictly based on strings. 

## Limits
A tag is a key-value pair. You can set tags for EMR clusters or node resources to manage them in a categorized manner. Then, you can easily view and identify clusters and node resources under the corresponding tags. You can edit tags in the EMR console.

There are several limits on tags:
- Quantity limit: Each cluster or node can have up to 50 tags. (**Up to five tags can be added at a time**.)
- Tag key limits:
 - You cannot use "qcloud", "tencent", or "project" at the beginning of a tag key because they are reserved by the system.
 - A tag key can contain up to 255 characters. Only digits, letters, and the + = . @ - symbols are supported.
- Tag value limit: A tag value can contain up to 127 characters. Only digits, letters, symbols + = . @ -, and a null string are supported.

## Directions
### Editing cluster tags
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr), select the target cluster on the **Cluster list** page and click **More** > **Edit tag**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/gYyV398_%E5%9B%BD%E9%99%8588.png)
2. Add, modify or delete tags as needed in the pop-up dialog box.
>?You can edit tags for up to 20 clusters at a time.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/npNH254_%E5%9B%BD%E9%99%8589.png)

### Editing node tags
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click a cluster ID/name to go to the cluster details page. Select **Cluster resources** > **Resources**, select the target node, and click **More** > **Edit tag**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/X2e8733_%E5%9B%BD%E9%99%8590.png)
2. Add, modify or delete tags as needed in the pop-up dialog box.
>?You can edit tags for up to 20 clusters at a time.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/xPVb537_%E5%9B%BD%E9%99%8591.png)
