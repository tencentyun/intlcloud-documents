
### What CAM permission rules are needed to use the plugin?

You can set `ReadOnlyAccess` (global read permission) for the account or grant the account `QcloudMonitorReadOnlyAccess` (CM's read-only permission) and "read-only permissions of each Tencent Cloud service" according to the principle of least permission.

### Does the plugin support multi-region query in the same panel?

If the `region` template variable is used in the dashboard, only single-region query is supported. To compare instances in multiple regions, you can create multiple query targets in the same panel.

### Does the plugin support comparison of multiple instances in the same region?

You can set `Multi-value` under `Selection Options` in the template variable to `true`.
![](https://qcloudimg.tencent-cloud.cn/raw/40c4ef15f5d86c7c6e6f616a78c697f3.png)
 You can select multiple instances from the drop-down list in the dashboard as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/52f6b4b6427f4167375aa161d3be2219.png)

### When I compare multiple instances, why is the error `Only queries that return single series/table is supported` reported in the panel?
![](https://main.qcloudimg.com/raw/35b75a1b7840e96df8b64940664233c7.png)

Some panel types such as `dashboard` chart only support single-instance query. If you need to compare multiple instances, use a line chart.

### The instance drop-down list in the template variable shows `InstanceId`. How do I make it show `InstanceName`?

 You can use `InstanceAlias=InstanceName` in the template variable or use the `display` attribute for splicing; for example:
  1. `Namespace=QCE/CVM&Action=DescribeInstances&Region=$region&InstanceAlias=InstanceName`
  2. `Namespace=QCE/CVM&Action=DescribeInstances&Region=$region&display=${InstanceId}-${InstanceName}`

>?If `InstanceAlias` and `display` appear at the same time, the drop-down list will only show the values of `display`.
