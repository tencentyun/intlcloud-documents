This document describes the common use cases and operations of TencentDB for SQL Server.

## 1. Basic Knowledge
If you purchase and use a TencentDB for SQL Server instance for the first time, we recommend you start with the overview and concepts of the product in the following order.
- [Product Overview](https://intl.cloud.tencent.com/document/product/238/2016)
- [Architecture](https://intl.cloud.tencent.com/document/product/238/3254)
- [Strengths](https://intl.cloud.tencent.com/document/product/238/6985)
- [Use Cases](https://intl.cloud.tencent.com/document/product/238/3248)
- [Common Concepts](https://intl.cloud.tencent.com/document/product/238/46489)
- [Regions and AZs](https://intl.cloud.tencent.com/document/product/238/7520)
- [Engines and Versions](https://www.tencentcloud.com/document/product/238/46496)
- [Features and Differences](https://intl.cloud.tencent.com/document/product/238/46495)
- [Instance Types](https://intl.cloud.tencent.com/document/product/238/46494)
- [Primary Instance Specifications](https://intl.cloud.tencent.com/document/product/238/46492)
- [Read-Only Instance Specifications](https://intl.cloud.tencent.com/document/product/238/46493)
- [Storage Types](https://intl.cloud.tencent.com/document/product/238/46490)
- [Network Environment](https://intl.cloud.tencent.com/document/product/238/32562)
- [License Statement](https://intl.cloud.tencent.com/document/product/238/6986)

Then, the use limits, specifications, and suggestions of TencentDB for SQL Server are provided to help you better use the product.
- [Constraints and Limits](https://intl.cloud.tencent.com/document/product/238/2021)
- [Usage Specifications and Suggestions](https://intl.cloud.tencent.com/document/product/238/48122)

## 2. Billing Mode
TencentDB for SQL Server adopts the **pay-as-you-go** billing mode. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/238/35798).
For more information on product billing, see the following documents:

- [Product Pricing](https://intl.cloud.tencent.com/document/product/238/8294)
- [Payment Overdue](https://intl.cloud.tencent.com/document/product/238/3117)
- [Refund](https://intl.cloud.tencent.com/document/product/238/31431)
- [Instance Adjustment Fees Description](https://intl.cloud.tencent.com/document/product/238/35799)
- [Backup Space Billing](https://intl.cloud.tencent.com/document/product/238/45849)
- [Cross-Region Backup Billing](https://www.tencentcloud.com/document/product/238/50229)
- [Viewing Bill Details](https://intl.cloud.tencent.com/document/product/238/47424)

## 3. Getting Started
### 3.1 Purchasing a TencentDB for SQL Server instance
Before using TencentDB for SQL Server, you need to sign up for a Tencent Cloud account and purchase an instance. For more information, see [Creating TencentDB for SQL Server Instance](https://intl.cloud.tencent.com/document/product/238/31571).
### 3.2 Connecting to a TencentDB for SQL Server instance
After purchasing a TencentDB for SQL Server instance, you can access the instance from a Windows or Linux CVM instance over the public network or private network. For more information, see [Instance Connection Scenarios](https://www.tencentcloud.com/document/product/238/48065).
### 3.3 Managing a TencentDB for SQL Server instance
After creating a TencentDB for SQL Server instance, you can manage the instance in the console. For more information, see [Managing TencentDB for SQL Server Instance](https://intl.cloud.tencent.com/document/product/238/35800).

## 4. Overview of Console Features
TencentDB for SQL Server provides an easy-to-use console to help you implement diversified features with ease, such as instance management, quick configuration adjustment, visual instance monitoring, and backup configuration and management. For more information, see the following documents.

<table>
<thead><tr><th>Console Feature</th><th>Documentation</th></tr></thead>
<tbody><tr>
<td>Instance management and maintenance</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/238/46508" target="_blank">Renaming Instance</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/46507" target="_blank">Setting Instance Remarks</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/46506" target="_blank">Setting Instance Tag</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/35786" target="_blank">Setting Instance Project</a></li><li><a href="https://cloud.tencent.com/document/product/238/79790" target="_blank">Modifying Instance-Level Character Set Collation</a></li><li><a href="https://cloud.tencent.com/document/product/238/79791" target="_blank">Modifying System Time Zone</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/35785" target="_blank">Setting Instance Maintenance Information</a></li><li><a href="https://cloud.tencent.com/document/product/238/43221" target="_blank">Multi-AZ Disaster Recovery</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/46505" target="_blank">Restarting Instance</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/35787" target="_blank">Terminating Instance</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/42695" target="_blank">Migrating Across AZs</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/46504" target="_blank">Recycle Bin</a></li></ul></td></tr>
<tr>
<td>Instance configuration adjustment</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/238/44352" target="_blank">Overview</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/44353" target="_blank">Adjusting Instance Architecture</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/44354" target="_blank">Adjusting Instance Version</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/35783" target="_blank">Adjusting Instance Specification</a></li></ul></td>
</tr>
<tr>
<td>Read-only instance</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/238/43142" target="_blank">Read-Only Instance Overview</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/43143" target="_blank">Managing Read-Only Instance</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/43144" target="_blank">Read-Only Group</a></li></ul></td></tr>
<tr>
<td>Network and security</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/238/46498" target="_blank">Switching from Classic Network to VPC</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/46497" target="_blank">Changing Network (from VPC to VPC)</a></li><li><a href="https://cloud.tencent.com/document/product/238/77966" target="_blank">Enabling/Disabling Public Network Address</a></li><li><a href="https://cloud.tencent.com/document/product/238/73132" target="_blank">Enabling Public Network Access Through CLB</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/35789" target="_blank">Configuring Security Group</a></li>Access management<li><a href="https://intl.cloud.tencent.com/document/product/238/34583" target="_blank">Overview</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/34584" target="_blank">Authorization Policy Syntax</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/34585" target="_blank">Authorizable Resource Types</a></li></ul></td>
</tr>
<tr>
<td>Account management</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/238/7521" target="_blank">Creating Account</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/35796" target="_blank">Resetting Password</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/35795" target="_blank">Modifying Account Permissions</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/35794" target="_blank">Deleting Account</a></li></ul></td>
</tr>
<tr>
<td>Database management</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/238/35780" target="_blank">Creating Database</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/47425" target="_blank">Setting Database Permissions</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/47426" target="_blank">Cloning Database</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/35781" target="_blank">Deleting Database</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/41608" target="_blank">Setting Change Data Capture (CDC)</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/41607" target="_blank">Setting Change Tracking (CT)</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/41606" target="_blank">Shrinking Database</a></li></ul></td>
</tr>
<tr>
<td>Parameter configuration</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/238/41609" target="_blank">Setting Instance Parameters</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/41610" target="_blank">Viewing Parameter Modification Log</a></li></ul></td>
</tr>
<tr>
<td>Monitoring and alarms</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/238/46503" target="_blank">Viewing Monitoring Charts</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/46502" target="_blank">Monitoring Metrics</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/46501" target="_blank">Setting Alarm Policies</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/46500" target="_blank">Setting Alarm Notification</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/46499" target="_blank">Viewing Alarm Records</a></li></ul></td>
</tr>
<tr>
<td>Backup and rollback</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/238/45857" target="_blank">Backup Overview</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/45855" target="_blank">Configuring Automatic Backup</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/45854" target="_blank">Creating Manual Backup</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/45853" target="_blank">Setting Backup Task</a></li><li><a href="https://cloud.tencent.com/document/product/238/75981" target="_blank">Cross-Region Backup</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/45852" target="_blank">Viewing Backup List</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/7523" target="_blank">Downloading Backup</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/45851" target="_blank">Deleting Manual Backup</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/45850" target="_blank">Viewing Backup Space</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/7522" target="_blank">Rolling back Database</a></li></ul></td>
</tr>
<tr>
<td>Log management</td>
<td><a href="https://cloud.tencent.com/document/product/238/71659" target="_blank">Querying and Downloading Slow Query Log</a></td>
</tr>
<tr>
<td>Publish/Subscribe</td>
<td><ul><li><a href="https://cloud.tencent.com/document/product/238/43326" target="_blank">Publish/Subscribe Overview</a></li><li><a href="https://cloud.tencent.com/document/product/238/43327" target="_blank">Managing Publish/Subscribe</a></li></ul></td>
</tr>
<tr>
<td>SQL Server Integration Services (SSIS)</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/238/75223" target="_blank">SSIS Overview</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/75224" target="_blank">Purchasing Business Intelligence Server</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/75225" target="_blank">Creating Windows Authentication Account</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/75226" target="_blank">Adding Flat File</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/75227" target="_blank">Interconnecting Source/Target Instances and Business Intelligence Server</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/75228" target="_blank">Deploying Project</a></li></ul></td>
</tr>
<tr>
<td>Data migration (New)</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/238/39005" target="_blank">Cold Backup Migration</a></li><li><a href="https://intl.cloud.tencent.com/document/product/238/39006" target="_blank">Migrating Data with DTS</a></li></ul></td>
</tr>
</tbody></table>

## 5. FAQs
The FAQs about the use of TencentDB for SQL Server are summarized to make it easier for you to find answers to common questions. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/238/47719).

## 6. Troubleshooting
If you encounter problems such as high CPU utilization, blockage, slow SQL, and deadlocks during your use of TencentDB for SQL Server, you can refer to [Performance/Space/Memory](https://intl.cloud.tencent.com/document/product/238/47626) for troubleshooting.

## 7. Feedback and Suggestions
If you have any questions or suggestions about TencentDB for SQL Server, you can send your feedback through the following channels, and we will get back to you accordingly:
- If you have any questions regarding the product documentation, such as links, content, or APIs, click **Send Feedback** on the right of the document page.
- If you encounter any problems while using the product, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

  

