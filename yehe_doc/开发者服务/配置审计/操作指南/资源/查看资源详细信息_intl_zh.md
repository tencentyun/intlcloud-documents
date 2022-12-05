###  资源详情信息

在资源列表，单击资源名称，可查看**资源详情**信息，该页面有三个子页面。

###  资源详情

资源详情展示资源最新更新的属性信息、配置信息json、资源的最新合规评估结果。具体请查阅[词汇表](https://www.tencentcloud.com/document/product/1164/51545)。
![](https://qcloudimg.tencent-cloud.cn/raw/190a40789c4e04b59929f37de391fdf2.png)

###  查看相关资源

切换到**相关资源**页面，可查看当前资源关联的具体资源。具体配置审计支持的资源关系请查阅 [支持的资源类型](https://www.tencentcloud.com/document/product/1164/51495)。
![](https://qcloudimg.tencent-cloud.cn/raw/c4ac8bf4ea7a3ef5a37b3550e6c864f6.png)

###  查看资源时间线

切换至**资源时间线**页面，可以查询仅一年内该资源的所有配置变更历史记录。
![](https://qcloudimg.tencent-cloud.cn/raw/b344e8ba415502b2fd1a65321887ee96.png)

**1、时间线中节点的类别**
资源每一次的配置变更将对应生成一个时间线的节点，每一节点的具体配置信息通过**配置项（ConfigurationItem）**来定义和展示。
- **时间线的起点**
如您的资源在被配置审计监控前已创建，则资源时间线的起点为配置审计首次识别并记录该资源配置信息的时间；如您的资源为开启配置审计监控后创建，则时间线的起点为资源首次创建的时间。
- **时间线的终点**
如该资源在配置审计监控期间被删除，则终点为资源删除的时间，如未删除，则终点为最近一次配置变更的时间。

**2、时间线中节点的格式**
时间线中每一节点的配置信息通过标准的配置项（ConfigurationItem）来展示。配置项指某一时间点资源的各类属性、配置信息的集合，由元数据（Metadata）、资源属性（Attribute）、关联资源（Relationship）、详细配置信息（Configuration）组成。具体如下：

<table>
<thead>
<tr>
<th>组成部分</th>
<th>字段名称</th>
<th>字段说明</th>
</tr>
</thead>
<tbody><tr>
<td rowspan="5">基本信息 Metadata</td>
<td>Version ID</td>
<td>Config 版本号，新版本从1.0开始</td>
</tr>
<tr>
<td>ConfigurationTime</td>
<td>该配置项生成的时间</td>
</tr>
<tr>
<td>Status</td>
<td><ul><li>ResourceDiscovered （资源配置首次发现）</li><li>ResourceRecorded （资源配置记录，非首次发现)</li><li>ResourceChanged （资源配置变更，且资源未删除）</li><li>ResourceDeleted（该资源被删除）</li></ul></td>
</tr>
<tr>
<td>StateID</td>
<td>配置项id，配置项的唯一键</td>
</tr>
<tr>
<td>EventType</td>
<td>事件类型：<ul><li>Configuration（当资源配置发现或记录时，配置审计生成资源配置事件）</li><li>ConfigurationChange（当资源配置变更或资源被删除时，配置审计生成配置变更事件）</li><li>Compliance（当触发了资源关联规则的评估时，配置审计生成合规评估事件）</li></ul></td>
</tr>
<tr>
<td rowspan="10">资源属性Attribute</td>
<td>AccountId</td>
<td>主账号uin</td>
</tr>
<tr><td>ResourceID</td>
<td>资源ID</td>
</tr>
<tr><td>ResourceName</td>
<td>资源名称</td>
</tr>
<tr><td>ResourceType</td>
<td>资源类型，如QCS::CVM::Instance</td>
</tr>
<tr><td>ResourceType Name</td>
<td>资源类型描述，如云服务器-实例</td>
</tr>
<tr><td>Tags</td>
<td>资源标签键对值</td>
</tr>
<tr><td>Product</td>
<td>云产品，如cvm等</td>
</tr>
<tr><td>QCS</td>
<td>资源六段式</td>
</tr>
<tr><td>Region</td>
<td>地域名称，指资源地域名称，比如ap-guangzhou 对于无地域属性的全局资源，region取global</td>
</tr>
<tr>
<td>CreatedTime</td>
<td>资源创建时间</td>
</tr>
<tr>
<td rowspan="5">关联资源Relationship</td>
<td>ResourceID</td>
<td>关联资源id，仅展示当前config支持的资源类型范围内的资源id，没有则置空</td>
</tr>
<tr><td>ResourceName</td>
<td>关联资源名称</td>
</tr>
<tr><td>ResourceType</td>
<td>关联资源类型</td>
</tr>
<td>RelationshipType</td>
<td>当前资源与关联资源的关系类型</td>
</tr>
<tr>
<td>RelationshipTypeName</td>
<td>关系类型名称</td>
</tr>
<tr>
<td>配置信息
Configuration
</td>
<td>_</td>
<td>详细配置信息，每一资源类型的个性化配置信息字段不同</td>
</tr>
<tr>
</table>

**3、时间线中的事件类别**
根据事件配置项中展示信息的不同，可将每一节点分为以下几类：

- **资源配置事件**
指对资源配置的首次发现或记录，一般来自对系统对资源的快照。由用户首次开启配置审计服务、手动修改监控的资源类型时触发。
- **配置变更事件**
指对资源配置变更的记录。如您资源的最新配置与上一次记录的配置存在差异，则节点会展示为资源配置变更。一般由云审计日志触发抓取或手动、自动执行的资源快照触发。如配置变更由云审计触发，则会相应记录关联的云审计事件。
- **合规评估事件**
指对资源配置评估结果的记录，规则触发机制可参阅[规则评估](https://www.tencentcloud.com/document/product/1164/51523)。

