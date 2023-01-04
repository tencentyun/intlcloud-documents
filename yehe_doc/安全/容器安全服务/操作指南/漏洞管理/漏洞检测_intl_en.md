TCSS periodically or promptly scans local and repository images for vulnerabilities. It bases the check on specified images or vulnerability types and allows for ignoring vulnerabilities. It notifies you of vulnerability risks, characteristics, severity, and fix suggestions on visual pages. This helps you better manage vulnerability risks to your images.

This document describes how to use the vulnerability detection feature to manage vulnerability risks to images. The feature supports quickly checking for system vulnerabilities, web application vulnerabilities, and emergency vulnerabilities.


## Prerequisites
You have purchased the [TCSS Pro Edition](https://www.tencentcloud.com/document/product/1163/50874).


## Vulnerability check
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and select **Vulnerability Detection** on the left sidebar.
2. On the **Vulnerability Detection** page, click **Quick check** to check for vulnerabilities and view the result.
![](https://qcloudimg.tencent-cloud.cn/raw/15a5aa99586889526b657348db9829b1.png)
3. In the **Quick check** pop-up window, select the target image and click **Check now**. The result will be visualized as charts on the **Vulnerability Detection** page.
>?
>- You need to license the image before the check.
>- A check generally takes 2–60 minutes, depending on the number of images, image size, and whether it's the first check.

![](https://qcloudimg.tencent-cloud.cn/raw/9bb71224509d04b9442b68cbdbed7c88.png)

## Viewing a vulnerability
1. On the [**Vulnerability Detection**](https://console.cloud.tencent.com/tcss/vulnerability/imageVul) page, view the information of the identified system vulnerabilities, web application vulnerabilities, and emergency vulnerabilities in the image. You can also view the affected local images, repository images, running containers, risk statistics, top 5 vulnerabilities, and images affected by critical and high severity vulnerabilities.
  - Top 5 vulnerabilities: The system ranks the top 5 vulnerabilities based on the CVSS score and dynamic risk level and displays their severity and the numbers of affected images (only those on the latest version) and containers. 
  - Images affected by Critical and High severity vulnerabilities: The system displays the trend of images (on the latest version) with extreme or high-risk vulnerabilities. After the switch to running containers, the system displays the trend of images with extreme or high-risk vulnerabilities and started containers. You can view the trend of the last 7 or 30 days.
2. In the vulnerability list, you can view the vulnerability name, severity, CVE No., first detected time, and latest detected time.
![](https://qcloudimg.tencent-cloud.cn/raw/829372447e4012f93564be3b36f237b1.png)
**Field description:**
 - Vulnerability name: The publicly known name of the vulnerability.
 - Severity: **Critical**, **High**, **Medium**, or **Low**, depending on the risk level of the vulnerability.
 - First detected: The time when the vulnerability is first detected in the image.
 - Latest detected: The time when the vulnerability is last detected in the image.
 - Affected local images: Number of local images found to contain the vulnerability, i.e., the number of local images affected by the vulnerability.
 - Affected repository images: Number of repository images found to contain the vulnerability, i.e., the number of repository images affected by the vulnerability.
 - Affected containers: Number of running containers found to contain the vulnerability, i.e., the number of running containers affected by the vulnerability.
>? The number of affected containers is based on the number of containers started in the affected local images. It is the count at the time of the check and is not subject to the container status change.

3. On the **Vulnerability Detection** page, you can filter vulnerabilities based on their urgency and priority.
![](https://qcloudimg.tencent-cloud.cn/raw/60d0a95657b86cc3d7d03a152c951ffa.png)
 - Urgency of the impact on the assets
    - Show only vulnerabilities that affect containers: This option displays the list of vulnerabilities that affect containers.
    - Only Latest images: This option displays the list of vulnerabilities that affect the latest image tag.
 - Priority
    - High & Critical: Vulnerabilities whose severity is extreme or high.
    - High-priority: High-priority vulnerabilities are vulnerabilities with urgent risks and need to be resolved as soon as possible.
    - POC/EXP: Vulnerabilities with the risk tag of EXP, POC, or EXP/POC.
    - Remote EXP: Vulnerabilities with the metric of NetWork (remote exploit) and with EXP.
5.	 Click **More filters** to search for vulnerabilities by severity, fix possibility, risk tag, CVE No., affected image ID, affected image name, affected container ID, affected container name, affected component version, or affected component name.
>? Vulnerabilities found based on the affected image ID, affected image name, affected container ID, and affected container name are visualized and don't affect the number of affected local images, repository images, or containers.

![](https://qcloudimg.tencent-cloud.cn/raw/e4f62e886b335209fb8515bb8a72c70a.png)

## Viewing vulnerability details
1. At the bottom of the [**Vulnerability Detection**](https://console.cloud.tencent.com/tcss/vulnerability/imageVul) page, view the vulnerability overview.
2. On the **Vulnerability Detection** page, click the **Vulnerability name** or **View details** in the **Operation** column of the vulnerability.
![](https://qcloudimg.tencent-cloud.cn/raw/5dffca641546162c043804b813f6871a.png)
3. On the **Vulnerability details** tab, view the vulnerability details, affected local images, affected repository images, and affected containers.
 - Vulnerability details: Include the description, type, severity level, disclosure time, solution, affected components, and characteristics of the vulnerability.
>?
>- Affected components and their versions come from the **Vendor Product** information of the vulnerability CPE in the National Vulnerability Database (NVD) and don't necessarily mean that the components exist in the checked images. The name of an affected component may differ from the actual name in the affected image.
>- To view the actually affected components in the image, select the **Affected local images** or **Affected repository images** tab and click **Expand** on the left of the image or click **View components** in the **Operation** column.

 ![](https://qcloudimg.tencent-cloud.cn/raw/1522b88f2b8d8c02ba19aecd03176c6c.png)
 - Affected local images: View the list of affected local images. You can search for images by image name, component name, or IP and view the numbers of associated servers and associated containers of the images.
 - Affected repository images: View the list of affected repository images. You can search for images by repository name/address.
 - Affected containers: View the list of affected containers. You can search for containers by container name/ID.
>? When the container status changes, the data in the list of affected containers may differ from the number of affected containers in the vulnerability list.

