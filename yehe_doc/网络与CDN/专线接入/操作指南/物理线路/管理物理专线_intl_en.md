After the connection is running, you can view or delete the connection, modify its bandwidth, add tags, or perform other operations in the console.

## Viewing the Connection
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc) and click **Connections** on the left sidebar.
2. In the list, click the **ID/Name** of the connection that you want to view.
3. The **Basic info** tab displays the connection details, including connection provider, port type, access point, bandwidth, and other information.

## Modifying the Connection Bandwidth[](id:xgzxdk)
You can change the connection bandwidth in the console to meet your business requirements.
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc) and click **Connections** on the left sidebar.
2. Locate the target connection, and click <img src="https://main.qcloudimg.com/raw/134ed671d2fa3ec1b82525985c0a6633.svg" style="zoom:6%;" /> under the **Bandwidth** column.
3. Specify a new bandwidth value in the edit box and click **OK**.
 > ?
> - If no dedicated tunnel is created, the connection bandwidth should be no less than 1 Mbps, and cannot exceed the port bandwidth.
> - If there are dedicated tunnels created, the connection bandwidth should be no less than the total bandwidth caps of all tunnels, and cannot exceed the port bandwidth.
> - The maximum port bandwidth varies with port types as follows:
>   - 1 Gbps electronic port: 1,000 Mbps
>   - 1 Gbps fiber optic port: 1,000 Mbps
>   - 10 Gbps fiber optic port: 10,000 Mbps
>   - 100 Gbps fiber optic port: 100,000 Mbps

## Adding Tags
To easily locate and manage the connections under your account, perform the following steps to add tags to your connections.
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc) and click **Connections** on the left sidebar.
2. Select the connection to which a tag is added, and click **Edit Tags** in the **Operation** column.
3. Select a tag key and tag value in the corresponding drop-down list. You can also click **Manage Tags** to create a tag.
4. Use a tag to locate the connection.
 1. Click the edit box in the upper-right corner of the **Connections** page, and select **Tag** in the drop-down list.
 2. Enter the tag in the edit box and click the magnifying glass icon.
5. Use a tag to manage the connections.
 1. Click ![](https://main.qcloudimg.com/raw/f22b6d803bb59529e530d140ee669a1c.png) in the upper-right corner of the **Connections** page.
 2. In the pop-up window, select the target tags, and click **OK**.
Then the tag keys will appear in the connection list.

## Deleting a Connection
You can delete a connection when you no longer need it.
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc) and click **Connections** on the left sidebar.
2. Select the connection to delete, and click **Delete** in the **Operation** column.
3. In the pop-up window, check **Confirm Deletion** and click **Confirm**.
>?The port monthly rental fees will no longer incur.
