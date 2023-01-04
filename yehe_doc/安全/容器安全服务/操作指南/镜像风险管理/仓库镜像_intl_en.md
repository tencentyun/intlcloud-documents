This document describes the repository image feature and how to enable data scan and view the repository image list.
>? The following image repositories are supported:
>- TCR/CCR
>- Third-party Harbor

## Prerequisites
You have purchased the [value-added feature](https://www.tencentcloud.com/document/product/1163/50875) of TCSS for image security.

## Connecting to TCR/CCR
TCSS and TCR/CCR are integrated by default to scan TCR and CCR images.
>?
>- By default, TCSS requests TCR repository assets over the public network. If you enable access control for your repository instance, you need to add the service IP range to the allowlist before use or switch the network type. On the [**Repository Images**](https://console.cloud.tencent.com/tcss/security/imageStore) page, click **Operation Guide** at the top to add the IP to the allowlist or switch to VPC as instructed.
>- During your first use, you need to manually update the repository image data. On the [**Repository Images**](https://console.cloud.tencent.com/tcss/security/imageStore) page, click **Data update** in the top-right corner to update the data, which may take a long time the first time.
>- The backend will automatically update the repository image data between 0:00 AM and 3:00 AM every day.

## Connecting to Harbor
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and select **Image Risk Control** > **Repository Images** on the left sidebar.
2. On the **Repository Images** page, click **Image repository management** in the top-right corner.
![](https://qcloudimg.tencent-cloud.cn/raw/ff436b4e47732b3484916a7ed990ed83.png)
3. In the image repository list, click **Add image repository**.
4. In the **Add image repository** pop-up window, configure parameters and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/5970b9994b88a371f7192b13ebb7be72.png" style="zoom:67%;" />
Parameters:
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Instance name</td>
<td>Enter the image repository name, which is unique and cannot be left empty.</td>
</tr>
<tr>
<td>Repository type</td>
<td>Select a third-party image repository, which can be <strong>Harbor</strong>.</td>
</tr>
<tr>
<td>Version</td>
<td>Select the third-party image repository version, which can be:<ul><li>V1: The image repository version of 1.X.X.</li>  <li>  V2: The image repository version of 2.X.X or later.</li></td>
</tr>
<tr>
<td>Network type</td>
<td>Select the network access type of the third-party image repository, which can be <strong>Public network</strong>.</td>
</tr>
<tr>
<td>Region</td>
<td>Select the region of the third-party image repository, which is **Default region** for Harbor.</td>
</tr>
<tr>
<td>Address</td>
<td>Enter the access address of the third-party image repository.</td>
</tr>
<tr>
<td>Username</td>
<td>Enter the username for accessing the third-party image repository.</td>
</tr>
<tr>
<td>Password</td>
<td>Enter the password for accessing the third-party image repository.</td>
</tr>
<tr>
<td>Limit</td>
<td>Select the number of images that can be pulled synchronously every hour. Valid values: 5, 10, 20, 50, 100, 500, 1000, unlimited (default).</td>
</tr>
<tr>
<td>Validate remote certificates</td>
<td>Specify whether to verify the certificate of the remote image repository for image sync. If the repository uses a self-signed or non-trusted certificate, do not select this option. By default, this option is selected.</td>
</tr>
</tbody></table>

## Enabling Data Scan
On the [**Repository Images**](https://console.cloud.tencent.com/tcss/security/imageStore) page, the data scan module displays the number of images at risk, total number of images, and the numbers of vulnerabilities, viruses, trojans, and sensitive data pieces in the images after the last scan.

### Enabling quick scan
1. On the **Repository Images** page, click **Scan now** on the right to get the latest image data or risk information.
![](https://qcloudimg.tencent-cloud.cn/raw/21848447eea15d8153c125325ef0a416.png)
2. On the **Scanning settings** page, select the **Risk category** and **Images** as needed.
 - Risk category: **Vulnerabilities** or **Sensitive data**.
 - Images: **All images** or **Specified images**. Click ![](https://main.qcloudimg.com/raw/37d813d17a69271ce31b3233ad0a949e.png) or ![](https://main.qcloudimg.com/raw/be9e47bccb644d8a099149bac4aef1e0.png) to select or delete the target specified image.
>? You can press Shift to select multiple ones.

![](https://qcloudimg.tencent-cloud.cn/raw/193fec47268152f6f22c00917f18f0c3.png)
4. After selecting the target content, click **Scan now**.
>! After the scan starts, all images with the same ID as the selected image will be scanned at the same time.

### Enabling scheduled scan
1. On the **Repository Images** page, click **Scheduled scan settings** on the right to specify whether to enable the scheduled scan feature.
![](https://qcloudimg.tencent-cloud.cn/raw/2490eb906ee424df4da3668467a6da67.png)
2. On the **Scheduled scan settings** page, toggle on the **On/Off** switch and set the **Frequency**, **Risk category**, and **Images** as needed.
  - Frequency: It can be every day, every 7 days, every 15 days, every 30 days, or a specified time range.
  - Risk category: Click ![](https://main.qcloudimg.com/raw/86d08a45be3bc5b91de551b390ebe15d.png) to select **Vulnerabilities**, **Sensitive data**, or **Virus & Trojan** as needed.
  - Images: **All images** or **Specified images**. Click ![](https://main.qcloudimg.com/raw/37d813d17a69271ce31b3233ad0a949e.png) or ![](https://main.qcloudimg.com/raw/be9e47bccb644d8a099149bac4aef1e0.png) to select or delete the target specified image.
>? You can press Shift to select multiple ones.

![](https://qcloudimg.tencent-cloud.cn/raw/c0214f06f98410aeba6119c4da6bf618.png) 
4. After selecting the target content, click **Set** or **Cancel**.

## Viewing the List of Repository Images
Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and select **Image Risk Control** > **Repository Images** on the left sidebar.
### Image licensing event
1. On the **Repository Images** page, click **License**.
![](https://qcloudimg.tencent-cloud.cn/raw/5d9c5a577d4d05e063ecc06024012f95.png)
2. In the pop-up window, click **OK**.
>? A license will be assigned to this image.

### Filtering images
On the **Repository Images** page, filter images as follows:
 - Click the scanning status drop-down list to filter images by scanning status.
<img src="https://qcloudimg.tencent-cloud.cn/raw/81ad2f85e431a81f0e3d298663d13393.png" style="zoom:67%;" />
 - Click the security status drop-down list to filter images by security status.
<img src="https://qcloudimg.tencent-cloud.cn/raw/088d6ed03dec1a3ff217e2599b64e00a.png" style="zoom:67%;" />
 - Click the repository type drop-down list to filter images by repository type.
<img src="https://qcloudimg.tencent-cloud.cn/raw/47758deacb9b105b460dfde4b021f609.png" style="zoom:80%;" />
 - Click the licensing status drop-down list to filter images by licensing status.
![](https://qcloudimg.tencent-cloud.cn/raw/5fd65ec7c30fe0f69ed981ef5ad1bba7.png)
 - Click the search box and search for images by keyword such as image name or image digest.
![](https://qcloudimg.tencent-cloud.cn/raw/bd9fd719cc1c29ecaf86a11fbd760f16.png)

### Exporting an image
On the **Repository Images** page, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target image repository and click ![](https://main.qcloudimg.com/raw/24d375a75e4ee95c77910d101f7203dd.png) to export it.
![](https://qcloudimg.tencent-cloud.cn/raw/58af135a04cad401d294c8c6f5a4bde4.png)

### Viewing the list details
On the **Repository Images** page, click **Details** to display the drawer on the right, which displays the image risk information, details, and list of vulnerabilities.
>?
>- Image risk: It indicates whether the image scan is successful and the numbers of vulnerabilities, viruses, trojans, and sensitive data pieces.
>- Image details: It includes the image name, image digest, and image size.
>- Vulnerability list: You can filter image security vulnerability events by vulnerability severity or search for them by vulnerability name. Click **View details** to view the vulnerability details and fix suggestion.
>- Virus and trojan list: You can filter image security events by virus or trojan severity or search for them by filename. Click **View details** to view the virus or trojan details and suggestion.
>- Sensitive data list: You can filter security events by sensitive data severity, name, or type.
>- Image build history: It logs the image build history.

![](https://qcloudimg.tencent-cloud.cn/raw/d14610d7260e0121408f96497929c561.png)

### Image scanning
1. On the **Repository Images** page, click **Scan now** > **OK** to scan an image in "Not scanned" status.
![](https://qcloudimg.tencent-cloud.cn/raw/f823637c5aa5feb425a8028d2e63e555.png)
2. On the **Repository Images** page, click **Cancel scanning** to cancel scanning an image in "Scanning" status.
>? Click ![](https://main.qcloudimg.com/raw/08dfa220659d6576a39a981e61ad02e2.png) to select multiple images and click **Cancel scanning** next to ② to batch cancel them.

![](https://qcloudimg.tencent-cloud.cn/raw/8ebb8afb81335b5b4e48bb948e82b29a.png)
3. On the **Repository Images** page, click **Scan again** after the previous scan task ends to scan the image again.
>? Click ![](https://main.qcloudimg.com/raw/08dfa220659d6576a39a981e61ad02e2.png) to select multiple images and click **Scan again** next to ② to batch scan them again.

![](https://qcloudimg.tencent-cloud.cn/raw/38ecf1dc48567fdf322953b2d3b1f602.png)

### Custom list management
1. On the **Repository Images** page, click ![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png) to pop up the **Custom List Management** window.
2. In the pop-up window, select the target type and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/152b44b9e08a9897baf033472fdffacf.png" style="zoom:67%;" />

#### Fields in the list
1. Image repository address: Source address of the repository image.
2. Repository type: Type of the image repository, which can be TCR or CCR.
4. Image version: Tag of the repository image.
6. Last scanned: The time of the last scan.
7. Risks: Type of the risks to the container.
8. Status: Container scanning status, which can be **Scanned**, **Not scanned**, **Scanning**, **Cancelled**, or **Scan exception**.
>! We recommend you scan again in case of an exception.