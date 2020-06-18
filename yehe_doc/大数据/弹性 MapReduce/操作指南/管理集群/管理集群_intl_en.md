## Managing the Cluster List
After successfully creating a cluster, log in to the [EMR Console](https://console.cloud.tencent.com/emr) and enter the cluster list page to manage its information.
![](https://main.qcloudimg.com/raw/e3cca432c58af3fb39ffdb0d712f8c30.png)
- Select the "Region" drop-down list to browse clusters by region.
- Select an EMR cluster instance, select **More** > **Edit Tags**, and click the icon in the top-right corner to customize a column so as to add a column of set tags.
- Click **Copy** on the right of an instance ID/name to copy the instance ID. Click the ID to view the cluster details.
- Click **Modify** on the right of an instance ID/name to rename the cluster.
- In the **Management** column of the instance list, click **Details** to view the details of an instance.
- In the **Management** column of the instance list, click the **More** drop-down list to select to restart a component, terminate a cluster, or export software configuration.


## Viewing Cluster Details
Click **Details** in the **Management** column of the instance list or click a cluster ID to enter the cluster details page.

You can view the server configuration, software configuration information, and node information of the cluster.
- The server configuration information section displays basic information of the cluster, such as network information, creation time, security group, and high-availability enablement status.
- The software configuration information section displays the software tools installed in the cluster and their version numbers, COS activation status, and Kerberos mode enablement status.
- The node information section displays the quantity of nodes in each type.
![](https://main.qcloudimg.com/raw/24c490d4cac246e375f1ace040fbc586.png)

If COS has not been activated for a cluster, and you want to activate it now for business needs, you can click **Set** and enter the correct authentication address, `SecretID`, and `SecretKey` as required.
>To ensure that COS can be properly activated and take effect after authentication, please make sure that the access domain names corresponding to the `SecretID` and `SecretKey` are the same.

![](https://main.qcloudimg.com/raw/492572698433980dd891d2a2e01a3c3d.png)
For detailed directions, please see [Manually Activating COS in Console](https://intl.cloud.tencent.com/document/product/1026/34570).
