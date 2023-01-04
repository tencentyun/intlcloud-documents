This document describes the local image feature and how to enable data scan and view the local image list.
![](https://qcloudimg.tencent-cloud.cn/raw/04040b472bd32cac3804987963f276fb.png)

## Enabling Data Scan
The data scan module displays the number of images at risk, total number of images, and the numbers of vulnerabilities, viruses, trojans, and sensitive data pieces in the images after the last scan.
### Enabling quick scan
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Image Risk Control** > **Local Images** on the left sidebar.
2. On the **Local Images** page, click **Scan now** on the right to scan again and get the latest image data or risk information.
![](https://qcloudimg.tencent-cloud.cn/raw/6493d408dba3a3d417b161fd155eae5d.png)
3. On the **Scanning settings** page, select the **Risk category** and **Images** as needed.
 - Risk category: **Vulnerabilities** or **Sensitive data**.
 - Images: **All images** or **Specified images**. Click ![](https://main.qcloudimg.com/raw/37d813d17a69271ce31b3233ad0a949e.png) or ![](https://main.qcloudimg.com/raw/be9e47bccb644d8a099149bac4aef1e0.png) to select or delete the target specified image.
>? You can press Shift to select multiple ones.

 ![](https://qcloudimg.tencent-cloud.cn/raw/8b1e0e71b1a89bb839dcea89d2de503f.png)
4. After selecting the target content, click **Scan now**.
>! After the scan starts, all images with the same ID as the selected image will be scanned at the same time.

 ### Enabling scheduled scan
 1. On the **Local Images** page, click **Scheduled scan settings** on the right to specify whether to enable the scheduled scan feature.
 ![](https://qcloudimg.tencent-cloud.cn/raw/a3e22341834abfc29f81901831d7ab55.png)
 2. On the **Scheduled scan settings** page, toggle on the **On/Off** switch and set the **Frequency**, **Risk category**, and **Images** as needed.
  - Frequency: It can be every day, every 7 days, every 15 days, every 30 days, or a specified time range.
  - Risk category: Click ![](https://main.qcloudimg.com/raw/86d08a45be3bc5b91de551b390ebe15d.png) to select **Vulnerabilities**, **Sensitive data**, or **Virus & Trojan** as needed.
  - Images: **All images** or **Specified images**. Click ![](https://main.qcloudimg.com/raw/37d813d17a69271ce31b3233ad0a949e.png) or ![](https://main.qcloudimg.com/raw/be9e47bccb644d8a099149bac4aef1e0.png) to select or delete the target specified image.
>? You can press Shift to select multiple ones.

 ![](https://qcloudimg.tencent-cloud.cn/raw/2e64ea860827ca932d61f043467c328c.png)
 3. After selecting the target content, click **Set** or **Cancel**.

### Enabling data update
On the **Local Images** page, click **Data update** > **OK** on the right to immediately update the security information of all images.
>? It takes up to one to three minutes.

![](https://qcloudimg.tencent-cloud.cn/raw/7218397cafe4e2ce2de5812c099482d6.png)

## Viewing the List of Local Images
### Image licensing event
1. On the **Local Images** page, click **License**.
![](https://qcloudimg.tencent-cloud.cn/raw/56c392934a8a6aed42286865084d65b1.png)
2. In the pop-up window, click **OK**.
>? A license will be assigned to this image.

### Filtering images
On the **Local Images** page, filter images as follows:
 - Click the scanning status drop-down list to filter images by scanning status.
<img src="https://qcloudimg.tencent-cloud.cn/raw/9cf2975a897af7da245120bf98d59f57.png" style="zoom:67%;" />
 - Click the security status drop-down list to filter images by security status.
<img src="https://qcloudimg.tencent-cloud.cn/raw/d18a6990a7ffa21fc5c1d6aeae87a158.png" style="zoom:67%;" />
 - Click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select **Show only high-priority images** and display the high-priority images based on the risk urgency.
![](https://qcloudimg.tencent-cloud.cn/raw/b398ed69b86c9c2c337947da77ac3e4f.png)
 - Click the search box and search for images by keyword such as image name or image ID.
![](https://qcloudimg.tencent-cloud.cn/raw/446265bb02db80b801696d810e3d2874.png)

### Exporting an image
On the **Local Images** page, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target local image and click ![](https://main.qcloudimg.com/raw/24d375a75e4ee95c77910d101f7203dd.png) to export it.
![](https://qcloudimg.tencent-cloud.cn/raw/5cbf99421e5cd7910456416516d97b99.png)

### Viewing the list details
1. On the **Local Images** page, click **Image name** to pop up the drawer on the right, which displays the image details.[](id:JXMC)
>?
>- Image risk: It indicates whether the image scan is successful and the numbers of vulnerabilities, viruses, trojans, and sensitive data pieces.
>- Image details: It includes the image name, image ID, image size, and operating system type.
>- Vulnerability list: You can filter image security vulnerability events by vulnerability severity or search for them by vulnerability name. Click **View details** to view the vulnerability details and fix suggestion.
>- Virus and trojan list: You can filter image security events by virus or trojan severity or search for them by filename. Click **View details** to view the virus or trojan details and suggestion.
>- Sensitive data list: You can filter security events by sensitive data severity, name, or type.
>- Image build history: It logs the image build history.

![](https://qcloudimg.tencent-cloud.cn/raw/a3cfc005c2e9c95b365fa8ea5fb13fc8.png)
2. On the **Local Images** page, click **Associated servers** to pop up the details window, which displays the server name, server IP, and Docker version.
>? If multiple servers are associated, you can filter them as follows:
>- Click the server status drop-down list to filter servers by status.
>- Click the search box and search for servers by keyword such as server name, project, or Docker version.

![](https://qcloudimg.tencent-cloud.cn/raw/80294cdb1d33808c653ce78d6a3f2d29.png)
3. On the **Local Images** page, click **Associated containers** to pop up the details window, which displays the container name, container ID, container running status, CMD, and last update time.
>? If multiple containers are associated, you can filter them as follows:
>- Click the status drop-down list to filter containers by status.
>- Enter the server name and click ![](https://main.qcloudimg.com/raw/b12f0b480adcd420cdd30445ba435c04.png) for search.

![](https://qcloudimg.tencent-cloud.cn/raw/7994ee84829353ad8968b22804267f4e.png)
4. On the **Local Images** page, click **Details** to display the drawer on the right, which displays the [image name](#JXMC).
![](https://qcloudimg.tencent-cloud.cn/raw/f4b914eba2fdb66fab30d7d69fcb9a4a.png)

### Image scanning
1. On the **Local Images** page, click **Scan now** > **OK** to scan an image in "Not scanned" status.
![](https://qcloudimg.tencent-cloud.cn/raw/8298745c11b7dbb5f8fb018e56d5153b.png)
2. On the **Local Images** page, click **Scan again** after the previous scan task ends to scan the image again.
>? Click ![](https://main.qcloudimg.com/raw/08dfa220659d6576a39a981e61ad02e2.png) to select multiple images and click **Scan again** next to ② to batch scan them again.

![](https://qcloudimg.tencent-cloud.cn/raw/c561a56ecb6204e15f13639fcced60d4.png)
3. On the **Local Images** page, click **Cancel scanning** to cancel scanning an image in "Scanning" status.
>? Click ![](https://main.qcloudimg.com/raw/08dfa220659d6576a39a981e61ad02e2.png) to select multiple images and click **Cancel scanning** next to ② to batch cancel them.

![](https://qcloudimg.tencent-cloud.cn/raw/772b580a1ce1a82832196828239cedc5.png)

### Custom list management
1. On the **Local Images** page, click ![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png) to pop up the **Custom List Management** window.
2. In the pop-up window, select the target type and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/8c1342b4db00c09680d672890baf2954.png" style="zoom:67%;" />

#### Key fields in the list
1. Creation time: The time when the image is created.
2. Last scanned: The time of the last scan.
3. Risks: Type of the risks to the container.
4. Status: Container scanning status, which can be **Scanned**, **Not scanned**, **Scanning**, **Cancelled**, or **Scan exception**.
>? We recommend you scan again in case of an exception.