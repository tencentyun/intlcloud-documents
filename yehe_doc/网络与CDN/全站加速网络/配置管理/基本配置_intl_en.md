You can view basic information and origin server information of a domain name in the ECDN Console. You can modify **Project**, **Origin Server Type**, and **Origin Server Address** of the domain name as needed.
- Basic information includes the acceleration domain name, CNAME record, project, and creation time of the acceleration service.
- Origin server information includes origin server type and origin server address.
>? If your application has been migrated to the CDN console, you can go to the console for operation by referring to [Content Delivery Network](https://intl.cloud.tencent.com/document/product/228).
## Domain Name Configuration Page
1. Log in to the [ECDN Console](https://console.cloud.tencent.com/dsa) and click **Domain Management** on the left sidebar to enter the management page.
2. Select **Manage** on the right of the target configuration domain name to enter the domain name configuration page.
![](https://main.qcloudimg.com/raw/dd32a2393844fa30784dedd2bdc272cd.png)
3. The **Basic Info** page of the domain name displays its basic configuration information, including the CNAME record, project, acceleration region, origin server information, and origin domain.
![](https://main.qcloudimg.com/raw/4a666cb9ee83ebfe8a2bb87b7d3d44d1.png)

## Basic Configuration Project
### Modifying project of domain name
1. Click **Modify** on the right of the project.
2. In the pop-up window, select the target project name, and click **OK**. 

### Modifying domain name acceleration region
1. Click **Modify** on the right of the acceleration region.
2. Select a domain name acceleration region. Currently, Mainland China, outside Mainland China, or global can be selected.
3. To avoid faulty operations, if you need to delete configuration of an acceleration region, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=83&level2_id=532&source=0&data_title=%E5%8A%A8%E6%80%81%E5%8A%A0%E9%80%9F%E7%BD%91%E7%BB%9C%20DSA&step=1) to apply for modification.

>? The acceleration service outside Mainland China is currently in beta test. If your account cannot modify the acceleration region, it indicates that you have not been granted the acceleration permission outside Mainland China. You can submit an application on the [ECDN global acceleration eligibility application page](https://intl.cloud.tencent.com/apply/p/1rks8dqy7lw), and we will review it in 5 business days and inform you of the result through SMS or internal message.

### Modifying origin server configuration
1. Click "Modify" on the right of the origin server configuration to enter the origin server modification page.
2. In the pop-up window, modify your origin server type, origin-pull policy, and origin server address. For more information, please see [Advanced Origin-Pull Policies](https://intl.cloud.tencent.com/document/product/570/35821).
3. After the modification is completed, click **OK** to submit the configuration. The system backend will distribute the new origin server modification to the domain name, which will take effect in 3–5 minutes.  
![](https://main.qcloudimg.com/raw/d124e64ad4faf93fc7f922a99835099a.png)

### Modifying origin-pull configuration
Click **Edit** next to the origin domain and modify it in the dialog box:
![](https://main.qcloudimg.com/raw/30b72a4fa1c6fc59fb2a65160feb736f.png)
![](https://main.qcloudimg.com/raw/eb8bcdb1264cffb77735ae7c376fc02f.png)
