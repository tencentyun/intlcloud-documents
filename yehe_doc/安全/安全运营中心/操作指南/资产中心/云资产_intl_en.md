The Security Operation Center provides the Asset Management feature to help you get a full picture of the security posture of your cloud products. Cloud assets display asset information from dimensions such as asset type distribution, configuration risks, threat alerts, and vulnerabilities. To facilitate the security control of assets, Asset Center provides asset grouping and tag classification features. You can group assets to view threat alerts by group, or filter assets with the same attributes by asset tags.

## Directions

1. Log on to the [Security Operation Center Console](https://console.cloud.tencent.com/ssav2/assets). In the left navigation pane, select **Asset Center** > **Cloud Assets** to go to the Cloud Assets page.
2. If you have not created a preset role for the service and granted permissions to the Security Operation Center, on the Cloud Assets page, click **Go to access manager**. On the Role Manager page that appears, click **Agree to grant permissions**. If you have granted such permissions, skip this step.
3. The upper half of the Cloud Assets page shows the following statistical charts.

- **Asset type distribution**: This section displays the number and proportion of each asset type, including Cloud Virtual Machine (CVM), TencentDB for MySQL, TencentDB for MariaDB, TencentDB for PostgreSQL, TencentDB for Redis, TencentDB for MongoDB, LoadBalancer (LB), Cloud Block Storage (CBS), Cloud Object Storage (COS), SSL Certificates, Tencent Container Registry, VPN Gateway, NAT Gateway, and non-Tencent Cloud servers.
- **Top 5 assets with the maximum number of configuration risks**: displays the 5 assets with the maximum number of configuration risks and quantities.
- **Top 5 assets with the maximum number of vulnerabilities**: displays the 5 assets with the maximum number of vulnerabilities and quantities.
- **Top 5 assets with the maximum number of threat alerts**: The 5 assets with the maximum number of threat alerts and quantities are displayed.

4. The lower half of the Cloud Assets page displays a cloud asset list from different dimensions.

- **Accessibility**
  In the upper-right corner of the cloud asset list, you can search assets, refresh the asset list, set the columns to display, export the list, and toggle full screen.
- **Search cloud assets**
  In the upper-right corner of the cloud asset list, click the search box, select a resource attribute, enter keywords, and then press **Enter** to search eligible cloud assets.
  
  >! Multiple keywords for the same "filter tag" (that is, resource attribute) are separated by vertical bars "|". Multiple "filter tags" (that is, resource attribute) are separated by pressing **Enter**.

- **Refresh the cloud asset list**
  To refresh the cloud asset list, click on the Refresh icon <img src= "https://main.qcloudimg.com/raw/7ebc758b02bd8690c885af3f7355e8d7.png" style="margin:0;">
- **Set the columns to display**
  Click <img src= "https://main.qcloudimg.com/raw/28f2bfe46373d488d335fa9af4599747.png" style="margin:0;"> for setting the columns to display. On the Custom List Management page that appears, select the required information fields to display as the headers of the cloud asset list, up to 19 fields.
- **Export cloud assets**
  Click on the Export button <img src= "https://main.qcloudimg.com/raw/5d6f28083f0484b4f0cb46b9c32717b5.png" style="margin:0;"> to export all asset information in the cloud asset list by default. You can also export partial cloud asset information.
- **Toggle full screen**
  Click <img src= "https://main.qcloudimg.com/raw/8e4e975a89de9d70be4768661a6f535b.png" style="margin:0;"> to toggle the cloud asset list to the full screen mode. Click on this button again to exit the full screen mode.
- **Filter/Sort** 
    1. To filter cloud assets, click the header "Asset Type", "Project", or "Region" of the cloud asset list. 
    2. Click the header "Configuration Risk", "Threat Alert", "Vulnerability", or "Discovery Time" to sort the cloud asset list in ascending or descending order. Click the **number of threat alerts** in the list to go to the details page.
  
  > ? By default, the cloud asset list is sorted in descending order by the sum of the numbers of configuration risks, threat alerts, and vulnerabilities.

- **View asset details**
In the cloud asset list, click the asset name to open the asset details page. The asset details page displays different items depending on the asset type. 
    - The asset details page of CVMs displays basic information, fingerprint information, configuration risks, attack surface, vulnerabilities, threat alerts, and configuration history. 
    - The asset details page of LoadBalancer displays basic information, configuration risks, attack surface, threat alerts, and configuration history. 
    - The asset details pages of COS, TencentDB for MySQL, TencentDB for PostgreSQL, TencentDB for MariaDB, TencentDB for Redis, TencentDB for MongoDB, SSL Certificates, Container Image Registry, and CBS display basic information, configuration risks, and configuration history. 
    - The asset details pages of non-Tencent Cloud servers display basic information, configuration risks, threat alerts, and vulnerabilities.

**The fields in the asset details page are defined as follows**: 
   - **Basic information**: The "Basic information" section displays different content for different asset types. For example, the basic information of a CVM includes asset ID, asset type, project, region, instance type, network, subnet, IPv4 address (public and private IP addresses), IPv6 address, status, discovery time, tag, risk tag, and group. 
   - **Fingerprint information**: You can view the fingerprint information of CVM assets from the dimensions of ports, processes, components, accounts, and account change history. 
   - **Attack surface**: You can view the services, ports, and components exposed by CVM and LB assets in Internet attack surface mapping. 
   - **Configuration risks**: You can view the configuration risks of all asset types from the dimensions of risk types and check results. 
   - **Vulnerabilities**: You can view the vulnerability information of CVM assets from the dimensions of system component vulnerabilities, Web application vulnerabilities, and security baselines. 
   - **Threat alerts**: You can view the threat alerts of CVM assets from the dimensions of alert categories, alert actions, attack results, and alert status. 
   - **Configuration history**: You can view the configuration history of all asset types, and search configuration history by specifying a time range or keywords. You can also view configuration history details and click "Ignore" to ignore unimportant configuration history. If you need to unignore it, click "Retrieve" on the right side of the search box.
