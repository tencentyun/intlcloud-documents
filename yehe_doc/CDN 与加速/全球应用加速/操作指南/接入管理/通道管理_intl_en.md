## Adding a Connection
1. Log in to the [Global Application Acceleration Platform console](https://console.cloud.tencent.com/gaap), enter the **Access Management** page and click **Add**.
2. In the pop-up window, enter the acceleration connection information.
 - Project: the project to which the connection belongs, which can be changed.
 - Connection name: it can contain up to 30 characters.
 - Acceleration region: the region where the client is located or the one closest to the client.
 - Origin region: the region where the destination server is located or the one closest to the destination server.
 - Bandwidth cap: maximum bandwidth for connection acceleration, which is 1000 Mbps (some connections have a maximum of 100 Mbps).
 - Maximum concurrent connections: maximum number of concurrent connections supported by a connection, which is 1 million (some connections have a maximum of 20,000).
![](https://main.qcloudimg.com/raw/d30c08d1cf9dedb12ed805bf731e073f.png)
3. Click **OK**.
4. On the **Access Management** page, view the connection list information.
![](https://main.qcloudimg.com/raw/b326c683b47321704d0269a0eb047f2d.png)
 - ID/connection name: ID and name of a connection. The connection name can be changed.
 - VIP: IP address accessed by the client.
 - Domain name: domain name accessed by the client, which is assigned by the system and automatically bound to the VIP.
 - Status: only the acceleration connections in the **Running** status can work normally.

## Viewing Connection Information
1. Log in to the [Global Application Acceleration Platform console](https://console.cloud.tencent.com/gaap), enter the **Access Management** page and click **ID/Connection Name** of a connection.
2. On the **Connection Info** tab, you can view connection details. **Forwarding Server IP** is the forwarding node IP at the end of the acceleration connection, and this forwarding node forwards the data of the acceleration connection to the origin server via a public network.
![](https://main.qcloudimg.com/raw/0f3097be7c9bb138d4287683a97863d1.png)

## Changing Projects
1. Log in to the [Global Application Acceleration Platform console](https://console.cloud.tencent.com/gaap), enter the **Access Management** page and select all connections to be changed.
2. Click **Change Project**.
3. Select a target project in the pop-up window and then click **OK**.
>!Connections that have been changed may not be displayed in the current project view. You can switch projects to view them.

## Setting a Connection
 Log in to the [Global Application Acceleration Platform console](https://console.cloud.tencent.com/gaap), enter the **Access Management** page. Click **Modify configuration** on the right of the target connection to modify its bandwidth cap and maximum concurrent connections.
>!If the acceleration region of an acceleration connection is a partner IDC, the bandwidth of the connection will be set to 1000 Mbps by default.

## Enabling a Connection
1. Log in to the [Global Application Acceleration Platform console](https://console.cloud.tencent.com/gaap), enter the **Access Management** page, and select all connections to be enabled (the connection status is **Disabled**).
2. Click **Enable** to enable the specified connections in batches.
3. After the connections are enabled, the client can access them using the VIP or domain name for acceleration.
![](https://main.qcloudimg.com/raw/3cc42929cf03bc654c096a8f5d46720a.jpg)

## Disabling a Connection
1. Log in to the [Global Application Acceleration Platform console](https://console.cloud.tencent.com/gaap), enter the **Access Management** page, and select all connections to be disabled.
2. Click **Disable** to disable the specified connections in batches.
>!A disabled connection will not generate a bandwidth fee but will incur a connection fee unless it is deleted.

## Deleting a Connection
1. Log in to the [Global Application Acceleration Platform console](https://console.cloud.tencent.com/gaap), enter the **Access Management** page, and select all connections to be deleted.
2. Click **Delete**.
>!Deleted connections cannot be used by the client for acceleration.

