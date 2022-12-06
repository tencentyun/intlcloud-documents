### Detailed resource information

In the resource list, click a **Resource name** to enter the **Resource details** page, which contains three tabs.

### Resource details

The **Resource details** tab displays the latest attribute information, JSON configuration information, and compliance evaluation result of the resource. For more information, see [Glossary](https://www.tencentcloud.com/document/product/1164/51545).
![](https://qcloudimg.tencent-cloud.cn/raw/190a40789c4e04b59929f37de391fdf2.png)

### Viewing related resources

Switch to the **Related resources** tab, where you can view the specific resources associated to the resource. For more information, see [Supported Resource Types](https://www.tencentcloud.com/document/product/1164/51495).
![](https://qcloudimg.tencent-cloud.cn/raw/c4ac8bf4ea7a3ef5a37b3550e6c864f6.png)

### Viewing the resource timeline

Switch to the **Resource timeline** tab, where you can query all the configuration change history of the resource in the last year.
![](https://qcloudimg.tencent-cloud.cn/raw/b344e8ba415502b2fd1a65321887ee96.png)

**1. Type of the time point on the timeline**
Each resource configuration change will generate a time point on the timeline. The specific configuration information at each time point is defined and displayed as a **configuration item**.
- **Start time of the timeline**
If a resource has been created before being monitored by Config, the resource timeline starts when Config first identifies and records the resource configuration information; if a resource is created after Config is activated, the timeline starts from the time of the first creation.
- **End time of the timeline**
If a resource is deleted when monitored by Config, the timeline ends at the time of deletion; otherwise, the timeline ends at the time of the last configuration change.

**2. Format of the time point on the timeline**
The configuration information at each time point on the timeline is displayed as a standard configuration item, which is a collection of attributes and configuration information of a resource at a certain time point, including metadata, attributes, relationships, and current configuration as shown below:

<table>
<thead>
<tr>
<th>Component</th>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td rowspan="5">Metadata</td>
<td>Version ID</td>
<td>Version number of Config. A new version starts from v1.0.</td>
</tr>
<tr>
<td>ConfigurationTime</td>
<td>Time when the configuration item is generated</td>
</tr>
<tr>
<td>Status</td>
<td><ul><li>`ResourceDiscovered` (the resource configuration is first discovered)</li><li>`ResourceRecorded` (the resource configuration is recorded but not first discovered)</li><li>`ResourceChanged` (the resource configuration is changed and the resource is not deleted)</li><li>`ResourceDeleted` (the resource is deleted)</li></ul></td>
</tr>
<tr>
<td>StateID</td>
<td>Configuration item ID, which is the unique key</td>
</tr>
<tr>
<td>EventType</td>
<td>Event type. Valid values:<ul><li>`Configuration` (Config generates a resource configuration event when it discovers or records a resource configuration)</li><li>`ConfigurationChange` (Config generates a configuration change event when it changes the resource configuration or deletes a resource)</li><li>`Compliance` (Config generates a compliance evaluation event when associated rules are triggered)</li></ul></td>
</tr>
<tr>
<td rowspan="10">Attribute</td>
<td>AccountId</td>
<td>UIN of the root account</td>
</tr>
<tr><td>ResourceID</td>
<td>Resource ID</td>
</tr>
<tr><td>ResourceName</td>
<td>Resource name</td>
</tr>
<tr><td>ResourceType</td>
<td>Resource type, such as `QCS::CVM::Instance`</td>
</tr>
<tr><td>ResourceType Name</td>
<td>Resource type description, such as `CVM - Instance`</td>
</tr>
<tr><td>Tags</td>
<td>Resource tag key-value pair</td>
</tr>
<tr><td>Product</td>
<td>Tencent Cloud product, such as CVM</td>
</tr>
<tr><td>QCS</td>
<td>Six-segment resource description</td>
</tr>
<tr><td>Region</td>
<td>Resource region, such as `ap-guangzhou`. It is `global` for global resources without the region attribute.</td>
</tr>
<tr>
<td>CreatedTime</td>
<td>Resource creation time</td>
</tr>
<tr>
<td rowspan="5">Relationship</td>
<td>ResourceID</td>
<td>Associated resource ID. It displays only the ID of a supported resource and is empty if there is no such ID.</td>
</tr>
<tr><td>ResourceName</td>
<td>Associated resource name</td>
</tr>
<tr><td>ResourceType</td>
<td>Associated resource type</td>
</tr>
<td>RelationshipType</td>
<td>Type of the relationship between the current resource and the associated resource</td>
</tr>
<tr>
<td>RelationshipTypeName</td>
<td>Relationship type name</td>
</tr>
<tr>
<td>Configuration</td>
Configuration
</td>
<td>_</td>
<td>Configuration details. This field varies by resource type.</td>
</tr>
<tr>
</table>

**3. Event type on the timeline**
Events fall into different types based on the information displayed in the configuration item:

- **Resource configuration event**
It indicates the first discovery or record of the resource configuration and is usually a system snapshot of a resource. It is triggered when Config is first activated or the monitored resource type is manually modified.
- **Configuration change event**
It indicates the record of a resource configuration change. If the latest resource configuration differs from the last configuration record, a resource configuration change will be displayed. Generally, this event is triggered by CloudAudit log scrape or manual or automatic resource snapshotting. If a configuration change is triggered by CloudAudit, the associated CloudAudit event will be recorded.
- **Compliance evaluation event**
It records the result of a resource configuration evaluation. For more information on the rule trigger types, see [Rule Evaluation](https://www.tencentcloud.com/document/product/1164/51523).

