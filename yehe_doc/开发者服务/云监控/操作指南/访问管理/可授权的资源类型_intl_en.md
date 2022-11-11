## Resource Types Authorizable by Custom Policy

Resource-level permission can be used to specify which resources a user can manipulate. Cloud Monitor alarm policies and notification templates support resource-level permission, that is, for operations that support resource-level permission, you can control the time when a user is allowed to perform operations or use specific resources. The table below describes the types of resources that can be authorized in CAM.

| Resource Type | Resource Description Method in Authorization Policy |
| :----------------- | :----------------------------------------- |
| Alarm policy/cm-policy | `qcs::monitor::uin/:cm-policy/${policyId}` |
| Notification template/cm-notice | `qcs::monitor::uin/:cm-notice/${noticeId}` |

The table below describes the alarm policy and notification template API operations that currently support resource-level permission. When setting a policy, you can enter the API operation name in the `action` field to control the individual API. You can also use `*` as a wildcard to set the `action`.

### List of APIs supporting resource-level authorization

| API Name | API Description |
| :------------------------- | :-------------------- |
| DeleteAlarmPolicy          | Deletes an Alarm 2.0 policy       |
| ModifyAlarmPolicyCondition | Edits the trigger condition of an alarm policy  |
| ModifyAlarmPolicyInfo      | Edits the basic information of an alarm policy  |
| ModifyAlarmPolicyNotice    | Edits notifications for an Alarm 2.0 policy |
| ModifyAlarmPolicyStatus    | Modifies the alarm policy status      |
| ModifyAlarmPolicyTasks     | Edits the alarm policy trigger task  |
| SetDefaultAlarmPolicy      | Sets the default alarm policy      |
| DeleteAlarmNotices         | Deletes alarm notifications          |
| ModifyAlarmNotice          | Edits alarm notifications          |
| ModifyAlarmPolicyNotice    | Edits notifications for an Alarm 2.0 policy |
| DescribeAlarmPolicies      | Displays the Alarm 2.0 policy list       |
| DescribeAlarmPolicyQuota   | Queries the alarm policy quota      |
| DescribeAlarmNotice        | Queries the alarm notification details      |
| DescribeAlarmNotices       | Queries the alarm notification list      |

