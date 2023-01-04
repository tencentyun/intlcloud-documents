This document describes the security overview of each security module of TCSS.
- Displays the overview of container security risks and container security events over time in real time.
- Describes TCSS versions and usage, along with upgrade and renewal features.

## Key Features
Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and select **Security Dashboard** on the left sidebar.
### Viewing asset information
1. On the **Security Dashboard** page, the asset information module displays the numbers of containers, images, clusters, and nodes.
![](https://qcloudimg.tencent-cloud.cn/raw/7f31a74181ba9e504223dde07f5b4f20.png)
2. On the **Security Dashboard** page, click **Modules** to enter the module list on the **Asset Management** page.

### Viewing versions, usage, upgrade, and renewal
On the **Security Dashboard** page, the version information window displays the current TCSS version and its expiration date. The following takes the Pro Edition as an example:
 - If the current version will expire soon, you will be prompted to renew it. Then, you can click **Renew now**.
![](https://qcloudimg.tencent-cloud.cn/raw/85546e9ac10de2dbab598b8a496c01ce.png) 
 - The version information window also displays the current licenses, including the total/licensed cores and purchased licenses.
    - Total/Licensed cores: **Total cores** indicates the total number of virtual cores on the business node, while **Licensed cores** indicates the number of cores enabled in the Pro Edition.
>?
>- When licensed cores are fewer than total cores, the required number of cores will be displayed. Then, you can click **Upgrade** to enter the purchase page and purchase licenses.
>- If you don't purchase the required number of cores, the flexible billing mode will apply, i.e., each excessive core will be charged at 0.25 USD/day.

  - Purchased licenses: The number of purchased image security scans.
>?
>- When there are local images or repository images with image security scan not enabled in the business environment, the required number of image licenses will be displayed. Then, you can click **Purchase** to enter the purchase page and purchase licenses.
>- After purchasing the image licenses, go to **Image Security** > **Local Images**/**Repository Images** to configure the licenses. You can customize the images for which to enable image security scan.

### Viewing pending events
1. On the **Security Dashboard** page, the **Pending events** module displays the number of pending security events.
![](https://qcloudimg.tencent-cloud.cn/raw/554801de598f94909689f0ccc879a053.png)
2. On the **Security Dashboard** page, click **Modules** to enter the security event page to view the details and process the events.

### Viewing security events over time
On the **Security Dashboard** page, the **Security events over time** module displays runtime security events over time in the last 7 or 30 days. You can switch between **7 days** and **30 days**.
![](https://qcloudimg.tencent-cloud.cn/raw/9ad2ab6cbaca1abe26894d4b3b5dde47.png)

### Viewing local image risks over time
The **Security Dashboard** page displays the trend of vulnerabilities, viruses, trojans, and sensitive data pieces of local images over time in the last 7 or 30 days. You can switch between **7 days** and **30 days**.
![](https://qcloudimg.tencent-cloud.cn/raw/34db8b3f4ffc36f01e7275830db2eeb0.png)

### Viewing risks in local images
On the **Security Dashboard** page, the **Risks in local images** module displays the total number of risks including sensitive data pieces, viruses, trojans, and vulnerabilities, as well as the severity distribution of the current image. Click **View details** to enter the **Image Security** module to view the details and handle the risks.
 ![](https://qcloudimg.tencent-cloud.cn/raw/68ba7ebb294caeb4be4eab04b1e293a9.png)