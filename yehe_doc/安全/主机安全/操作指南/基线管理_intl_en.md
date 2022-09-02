This document describes how to use the Baseline Management to ensure baseline security for servers.
## Overview
Tencent Cloud CWPP (Cloud Workload Protection Platform) allows you to perform periodic and quick baseline checks on servers based on default or custom baseline policies. You can also specify check items and servers to be included in baseline policies. By providing information such as baseline check pass rates, detected risks, threat levels, and suggestions on how to fix the vulnerabilities, the product helps you better manage the baseline security of your servers.

## Important Notes
- The Baseline Management feature is available only if you have at least one server bound to a (**CWPP Pro/Ultimate**) license.
- Supported baseline types for check

| Baseline Type | Supported Baselines for Check |
|---------|---------|
| Unauthorized access | Unauthorized access to CouchDB<br>Unauthorized access to Elasticsearch<br>unauthorized access to MongoDB<br>unauthorized access to Hadoop<br>unauthorized access to Kubelet<br>Redis baseline compliance check<br>unauthorized access to ZooKeeper<br> |
| Weak passwords | Linux system weak passwords<br>MySQL weak passwords<br>Windows system weak passwords<br>Linux system weak passwords<br>Rsync weak passwords<br>Linux account with empty password<br>Access to Rsync without a password<br>Xampp default FTP password<br>ActiveMQ baseline compliance check |
| Remote code execution | JavaRMI remote code execution<br>Jenkins without authentication causes execution of arbitrary commands |
| Tencent Cloud security standards | MongoDB security baseline check<br>Linux security baseline check<br>Windows security baseline check<br>FTP security baseline check<br>Nginx security baseline check<br>Information leakage baseline check|
| Other | NFS misconfiguration causes mounting of sensitive directories<br>PHP-FPM misconfiguration<br>Docker daemon port (2375) is open<br>Detection of Tomcat example directories<br>Memcached's UDP port exploited by DDoS amplification attacks<br>IIS misconfiguration causes resolution vulnerability<br>RPCBind misconfiguration<br>CentOS baseline check|




## Operation Guide
1. Log in to the [CWPP console](https://console.tencentcloud.com/cwp).
2. Click **Baseline Management** on the left sidebar. The fields and operations related to the feature are described as follows.

### Baseline policies
A baseline policy is a collection of user-defined baseline check items, allowing you to track baseline pass rates and detected risks based on the dimensions included in the policy.
- **Tencent Cloud default baseline policies**: Tencent Cloud CWPP provides default baseline policies based on mainstream network security baseline check items, including: weak password policy, CIS baseline policy, and Tencent Cloud best security practice policy. You can add check items and servers to be checked to a default baseline policy, under which the check is conducted once every 7 days by default (at 00:00 of the day).
>? Pass rate of policy = the number of servers that pass all check items under this policy/the number of all servers checked under this policy

![](https://qcloudimg.tencent-cloud.cn/raw/8ebef1a2a9b0b3e351788bfa5f3f1000.png)
- **Add Baseline Policies**
	1. Click **Baseline Settings** in the upper right corner of the baseline check result section.
	2. In the "Baseline Policy Settings" section of the "Baseline Settings" page, click **Add Policies**.
![](https://qcloudimg.tencent-cloud.cn/raw/e143e2b4d2dadd5667b7f431db4ff0a6.png)
	3. Enter the name of the new policy (must be different from existing policy names), specify Interval, Baseline Types, and Target Assets in the "Add Policies" page, and then click "Save and update".

<dx-alert infotype="explain" title="">
A maximum of 20 baseline policies. If this limit is reached, you must delete an existing policy before you can create a new one.
</dx-alert>

### Quick Check
Select the baseline policies for your check, click **Quick Check** (The check generally takes 2-10 minutes).

### Periodic Check
1. Click **Baseline Settings** in the upper right corner of the baseline check result section.
2. You can set the interval of periodic checks and manage ignored check items
![](https://qcloudimg.tencent-cloud.cn/raw/072a289099a4dce158743bc680e8ccbf.png)


### Visualized baseline data
After selecting baseline policies and running a check, the [Baseline Management](https://intl.cloud.tencent.com/document/product/296/45862) page shows the number of checked servers, number of check items, the pass rate of the baseline policies, top 5 baseline check items, and top 5 risk items, which are categorized by threat level.


#### Baseline check result list
At the bottom of the [Baseline Management](https://intl.cloud.tencent.com/document/product/296/45862) page, the list of baseline check results is shown, where you can view baseline details, perform fuzzy search and status filtering for a single baseline, and download all tables.
![](https://qcloudimg.tencent-cloud.cn/raw/908da62a47ac5721f65f8882e3c18c3f.png)

Field description:

- Baseline Name: The name of the current baseline set, which contains multiple check items of the same category.
- Threat Level: Divided into Severe, High, Medium, and Low
- Baseline Check Items: The total number of check items included in the current baseline set.
- **Affected servers**: The number of servers that do not pass every check item in the current baseline set under the baseline policy, i.e. the number of servers affected by this baseline set.
- Last Checked: The time when the check items in the baseline set were last executed on a server.
- **Status**: Pass, Fail and In Progress.
- **Opereation**: Allows you to view baseline details and run a recheck for failed baselines.
	- **Rescan**:
		- Option 1: Select the baselines for a recheck, and click **Recheck** in the upper left corner of the list to run a recheck for the selected baselines at one time.
		- Option 2: Click **Recheck** on the right of the desired baseline to run a recheck for the baseline.
	- View details:
	 - In the baseline check result list, locate the desired baseline, and then click **Details** in the Action column on the right to open the baseline details page.
	 - The baseline details page shows the description and threat level of the baseline, as well as the list of affected servers.
		![](https://qcloudimg.tencent-cloud.cn/raw/5eca48d5d7ff1b44ab9060074851359e.png)
 - The check details page shows the basic information including baseline name, server name, and check items.
		![](https://qcloudimg.tencent-cloud.cn/raw/97129205f6845ec9204000e347ef336f.png)

	- You can run a "Recheck" or select "Ignore" for multiple check items.
	- You can filter check items by threat level or status.
	- When you hover the mouse cursor over a check item, the details of the item, and solutions to the detected issue will appear.

