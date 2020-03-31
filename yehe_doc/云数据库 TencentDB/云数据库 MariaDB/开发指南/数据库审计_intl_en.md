## Overview
### Background
You may face the following security risks when using databases, which calls for a complete post-transaction auditing and tracking mechanism. This is where database auditing comes into play.
**Administrative risks**
- Business system security risks caused by faulty, non-compliant, and unauthorized operations by system administrators. 
- Difficulty in defining accountability due to account sharing.
- Faulty and malicious operations and tampering by third-party development and maintenance personnel. 
- Excessive permissions granted to the root account, which cannot be audited and monitored.

**Technical risks**
- Backdoors or vulnerabilities of application system developers. 
- Backdoors left by former employees.

**Political risks**
- Inability to satisfy the requirements defined by China's Cybersecurity Classified Protection Certification (Level 3, 7.1.3.3).
- Inability to satisfy the requirements defined by industry-specific information security compliance documents, such as Testing and Evaluation Guide for Classified Protection of Information System of Financial Industry stipulated by PBOC.

### Terminology
**Audit policy:** a policy that defines what behaviors are to be audited and how to audit them. **Audit policy = audit object + audit rule + responsive action**. In other words, when configuring an audit policy, you need to specify the things to be audited, and if the characteristics of certain (user or system) behaviors hit an audit rule after being analyzed during the validity period of the policy, then the audit engine will take responsive actions as defined in the policy, such as sending an alarm.

**Audit rule:** a rule is a collection of behaviors that need to be audited as defined in an audit policy. A rule consists of rule parameters, each of which defines a specific characteristic for behavior matching.

### Capabilities and restrictions
TencentDB provides a database audit feature. Audit logs are retained for 15 days by default to help you perform risk management on database access and improve database security.

## Audit Operations

### Enabling database audit
You can enable database audit for TencentDB for MariaDB free of charge on the [database audit](https://console.cloud.tencent.com/tdsql/audit) page.

>Precautions on enabling audit:
- You must have at least one TencentDB for MariaDB instance which is not deactivated or isolated; otherwise, the system will automatically disable the audit feature.
- TencentDB for MariaDB instances purchased before June 5, 2016 need to be restarted and upgraded before they can support the audit feature. As this process may cause business interruption for 1–5 seconds, you can contact Tencent Cloud customer service to schedule an upgrade time.
- Database audit logs are in plaintext. Therefore, you are recommended to enable [MFA](https://intl.cloud.tencent.com/document/product/378/8392).
It takes several minutes to initialize the audit feature. Please wait patiently.


### Creating an audit rule
After the audit feature is enabled, logs will be forwarded to the audit cluster through the TencentDB for MariaDB gateway cluster. As no audit rule or policy has been created, the logs will not be recorded and displayed persistently. Therefore, you can select **Create Audit Rule** &gt; **Associate Audit Policy** to store logs in the audit cluster.

1. Go to the [audit rule](https://console.cloud.tencent.com/tdsql/audit) page and click **Create Rule**.
2. Enter the audit rule name and click **Next**.
3. Go to the parameter setting page and set the rule parameters (at least one of the listed parameters is required, but you do not need to set all of them).
 - **Logic of Rule Parameters:** the logic between each parameter in a rule is "AND", which means that the rule will only be considered a match when all parameters meet the conditions.
 - **Characteristic String:** it defines the parameter details, i.e., the specific characteristics of audit objects. To implement exact match, you only need to define keywords of the desired parameters, so that the audit system can record only custom rules to improve audit efficiency. Note: an empty string indicates that the parameter is ignored, i.e., "match all".
 - **Match Type:** relationship between parameter object and characteristic.
    - **Included:** it means the match will be successful if a characteristic string is displayed in the network field.
    - **Excluded:** it means the match will be successful if a characteristic string is not displayed in the network field.
    - **Equal to:** it means the match will be successful if the network field is equal to the characteristic string.
    - **Not equal to:** it means the match will be successful if the network field is not equal to the characteristic string.
    - **Regex:** it represents the characteristic string and supports standard regex syntax.
4. You can view all created rules in the rule list.
5. After completing audit rule settings, you can modify them at any time. You can create similar rules through **clone rule** to improve efficiency.

### Creating an audit policy
An audit policy is an audit scheme composed of audit rules, audit objects, and responsive actions. You can set multiple audit policies for one instance. When the audit engine parses policies, it will **match them in the order of configured priority from top to bottom**.
1. Select **Audit Policy** and click **Create Policy**.
2. Enter the policy requirement, select the instance to be audited based on your needs, and select the corresponding rules (alarm configuration is not supported currently).
3. Adjust the priority: you can adjust the priority of multiple policies under the same instance; the smaller the number, the higher the priority. The adjustment will take effect in 1 minute.
4. You can modify audit policies in real time by using the modification feature. Modified policies will take effect in about 5 minutes and then be used for audit and monitoring, but logs recorded prior to the modification will not be modified.

### Viewing logs
SQL statements that hit audit policies are displayed on the audit logs page. You can click them view or search. Pay attention to the following points:
- Audit logs are in plaintext. Therefore, you are recommended to enable [MFA](https://intl.cloud.tencent.com/document/product/378/8392) to ensure log security.
- Logs are recorded only after an audit policy is created. Historical data is not recorded.
- Each transaction and stored procedure may be recorded as a single statement. For more information, please see [Syntax Supported by Database Audit](https://intl.cloud.tencent.com/document/product/237/35422).
- The allowed maximum length of one SQL statement is 1 KB. Excessive content will be truncated.
