You can view basic information and origin server information of domain names in the ECDN Console. You can modify the **project**, **origin server type**, and **origin server address** of domain names as needed.
- Basic information includes the acceleration domain name, CNAME record, project, and creation time of the acceleration service.
- Origin server information includes origin server type and origin server address.

## Domain Name Configuration Page
1. Log in to the [ECDN Console](https://console.cloud.tencent.com/dsa) and click **Domain Management** on the left sidebar to enter the management page.
2. Select **Manage** on the right of the target configuration domain name to enter the domain name configuration page.
3. The **Basic Info** page of the domain name displays basic configuration information of the domain name, including the domain name CNAME record, project, acceleration region, origin server information, and origin domain.

## Basic Configuration Project
### Modifying project of domain name
1. Click **Modify** on the right of the project.
2. In the pop-up window, select the target project name, and click **OK**. 

### Modifying domain name acceleration region
1. Click **Modify** on the right of the acceleration region.
2. Select a domain name acceleration region. Currently, Mainland China, outside Mainland China, or global can be selected.
3. To avoid faulty operations, when you need to delete configuration of an acceleration region, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=83&level2_id=532&source=0&data_title=%E5%8A%A8%E6%80%81%E5%8A%A0%E9%80%9F%E7%BD%91%E7%BB%9C%20DSA&step=1) to apply for modification.

> The acceleration service outside Mainland China is currently in beta. If your account cannot modify the acceleration region, it indicates that you have not been granted the acceleration permission outside China. You can submit an application on the [ECDN global acceleration eligibility application page](https://cloud.tencent.com/apply/p/4q956obis68), and the system will review it in 5 business days and inform you of the result through SMS or internal message.

### Modifying origin server configuration
1. Click "Modify" on the right of the origin server configuration to enter the origin server modification page.
2. In the pop-up window, modify your origin server type, origin-pull policy, and origin server address. For more information, please see [Advanced Origin-Pull Policies](https://cloud.tencent.com/document/product/570/19915).
3. After the modification is completed, click **OK** to submit the configuration. The system backend will deliver the new origin server modification to the domain name, which will take effect in 3–5 minutes.  


### Modifying origin-pull configuration
Click **Edit** next to the origin domain and modify it in the dialog box.

