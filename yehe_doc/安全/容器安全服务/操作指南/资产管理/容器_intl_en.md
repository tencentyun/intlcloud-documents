This document describes the container module feature and how to view the details of containers, images, and servers.
![](https://qcloudimg.tencent-cloud.cn/raw/fc1c92336f912f2e561e5be0bac01309.png)

## Viewing the Container Module
The container module displays the total number of containers and the numbers of running, suspended, and aborted containers.
### Filtering containers
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Asset Management** on the left sidebar.
2. On the **Asset Management** page, click **Containers** to enter the container list page.
![](https://qcloudimg.tencent-cloud.cn/raw/35434bace3aea3077242fbcdc17fc441.png)
3. On the container list page, filter containers by status or click the search box and search for containers by keyword such as container name/ID, image name, or server IP.
 - Click the status drop-down list in the top-left corner to filter containers by status.
 <img src="https://qcloudimg.tencent-cloud.cn/raw/039b82d88e66b63a8da93a29d37146e1.png" style="zoom:80%;" />
 - Click the search box and search for containers by keyword such as container name, container ID, image name, or server IP.
 <img src="https://qcloudimg.tencent-cloud.cn/raw/4f353d726656b5cee7d5bf26c4fee351.png" style="zoom:80%;" />

### Viewing the list of containers
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Asset Management** on the left sidebar.
2. On the **Asset Management** page, click **Containers** to enter the container list page.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e4c69b63a584601969c6b0ca273a7083.png" style="zoom:80%;" />
3. On the container list page, click a **Container name** to pop up the drawer on the right, which displays the container details, including the basic container information, process information, and port information.
![](https://qcloudimg.tencent-cloud.cn/raw/cf8bb0e835c41ff857d9edb203d2892f.png)
![](https://qcloudimg.tencent-cloud.cn/raw/418576b0a585e60754dd34a456020d5c.png)
4. On the **Asset Management** page, click a **Server IP** to pop up the drawer on the right, which displays the server details, including the basic server information, Docker information, and the numbers of images and containers.
>?In the drawer, click the number to view the numbers of images and containers on the server.
><img src="https://qcloudimg.tencent-cloud.cn/raw/519c19224986ac12f7c489345aa9beea.png" style="zoom: 67%;" />

 ![](https://qcloudimg.tencent-cloud.cn/raw/8138493ec02e7e7500ab18fb567cd111.png)

### Custom list management
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Asset Management** on the left sidebar.
2. On the **Asset Management** page, click **Containers** to enter the container list page.
<img src="https://qcloudimg.tencent-cloud.cn/raw/2901f75ddc60d38092fdd6173e52c260.png" style="zoom:80%;" />
3. On the container list page, click ![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png) to pop up the **Custom List Management** window.
3. In the pop-up window, select the target type and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/cd74bdaea9642a37ab2add6a9c4a4321.png" style="zoom:80%;" />

#### Key fields in the list
1. Status: **Running**, **Suspended**, or **Aborted**.
2. Image: Name of the associated image.
3. Pod: Pod of the container.
4. CPU | Utilization: CPU utilization.
5. MEMUsage: Memory utilization.

## Viewing the Local Image Module
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Asset Management** on the left sidebar.
2. On the **Asset Management** page, the image module displays the total number of images. Click **Images** to enter **Image Security** > **Local Images** and view the details.
>? For more information, see [Local Image](https://www.tencentcloud.com/document/product/1163/50891).

<img src="https://qcloudimg.tencent-cloud.cn/raw/953a6225bb4b7b5d8066f413c4bdf72a.png" style="zoom:80%;" />

## Viewing the Image Repository Module
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Asset Management** on the left sidebar.
2. On the **Asset Management** page, the image repository module displays the total number of image repositories. Click **Image repositories** to enter **Image Security** > **Image repository** and view the details.
>? For more information, see [Image Repository](https://www.tencentcloud.com/document/product/1163/50892).

<img src="https://qcloudimg.tencent-cloud.cn/raw/15c55d5eb0aaf126e5dfbaab952ccd38.png" style="zoom:80%;" />

## Viewing the Server Module
The server module displays the total number of servers and the numbers of running and offline servers.
### Filtering servers
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Asset Management** on the left sidebar.
2. On the **Asset Management** page, click **Servers** to view the list of all servers.
<img src="https://qcloudimg.tencent-cloud.cn/raw/163265ba97903e592511c9d568d6bcf9.png" style="zoom:80%;" />
3. On the server list page, filter servers by running status or click the search box and search for servers by keyword such as server name, project, Docker version, or server IP.
 - Click the status drop-down list in the top-left corner to filter servers by status.
 <img src="https://qcloudimg.tencent-cloud.cn/raw/6ddfbcd4abdde2829585dac2e7d74507.png" style="zoom:67%;" />
 - Click the search box and search for servers by keyword such as server name, project, Docker version	, or server IP.
 <img src="https://qcloudimg.tencent-cloud.cn/raw/88038c9a34722c3ca47e27fe63490f43.png" style="zoom:67%;" />

### Viewing the list of containers
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Asset Management** on the left sidebar.
2. On the **Asset Management** page, click **Servers** to view the list of all servers.
<img src="https://qcloudimg.tencent-cloud.cn/raw/dece04e5e03c2ae6b9532228e549e816.png" style="zoom:80%;" />
3. On the server list page, click a **Server IP** to pop up the drawer on the right, which displays the server details, including the basic server information, Docker information, and the numbers of images and containers.
>? In the drawer, click the number to view the numbers of images and containers on the server.
><img src="https://qcloudimg.tencent-cloud.cn/raw/ae1a64866593098c7be0495c9b50effe.png" style="zoom: 67%;" />

![](https://qcloudimg.tencent-cloud.cn/raw/7a16e7d58dce8b19464e26ae8578b55c.png)
4. On the server list page, click **Images** to view the details of associated images.
![](https://qcloudimg.tencent-cloud.cn/raw/9c0faed8d6da42e60c5fca5980b25c50.png)
5. On the server list page, click **Containers** to view the details of associated containers.
![](https://qcloudimg.tencent-cloud.cn/raw/45b2e82d9c3cd4bc23ab6eabd867326d.png)

### Custom list management
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Asset Management** on the left sidebar.
2. On the **Asset Management** page, click **Servers** to view the list of all servers.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f0822d61df17196ecdb629b1fce2b246.png" style="zoom:80%;" />
3. On the server list page, click ![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png) to pop up the **Custom List Management** window.
4. In the pop-up window, select the target type and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/abe1abeea2988ac787bbf5660aeb5656.png" style="zoom:67%;" />

#### Fields in the list
1. Server name: Server name.
2. Server IP: Click a **Server IP** to pop up the drawer on the right, which displays the server details, including the basic server information, Docker information, and the numbers of images and containers.
3. Project: Project name of the server.
4. Docker version: Docker version number. If no Docker version is installed, "Not installed" will be displayed.
5. Docker file system type: Type of the Docker file system.
6. Images: Number of images associated with the server. Click the number to view the details.
7. Containers: Number of containers associated with the server. Click the number to view the details.
