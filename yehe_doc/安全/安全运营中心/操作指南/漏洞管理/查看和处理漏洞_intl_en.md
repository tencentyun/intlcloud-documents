## Prerequisites
To view or handle vulnerabilities, you must have enabled [CWP](https://buy.cloud.tencent.com/yunjing) and [Vulnerability Scan](https://buy.cloud.tencent.com/vss).
## Directions
### Pending Vulnerabilities Dashboard
The Pending Vulnerabilities Dashboard presents the general information of the current pending vulnerabilities, and the vulnerability list displays vulnerability details.
1. Log on to the [Security Operation Center Console](https://console.cloud.tencent.com/ssav2/vulner). In the left navigation pane, click **Vulnerability Management**.
2. On the Vulnerability Management page, click **Pending Vulnerabilities Dashboard**.
3. On the Pending Vulnerabilities Dashboard, you can find the name, CVE number, vulnerability level, and other information of a type of vulnerability.
	- **Search**
At the top of the Pending Vulnerabilities Dashboard, locate a vulnerability by entering its name or CVE number or using filters such as Vulnerability Type and Risk Level.
![](https://main.qcloudimg.com/raw/9b83993accbf554cc97632b79ba3d9b3.png)
	- **View details of a pending vulnerability**
On the Pending Vulnerabilities Dashboard, click **Vulnerability Name**. On the Vulnerability Details page that appears, view the basic information and asset information of the vulnerability. Click **Number of Assets Not Fixed**. On the Vulnerability List page, you can view the records of assets not fixed.
![](https://main.qcloudimg.com/raw/1b6b921808ef70d2408329165582f2ef.png)
In the upper-right corner of the Vulnerability Details page, you can click <img src= "https://main.qcloudimg.com/raw/5d6f28083f0484b4f0cb46b9c32717b5.png" style="margin:0;"> to export vulnerability details and the list of affected assets.
![](https://qcloudimg.tencent-cloud.cn/raw/f156cac2e0aae6e83bd065f30dff7147.png)

### Vulnerability List
1. Log on to the [Security Operation Center Console](https://console.cloud.tencent.com/ssav2/vulner). In the left navigation pane, click **Vulnerability Management**.
2. On the Vulnerability Management page, click **Vulnerability List**.
3. On the Vulnerability List page, you can view details lists such as the number of assets with vulnerabilities, pending vulnerabilities, and vulnerabilities under fixing. In the vulnerability details list, you can export, search, and view details.
- **Vulnerabilities Summary**
   - **Number of assets with vulnerabilities**: displays the total number of assets with vulnerabilities.
   - **Overview of pending vulnerabilities**: displays the total number of pending vulnerabilities and the numbers of high-, medium-, and low-risk pending vulnerabilities.
   - **Overview of vulnerabilities under fixing**: displays the total number of vulnerabilities under fixing and the numbers of high-, medium-, and low-risk vulnerabilities under fixing.
   - **Overview of handled vulnerabilities**: displays the total number of handled vulnerabilities and the numbers of high-, medium-, and low-risk handled vulnerabilities.
- **Trend graph of pending vulnerabilities*
This trend graph shows the trend of pending vulnerabilities in the past 24 hours, 7 days, 30 days, and 90 days.
![](https://main.qcloudimg.com/raw/b2788c6a0fb315f297a7a86374a5df2d.png)
- **Search**
At the top of the list of vulnerability details, you can locate a vulnerability by using filters such as Vulnerability Type, Risk Level, status and Last Checked, or by entering its asset name or ID.
![](https://qcloudimg.tencent-cloud.cn/raw/b98fba706645fc5a68dd44a862ee55d4.png)
- **Set all as processed**
After all vulnerabilities are fixed as instructed, you can click **Set all as processed** in the upper-left corner of the list. Then the vulnerabilities in "Pending" or "Fixing" status will be changed to the "Processed" status.
- **Status change**
	- **Method 1**: In the list of vulnerability details, select the target vulnerabilities, choose the required status from the **Status Change** dropdown list at the top of the list to batch change the status.
	- **Method 2**: In the list of vulnerability details, choose the required status from the **Status Change** dropdown list in the operation column on the right of the target vulnerability to change the status.
>?
>- Confirm processing: You can confirm the processing of vulnerabilities after they are processed based on the description and fixing instructions on the Vulnerability Details page.
>- Mark as "Fixing": You can mark vulnerabilities as "Fixing" when they are being processed based on the description and fixing instructions on the Vulnerability Details page.
>- Ignore vulnerabilities: Fill in scenario-specific comments when ignoring the scanned vulnerabilities. Once ignored, CWP (Cloud Workload Protection) or Vulnerability Scan will no longer detect the selected vulnerabilities.

![](https://qcloudimg.tencent-cloud.cn/raw/efa6f9b4221a44aeb4098b967eaa7e52.png)
- **Redetection**
	- **Method 1**: In the list of vulnerability details, select the target vulnerabilities, and then click **Redetect** at the top of the list to redetect vulnerabilities in batches.
	- **Method 2**: In the list of vulnerability details, click **Redetect** in the operation column on the right of the target vulnerability.
>? "Pending" and "Fixing" vulnerabilities also can be redetected.

![](https://qcloudimg.tencent-cloud.cn/raw/4ad0fe3d5e73623157f9b344c1b161eb.png)
- **Ignored Records**
On the Vulnerability Management page, you can click "Ignored Records" to view the records of ignored vulnerabilities. In the list of ignored records, you can unignore them. Unignoring resumes detection of that asset for that vulnerability.
    - Method 1: In the list of ignored records, select the target vulnerabilities, and click **Unignore** at the top of the list to unignore records in batches.
    - Method 2: In the list of ignored records, click **Unignore** in the operation column on the right of the target vulnerability to remove the ignored record.
![](https://qcloudimg.tencent-cloud.cn/raw/d8886de0fd4c80680802b832130ed17c.png)
- **Vulnerability details**
	In the vulnerability details list, click **View Details** in the operation column on the right of the target vulnerability. On the Vulnerability Details page that appears, you can view the basic information of the vulnerability.
- **Vulnerability synchronization**
In the upper-right corner of the vulnerability details list, click on the Refresh button <img src= "https://main.qcloudimg.com/raw/bc8e502faa0460899d1c97b54a510bf1.png" style="margin:0;"> to synchronize vulnerabilities with CWP.
- **Export**
In the upper-right corner of the vulnerability details list, click on the Export button <img src= "https://main.qcloudimg.com/raw/5d6f28083f0484b4f0cb46b9c32717b5.png" style="margin:0;"> to export all data in the list by default. You can also select the "Export partial data" option.
>? If you select the "All" option at the top of the list, all data on the current page is selected.

- **Toggle full screen**
In the upper-right corner of the vulnerability details list, click on the button <img src= "https://main.qcloudimg.com/raw/e7325c2591be9e720aed26c41ccb2ab1.png" style="margin:0;"> to toggle the list to full screen mode.

### Asset vulnerabilities
1. Log on to the [Security Operation Center Console](https://console.cloud.tencent.com/ssav2/vulner). In the left navigation pane, click **Vulnerability Management**.
2. On the Vulnerability Management page, click **Asset Vulnerabilities** to go to the list of server vulnerabilities.
3. In the list of server vulnerabilities, you can view vulnerability details and scan vulnerabilities.
![](https://main.qcloudimg.com/raw/72fca63fdf99f2ba9a16a35578b91212.png)
 - Click "Asset ID" to go to the details page where you can view asset details.
 - Click the number of risks in the "Vulnerability (CWP)" column to view the vulnerability data from CWP for the asset.
 - Click the number of risks in the "Vulnerability (Scan)" column to view the vulnerability data from Vulnerability Scan for the asset.
 - Click "Scan" to scan the asset through Vulnerability Scan.
>? "Not configured" indicates that you did not add the server to the list of servers in [Asset Management](https://console.cloud.tencent.com/vss/assets/host) through the Vulnerability Scan Console.

![](https://qcloudimg.tencent-cloud.cn/raw/8d39d8c68a7897302f2d9f3548719f83.png)

4. On the Vulnerability Management page, click **Website Vulnerabilities** to go to the list of website vulnerabilities.
