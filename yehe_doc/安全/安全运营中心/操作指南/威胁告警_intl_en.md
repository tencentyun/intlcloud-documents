## Overview

The Threat Alerts module integrates Tencent Cloud's threat analytics methods and event investigation capabilities. You can view and analyze alerts with potential threats from "Urgent", "Prioritized protection", and other scenarios in this module.

For centralized management and analysis of threat alerts on the public cloud, the Security Operation Center (SOC) collects the alerts from [CWP](https://console.cloud.tencent.com/cwp/manage), [CFW](https://console.cloud.tencent.com/cfw/ips), and [WAF](https://console.cloud.tencent.com/guanjia/ip/list). These alerts can be managed by setting their status to "Open" or "Close".

You can perform various actions on alerts in the Alert Details page. All historical actions are recorded in the Handling Center. SOC also integrates the data from Threat Intelligence X to facilitate alert handling. If you have no alerts that have significant impact, you can generate sample alerts as instructed in the "Usage Instructions" section. Sample alerts help you learn about this module and are only stored in the system for 10 minutes.

## Directions

1. Log on to the [Security Operation Center Console](https://console.cloud.tencent.com/ssav2/response). In the left navigation pane, click **Threat Alerts** to go to the Threat Alerts page.
2. A "Threat Operation Instructions" prompt box pops up on the page. You can view the instructions for threat alerts. [](id:2)
   - Click on the icon ![](https://qcloudimg.tencent-cloud.cn/raw/6019d894f526e6f160f654d5d6905f36.png) next to **Not Recommended** to view the specific instructions.
   - Click **Download the Threat Operation Instruction Manual** to download the manual.
   - Clicking **Download later** indicates not to download this manual. When you reopen the Threat Alerts page, the "Threat Operation Instructions" prompt box will not appear. But you can view this manual by clicking **Threat Operation Instructions** in the "Usage Description" section.
3. At the top of the Threat Alerts page, Usage Description is displayed by default. Click **View full description** to view the full documentation. Click ** Threat Operation Instructions**. A "Threat Operation Instructions" prompt box appears. For more information, see [Step 2](#2). To view the list of threat alerts and other actions, click **Hide** in the upper-right corner to hide this area. You can also click **Usage Description** to show this area.

### Quick filter area

1. In the upper part of the quick filter area, you can select a scenario and filter the alert records of yesterday, today, last 7 days, last 30 days, or a specified time period in that scenario.
   The three scenarios are described as follows.:
   - **Urgent**
     Based on the analytics in SOC, the alerts that have caused or are likely to cause the compromise of assets are filtered out. Users should troubleshoot and handle these alerts one by one. After all alerts are analyzed or handled, you can close these alerts. After that, they will no longer appear in the "Urgent" scenario.
   - **Prioritized protection**
     SOC will filter out all alerts that still have the compromise risk, and these alerts have potential adverse impact. The alerts appearing in the "Urgent" scenario also appear in this filter mode. After all alerts are analyzed or handled, you can close these alerts. After that, they will no longer appear in the "Prioritized protection" scenario.
   - **Full alert**
     It is not recommended for operational purpose, but mainly for audit (or query in the case of suspected false negatives). In this case, a huge number of alerts are filtered out. It is often difficult to analyze them one by one. All closed alerts are only displayed here.
2. In the lower part of the quick filter area, you can filter alert records by alert sources and alert categories.
   - Alert sources: include Web Application Firewall (WAF), Cloud Workload Protection (CWP), Cloud Firewall (CFW), and SOC. The digits on the right of the alert source name indicate the number of alerts from that source that meet the current filtering criteria. You can select one or more alert sources for searching.
   - Alert categories: Alert categories are divided into level 1 and level 2 alert categories. Level 1 alert categories include WEB attack, vulnerability attack, unusual server behavior, malicious program, brute force cracking, and access control. The digits on the right of the category name indicate the number of alerts of that category that meet the current filtering criteria. Click the name of a level 1 alert category. A drop-down menu of level-2 alert categories appears. You can select one or more alert categories for searching.

### Main functional areas

In the area for displaying the alert list, the alert list is displayed by alert time in descending order by default. The alert lists display the same items and work in a similar way in the three scenarios, as described below.

#### Search

In the upper-right corner of the alert list, click the Search input box, select one or more "Resource Attributes" (that is, filter tags), and then press **Enter** twice to separate. Then enter one or more keywords, where multiple keywords are separated by vertical bars "|". When you finish typing, press **Enter** or click on the button ![](https://qcloudimg.tencent-cloud.cn/raw/9b9a5be3aa148344172ae9fbd9df2740.png).

#### Sort

Click the header "Alert Name/Time" in the alert list to sort by alert name or by alert time in ascending/descending order.

#### Filter

Click the header "Alert Level", "Attack Chain", "Attack Tactics", "Alert Action", "Compromise Status", "Event Investigation", "Alert Status", "Asset Project", and "Asset Group" in the alert list to filter alerts.
The preceding fields are described as follows:

- Alert Level: Options include Unknown, Low Risk, Medium Risk, High Risk, and Critical.
- Attack Chain: Options include Reconnaissance, Weaponization, Attack Tool Delivery, Vulnerability Exploitation, Installation, Command and Control, and Target Accomplishment.
- Attack Tactics: Options include Reconnaissance, Resource Development, Initial Access, Execution, Persistence, Privilege Escalation, Defense Evasion, Credential-based Access, Discovery, Lateral Movement, Collection, Command and Control, Disclosure, and Impact.
- Alert Action: Options include "Detected Only" and "Blocked".
  - Detected Only: means that the alert is not blocked by the security device, and you must confirm whether it may cause a compromise.
  - Blocked: means that the alert has been blocked by the security device and will not cause further damage.
- Compromise Status: Options include Compromised, Suspected Compromise, Not Compromised, and Unknown.
  - Compromised: means that the server has compromised and SOC has traced the intrusion process.
  - Suspected Compromise: means that the server may have compromised, but SOC has not found other evidence for the compromise. Whether an asset has compromised must be further determined by human.
  - Not Compromised: means that SOC confirmed that the alert did not cause any damage to the attack target.
  - Unknown: The current detection technology cannot determine whether this alert indicates that an asset has compromised. Whether an asset has compromised must be further determined by human.
- Event Investigation: Options include No Event Generated, Investigating, and Investigation Complete.
- Investigation Complete: means that an analysis result has been generated for the current event. Click **View Details** in the Event Investigation column or click **Alert Name** -> **Event Investigation Results** to view the basic information, affected assets information, attack chain process of attack techniques and tactics, details of intrusion timeline, list of alerts triggered by the event, and list of concerns of the event, and perform related actions.
  - Investigating: means that the current event is under investigation, without conclusion reached.
  - No Event Generated: means that this alert has no relation with any event.
  - Alert Status: Options include "Open" and "Close".
    > ?
    >
    > - SOC will initiate event investigation for alerts that pose a risk of compromise, ascertain the whole attack process of the event, and determine the event nature. Once an alert is in Investigation Complete status, you can view the alert details. Some alerts cannot be investigated for now. Tencent Cloud will cover more scenarios very soon. Stay tuned.
    > - For more information about the tactical phases in ATT&CK, see [MITRE](https://attack.mitre.org/). In the future, we will enrich the local knowledge base of Tencent Cloud to help you quickly learn and use related capabilities.

### Area for displaying the alert list

#### Copy the alert ID

In the alert list, click ![](https://qcloudimg.tencent-cloud.cn/raw/63006f19ade629f7e23a99521f2f632a.png) next to the alert ID to copy the full alert ID for subsequent queries or other operations.

#### View alert details

1. In the alert list, click the alert name or "Attack IP" or "Victim IP" in the "Concern" column to go to the Alert Details tab.
2. In the Alert Details tab, you can view the details of affected assets, alert situation, alert details (you can switch between **List Mode** and **JSON Mode**), and alert concerns.
3. In the Alert Concerns tab, you can click **Isolate** to isolate the affected assets from the server.
   > ?
   >
   > - To view threat intelligence of alert concerns, you must have [Security Operation Center Premium](https://buy.cloud.tencent.com/soc?type=new) enabled.
   > - Server isolation mainly serves as a mitigation means to prevent a compromised server from infiltrating internally after a major security issue occurs. This handling method may suspend the business. We recommend that you communicate with business personnel before handling.

#### Custom list management

In the upper-right corner of the alert list, click ![](https://qcloudimg.tencent-cloud.cn/raw/9b06adf166ff2f4eed825658eaecb95b.png). On the Custom List Management page that appears, select the required fields (up to 14 fields), and click **OK** to customize the columns to display on the alert list.

#### Manually synchronize alert events

In the upper-right corner of the alert list, click ![](https://qcloudimg.tencent-cloud.cn/raw/4c1c2f6300eb800e5c7c43ba1e1030c5.png) to synchronize the alert events detected by other security products.

#### Export alert data

In the upper-right corner of the alert list, click ![](https://qcloudimg.tencent-cloud.cn/raw/67593b4fea7cb1d9c5f5fd797526c5d3.png) to export the alert data in the current alert list to an Excel file.

> ?
>
> - We recommend that you select "Export data of currently displayed fields" to export the alert data in the fields displayed in the current alert list.
> - If you select "Export data of all fields", alert data is exported based on the fields displayed in the full alert list.
> - You can export the first 5,000 pieces of alert data. Please select the fields to export as needed.

#### Close alerts

If you have modified the alert status on other products, SOC will synchronize the alert status to the alert list and manage the status by setting it to the "Close" or "Open" status. You can close the analyzed and handled alerts that you no longer follow. Here are 3 methods to close alerts:

- Method 1: Select the alerts that you no longer follow, and click **Close Alert** at the top of the alert list. Once confirmed, the system will close the selected alerts. If you check the "Close similar alerts detected within past 7 days" option in the confirmation prompt box, these similar alerts will be closed together with the selected alerts.
- Method 2: Click **Close** in the Operation column of the alert list. Once confirmed, this alert will be closed. If you select the "Close similar alerts detected within past 7 days" option in the confirmation prompt box, these similar alerts will be closed together with this alert.
- Method 3: Click an **alert name** to go to the Alert Details page and then click **Close Alert** in the upper-right corner of the page. Once confirmed, this alert will be closed. If you select the "Close similar alerts detected within past 7 days" option in the confirmation prompt box, these similar alerts will be closed together with this alert.

#### View event investigation details

1. In the alert list, filter out the events that are in the **Investigation Complete** status. Click **View Details** in the Event Investigation column to go to the details page of the event.
2. On the details page, you can view the investigation details of that event, including basic information, affected assets, flow of attack techniques and tactics, details displayed by the intrusion timeline, event alerts, and event concerns.
3. In the flow of attack techniques and tactics, click the "icon button with details" to display techniques and tactics details.

#### View asset cards

In the alert list, move the pointer over any position of the alert until an icon appears next to the asset IP of this alert. Then move the pointer over the icon ![](https://qcloudimg.tencent-cloud.cn/raw/6e3d53e1e38cee83dfc1fbe14b9d056c.png) and wait a few seconds for the asset details card to pop up.

#### View event investigation details

1. In the alert list, filter out the events that are in the Investigation Complete status. Click **View Details** in the Event Investigation column to go to the details page of the event.
2. On the details page, you can view the investigation details of that event, including basic information, affected assets, flow of attack techniques and tactics, network attack correlation graph, event alerts, and event concerns. Click **Export event investigation report** to export the investigation report for that event to your local computer.
3. The network attack correlation graph shows the relationship among entities such as attack and victim IP addresses.
