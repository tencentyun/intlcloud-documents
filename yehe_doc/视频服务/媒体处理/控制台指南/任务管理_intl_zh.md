## 操作场景
当您通过上传 COS、手动发起转码、调用 API 其中的一种方式发起了媒体处理后，您发起的任务信息都可以在 [任务管理](https://console.cloud.tencent.com/mps/tasks) 中进行查看和管理。

## 操作详情
### 任务列表[](id:tlist)
![](https://qcloudimg.tencent-cloud.cn/raw/0123f31fa34d38898ba9eab19ff6ea33.png)

<table border="1">
<tr>
  <th>列名称</th>
  <th>说明</th>
</tr>
<tr>
  <td>任务 ID</td>
  <td>发起的主任务 ID</td>
</tr>
<tr>
  <td>任务状态</td>
  <td>当前的主任务状态情况，其中任务状态分为：排队中、进行中、已完成</li>
    <ul style="margin:0">
			<li><strong>排队中</strong>：该任务正在排队等待处理</li>
			<li><strong>进行中</strong>：该任务只要有一个子任务在进行中，主任务状态即为进行中</li>
			<li><strong>已完成</strong>：该任务下无进行中的子任务时，任务状态为已完成</li>
			</ul>
  </td>
</tr>
<tr>
  <td>创建时间</td>
  <td>发起该任务的时间点</td>
</tr>
<tr>
  <td>结束时间</td>
  <td>该任务的结束时间点</td>
</tr>
<tr>
  <td>操作</td>
  <td>详见下方 <a href="#tquery">任务操作</a> 描述</td>
</tr>
</table>

### 任务查询[](id:tquery)
1. 单击 [任务管理](https://console.cloud.tencent.com/mps/tasks)，进入任务管理页，该列表中展示该账号下发起的主任务记录。
2. 通过列表右上角的**任务 ID 搜索**框或者列表上**任务状态筛选**项在列表中筛选您所需要的主任务信息。


### 创建任务[](id:cquery)
1. 进入 [任务管理](https://console.cloud.tencent.com/mps/tasks) 页，单击 [创建任务](https://console.cloud.tencent.com/mps/tasks/create) 进入任务创建页面。
2. 选择需要处理的视频文件、输出路径、转码模板等信息，并发起任务。

### 任务操作[](id:operate)
任务管理中支持的任务操作有：展开详情、任务重启、任务终止、播放源视频。
- 展开详情：单击**展开详情**，会展开该主任务下的全部子任务信息。
- 重启：状态为“已完成”的任务支持重启，单击 **重启** 将重新启动执行该主任务下的全部子任务。
- 终止：状态为“排队中”的任务支持终止，单击 **终止**后，将取消任务排队并不再继续执行。
- 播放源视频：单击**播放源视频**，将获取并播放该任务的输入视频文件。

### 子任务列表[](id:slist)
任务列表中单击 **展开详情**，会展开该主任务下的全部子任务信息，子任务信息说明如下：

| 列名称     | 说明 |
| -------- | -------- |
| 子任务序号 | 该主任务下的子任务自增序号，区分不同子任务 |
| 子任务状态 | 子任务状态信息，包含：排队中、进行中、成功、失败 |
| 子任务类型 | 子任务类型信息，包含：音视频转码、截图、内容理解、审核、音视频增强等 |
| 开始时间   | 该子任务的发起时间 |
| 结束时间   | 该子任务的结束时间 |
| 输出位置   | 该子任务的输出位置（当子任务类型为内容理解、审核的时候无输出位置） |
| 操作 | 详见下方 [子任务操作](#squery) 说明 |

### 子任务操作[](id:squery)
子任务列表中支持的子任务操作有：**详情**、**播放/查看** 、下载。

| 操作名称  | 说明 |
| -------- | -------- |
| 详情      | 点击“详情”按钮，弹出子任务详情信息，可查看子任务的基础信息、模板信息、输入信息、输出信息 |
| 播放/查看 | <li>当子任务类型为“音视频转码任务”时展示“播放”按钮，点击按钮播放音频/视频</li><br/><li>当子任务类型为“截图”任务时，展示“查看”按钮，点击按钮查看图片</li> |
| 下载      | <li>单击**下载**可下载该子任务的输出文件</li><br/><li>只有子任务类型为：音视频转码、截图、音视频增强类的任务支持下载操作</li><br>**注意：当前多张截图情况支持下载第一张截图，后续计划支持打包下载** |
