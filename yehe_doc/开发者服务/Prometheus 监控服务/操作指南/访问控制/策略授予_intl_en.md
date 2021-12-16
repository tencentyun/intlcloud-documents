## Custom Policy for TMP

If preset policies cannot meet your needs, you can click **Create Custom Policy** to create custom policies.

![](https://qcloudimg.tencent-cloud.cn/raw/54fe223a7b70c16fe5c2931404d0d4bf.png)

For the method of custom policy creation, please see Setting Policy.

## Policy Authorization

A configured policy can grant permissions by associating user groups or sub-users.

![](https://qcloudimg.tencent-cloud.cn/raw/26b5e8ab2aaf512581efa457790b8692.png)

## Resource Types Authorizable by Custom Policy

Resource-Level permission can be used to specify which resources a user can manipulate. TMP supports certain resource-level permissions. This means that for TMP operations that support resource-level permission, you can control the time when a user is allowed to perform operations or to use specified resources. The following table describes the types of resources that can be authorized in CAM.

| Resource Type | Resource Description Method in Authorization Policy |
| ---------- | ------------------------------------------------------------ |
| TMP | `qcs::monitor:$region:$account:prom-instance/*`<br>`qcs::monitor:$region:$account:prom-instance/$instanceId` |

The following table describes the TMP API operations that currently support resource-level permissions. When setting a policy, you can enter the API operation name in the `action` field to control the individual API. You can also use `*` as a wildcard to set the `action`.

#### List of APIs supporting resource-level authorization

| API Operation | API Description |
| ------------------------------------ | -------------------------- |
| DescribePrometheusInstances | Lists all TMP instances of the user |
| TerminatePrometheusInstances | Terminates TMP instance |
| RecreatePrometheusInstance | Reboots TMP instance |
| ModifyPrometheusInstanceAttributes | Modifies TMP instance attributes |
| ChangeGrafanaAdminPassword | Changes Grafana admin Password |
| UpgradeGrafanaDashboard | Upgrades Grafana dashboard |
| DescribePrometheusKubeClusters | Lists TKE clusters that can be integrated with TMP |
| InstallPrometheusAgent | Installs Prometheus agent |
| UninstallPrometheusAgent | Uninstalls Prometheus agent |
| DescribeServiceDiscovery | Lists TMP scrape configurations |
| CreateServiceDiscovery | Creates TMP scrape configuration |
| UpdateServiceDiscovery | Updates TMP scrape configuration |
| DeleteServiceDiscovery | Deletes TMP scrape configuration |
| DescribePrometheusKubeBasicMonitor | Queries basic monitoring status |
| EnablePrometheusKubeBasicMonitor | Enables basic monitoring |
| DisablePrometheusKubeBasicMonitor | Disables basic monitoring |
| DescribePrometheusAgentRuntime | Gets the runtime status of Prometheus agent |
| DescribePrometheusJobTargets | Lists the status information of TMP metric scrape tasks |
| DescribeRecordingRules | Queries recording rules |
| CreateRecordingRule | Creates recording rule |
| UpdateRecordingRule | Updates recording rule |
| DeleteRecordingRules | Deletes recording rule |
| DescribeAlertRules | Queries alarming rules |
| DeleteAlertRules | Deletes alarming rule |
| UpdateAlertRuleState | Updates alarming rule status |
| CreateAlertRule | Creates alarming rule |
| UpdateAlertRule | Updates alarming rule |

#### List of APIs not supporting resource-level authorization

For TMP API operations that don't support resource-level authorization, you can still authorize a user to perform them, but you must specify `*` as the resource element in the policy statement.

| API Operation | API Description |
| --------------------------- | --------------------   |
| CreatePrometheusInstance | Creates TMP instance |
