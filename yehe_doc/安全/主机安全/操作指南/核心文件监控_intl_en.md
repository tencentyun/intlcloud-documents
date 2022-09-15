This document describes how to use the Critical File Monitor feature.

## Overview
Based on Tencent Cloud's adaptive learning technology, this feature allows you to monitor critical files in real time based on system rules and custom rules. If suspicious access to a file is detected, the system will send you an alert in real time.

## Limits
The Critical File Monitor feature is available only if you have at least one server bound to a (CWPP Pro/Ultimate) license.
- Only Linux kernel 3.10 or above is supported.

## Operation Guide
1. Log in to the [CWPP console](https://console.tencentcloud.com/cwp).
2. Click **Advanced Defense** > **Critical File Monitor** on the left sidebar. The fields and operations related to the feature are described as follows.

### Event List
In the **Event List**, you can view and handle the risks related to core files (file is tampered with or files are added) that are detected by CWPP.
![](https://qcloudimg.tencent-cloud.cn/raw/6f210f4284af0f5167df3c2a4916725c.png)

Field description:
 - Server IP/Name: The server where the core file risk was detected.
 - Rule Category: System rule or custom rule.
 - Matched Rule Name: The name of the matched system rule or custom rule.
 - Event Description: A description of the core file risk.
 - **Occurrence time**: The time when the core file risk event first occurred.
 - Last Occurred: The time when the core file risk was last detected.
 - **Status**: **Pending processed**, **Allowed**, **Processed manually** and **Ignored**
 - **Operation**
   - **Details**: You can view more information about core file risks, such as process information and risk description.
   - **Actions**
     - **Mark as processed**: Please handle the risk manually by referring to "Solutions" in the event details, and then mark the event as "Handled".
     - Add to Allowlist: Once an event is added to the allowlist, no alert will be sent if the same event occurs again.  
     - Ignore: Only ignore this alert event. If the same event occurs again, an alert will be sent again.
     - Delete Record: Once deleted, the event record will no longer be displayed on the console and cannot be recovered.  

### Configure Monitoring Rules
In **Configure Monitoring Rules**, you can configure allow/alert rules for the core file access processes and add, delete, edit and check the rules.
![](https://qcloudimg.tencent-cloud.cn/raw/0e6c952bb46d36c31d1ea07e20c2c28a.png)

<dx-alert infotype="explain" title="">
System rules take effect on all servers on which CWPP Ultimate is installed. They can only be enabled or disabled, and cannot be edited or deleted.
</dx-alert>

Field description:
 - Rule Name: The name of the core file monitoring rule.
 - Rule Category
   - System Rule: System rules are configured by Tencent's CWPP operation experts and algorithm experts based on multiple models and apply to most scenarios for monitoring the tampering with users' settings.
   - Custom Rule: The rule configured by users.
 - Threat Level: High, Medium, Low, None.
 - Covered Servers: The range of servers on which a rule takes effect.
 - **Creation time**: The time when the rule was created.
 - Last Edited: The time when the rule was last edited.
 - Enabled: On/Off.
 - **Operation**
    - Copy: Copy an existing rule for editing.
    - **Edit**: Edit the range of servers on which a rule takes effect.
    - **Delete**: Delete rules.

