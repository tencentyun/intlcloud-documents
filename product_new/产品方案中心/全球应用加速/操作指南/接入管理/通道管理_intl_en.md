## Adding a connection
1. Log into the [Global Application Accelerate Platform Console](https://console.cloud.tencent.com/gaap). Enter the **Access Management** page and click **Add**.
2. In the pop-up window, enter the acceleration connection information.
 -Projects: The project to which the connection belongs, which can be changed.
 -Connection Name: Length limited to 30 characters.
 -Acceleration Region: The region where the client is located or the one closest to the client.
 -Origin Region: The region where the destination server is located or the one closest to the destination server.
 -Bandwidth Cap: Maximum bandwidth for connection acceleration, which is 1000MB (some connections have a maximum of 100MB).
 -Max concurrent connections: Maximum number of concurrent connections supported by a connection, which is 1 million (some connections have a maximum of 20,000).
![](https://main.qcloudimg.com/raw/d30c08d1cf9dedb12ed805bf731e073f.png)
3. Click **OK** to finish the creation.
4. On “Access Management” page, view the connection list information.
![](https://main.qcloudimg.com/raw/b326c683b47321704d0269a0eb047f2d.png)
 -ID/Name: ID and name of a connection, connection name can be changed.
 -VIP: IP address accessed by the client.
 -Domain Name: Domain name accessed by the client, which is assigned by the system and automatically bound to VIP.
 -Status: Acceleration connection can work normally only under "Normal" status.

## Viewing connection information
1. Log into the [Global Application Accelerate Platform Console](https://console.cloud.tencent.com/gaap). Enter the **Access Management** page. Click the **ID/Connection Name** of the specified connection.
2. On the **Connection Info** tab, you can view connection details. **Forwarding server IP** is the forwarding node IP at the end of the acceleration connection, and this forwarding node forwards the data of the acceleration connection to the origin server via a public network.
![](https://main.qcloudimg.com/raw/0f3097be7c9bb138d4287683a97863d1.png)

## Changing Projects
1. Log into the [Global Application Accelerate Platform Console](https://console.cloud.tencent.com/gaap). Enter the **Access Management** page and select all connections to be changed.
2. Click **Change Project**.
3. Select a destination project in the pop-up window, click **OK** to complete the project change.
>Connections that have been changed may not reside in the current project view. You can switch projects to view them.

## Configuring a connection
 Log into the [Global Application Accelerate Platform Console] (https://console.cloud.tencent.com/gaap) and enter the "Access Management" page. For the specified connection, click [Set] to modify parameters such as project, connection name, bandwidth cap, and maximum concurrent connections.
>In acceleration connection, if the origin server is in the following regions, the connection currently does not support configuration adjustment: Tokyo, Japan; Chennai, India; Sydney, Australia; Sao Paulo, Brazil; Dallas, Central US.; Washington, Eastern US.

## Enabling a connection
1. Log into the [Global Application Accelerate Platform Console](https://console.cloud.tencent.com/gaap). Enter the **Access Management** page and select all connections to be enabled (the connection status is "Disabled").
2. Click **Enable** to enable the specified connections in batch.
3. After the connections are enabled, the client can access them using VIP or domain name for acceleration.
![](https://main.qcloudimg.com/raw/3cc42929cf03bc654c096a8f5d46720a.jpg)

## Disabling a connection
1. Log into the [Global Application Accelerate Platform Console](https://console.cloud.tencent.com/gaap). Enter the **Access Management** page and select all connections to be disabled.
2. Click **Disable** to disable the specified connections in batch.
>A disabled connection will not generate bandwidth fee but will incur a connection fee unless it is deleted.

## Deleting a connection
1. Log into the [Global Application Accelerate Platform Console](https://console.cloud.tencent.com/gaap). Enter the **Access Management** page and select all connections to be deleted.
2. Click **Delete**.
>Deleted connections cannot be used by the client for acceleration.

