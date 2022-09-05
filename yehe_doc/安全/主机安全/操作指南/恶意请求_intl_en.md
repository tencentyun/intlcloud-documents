This document describes how to use the Anti-Malicious Requests feature.

## Overview
The Anti-Malicious Requests feature monitors requests sent to the external domains in real time to identify and handle the requests to malicious domains. If a request sent to a malicious domain is detected, you will receive an alert in real time.

## Limits
The Anti-Malicious Requests feature is available only if you have at least one server bound to a (CWPP Pro/Ultimate) license.

## Operation Guide
1. Log in to the [CWPP console](https://console.intl.cloud.tencent.com/cwp).
2. Click **Intrusion Detection** > **Anti-Malicious Requests** on the left sidebar. The fields and operations related to the feature are descibed as follows.

### Event List
In the **Event List**, you can view and handle the requests sent to malicious domains that are detected by CWPP.
![](https://qcloudimg.tencent-cloud.cn/raw/f199ad4c197b594c9d7121fb6a8637db.png)
Field description:
- **Server IP/Name**: The server which sent a request to a malicious domain.
- Malicious Domain: The malicious domain to which a request was sent.
- No. of Requests: The number of the requests sent to the malicious domain.
- **Process**: Only supported for Windows system.
- **Description**: The risk description of the malicious domain.
- **Last requested**: The time when the last request was sent to the malicious domain.
- **Status**: **Pending processed**, **Added to allowlist**, **Processed** and **Ignored**
- **Operation**
  - **Details**: You can view more information about the request to the malicious domain, such as process information, command lines, and risk description.
  - **Actions**
    - **Mark as processed**: Please handle the risk manually by referring to "Solutions" in the event details, and then mark the event as "Handled".
    - **Add to Allowlist**: Once an event is added to the allowlist, no alert will be sent if the same event occurs again. 
    - **Ignore**: Only ignore this alert event. If the same event occurs again, an alert will be sent again.
    - Delete Record: Once deleted, the event record will no longer be displayed on the console and cannot be recovered.  

### Allowlist Management
In **Allowlist Management**, you can add/delete items to/from the allowlist, or edit and check the allowlist.
![](https://qcloudimg.tencent-cloud.cn/raw/63023a83581d977ea5e47ee6f5dc1ca8.png)
Field description:
- Allowed Domain Name: It can be an exact domain name or a wildcard domain name. When a request to this domain is detected, no event alert is generated.
- Remarks: Remarks for the allowlist.
- **Creation time**: The time when the allowlist was created.
- **Update time**: The time when the allowlist was last updated.
- **Operation**
   - **Edit**: Edit the allowed domain names and remarks.
   - **Delete**: Delete items from the allowlist.

<dx-alert infotype="explain" title="">
The allowlist takes effect on all servers (Pro/Ultimate).
</dx-alert>

