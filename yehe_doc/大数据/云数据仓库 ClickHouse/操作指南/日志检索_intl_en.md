## Configuring Cluster Log Service
### Cluster logging configuration
You can collect ClickHouse node logs under your account to Cloud Log Service (CLS) as well as enable and use the log search feature as needed.
>?CLS is postpaid, so make sure that your account balance is sufficient to ensure normal ClickHouse log upload and display. For more information on CLS fees, see [Billing Overview](https://intl.cloud.tencent.com/document/product/614/37509). When CLS is enabled, the authorized permissions will take effect simultaneously.

### Enabling cluster logging
- Enable CLS for a new cluster 
You can configure CLS when creating a cluster. Select an existing CLS logset or create one in the same region as the cluster. Logs are stored for 30 days by default.
![](https://qcloudimg.tencent-cloud.cn/raw/521f9e0caecbaf9f98eba7594f3409f4.png)
>?A log topic will be created in your configured logset to store ClickHouse logs. You can view the topic on the CLS page. Do not delete this topic configured for the ClickHouse cluster; otherwise, log queries will fail on the ClickHouse log search page.
>
- Enable or modify CLS for an existing cluster
If CLS is not enabled for a ClickHouse cluster during cluster creation, you can enable it by selecting **Operation > More > Create Log Service** in the cluster list. Note that you need to be authorized first before configuring a logset.
 ![](https://qcloudimg.tencent-cloud.cn/raw/3727abbf1528b8a69c3d7a6aac472a33.png)

## Using Log Search
1. Log in to the [Cloud Data Warehouse console](https://console.cloud.tencent.com/cdwch), click a **Cluster ID/Name** in the **Cluster List** to enter the cluster details page, and switch to the **Log Search** tab.
2. The **Page Mode** can be **Node log** or **Search**. The **Log Type** can be **Running log** or **Error log**. You can view logs of each node as needed.
 ![](https://qcloudimg.tencent-cloud.cn/raw/7ed0845d6e901cd98bf17465d4744d6c.png)
3. You can query logs by keyword. The results are grouped by node IP. The last 100 logs are displayed for each node by default.
![](https://qcloudimg.tencent-cloud.cn/raw/b23f4d81b49bbed77b0bcb7d98a567b7.png)
