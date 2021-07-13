<dx-alert infotype="explain" title="">
云函数 SCF 于2021年01月29日起全量接入腾讯云 [日志服务 CLS](intl.tencent.com/document/product/614)，在此之后创建的函数调用日志将默认投递至 CLS，且支持日志实时输出。若您的函数于2021年01月29日前创建，且需进行日志检索与日志投递，请参考本文档使用该功能。
</dx-alert>

## 操作场景

在使用云函数 SCF 进行函数计算时，会产生大量的函数运行日志，如果您需要将日志进行持久化存储、投递或消费，对日志内容进行监控告警，您可将日志投递到腾讯云日志服务 CLS 平台。如下图所示：
![](https://main.qcloudimg.com/raw/ca4e6aefa5b78812d98ea8baaac25238.png)


## 前提条件

在使用云函数实时日志服务功能之前，需开通 [日志服务](https://intl.cloud.tencent.com/product/cls)。


## 操作步骤

### 创建日志集和日志主题

登录 [日志服务控制台](https://console.cloud.tencent.com/cls) 并 [创建日志集和日志主题](https://intl.cloud.tencent.com/document/product/614/31592)。本文以在广州创建 `SCF-test` 日志集和日志主题为例。如下图所示：

>!日志集地域请选择函数服务所在地域，暂不支持跨地域日志推送。
>
>![](https://main.qcloudimg.com/raw/372b2b2c57ca6f22181d923889f7d8ca.png)

### 配置日志服务

1. 登录云函数控制台，选择左侧导航栏中的【[函数服务](https://console.cloud.tencent.com/scf/list)】。
2. 在页面上方选择函数所在地域及命名空间，并在列表中单击需实时采集日志的函数名。
3. 在“函数配置”页面，单击右上角的【编辑】。如下图所示：
      ![](https://main.qcloudimg.com/raw/6b74418e46923017c70cdd7a829d650d.png)
4. 在“日志投递”中，勾选“启用”并选择已为该函数创建的日志集和日志主题，本文以 `SCF-test` 为例。如下图所示：
      ![](https://main.qcloudimg.com/raw/3a51957107ea5152ce9f17c66cda461d.png)
5. 单击【保存】即可成功接入日志服务平台。

### 开启索引

>?日志检索依赖日志主题的索引配置，函数关联日志主题后，SCF 自动为日志主题配置索引。如仍遇索引异常导致日志拉取失败，请参考此步骤调整索引配置。






1. 登录日志服务控制台，选择左侧导航栏中的【[日志集管理](https://console.cloud.tencent.com/cls/logset)】。
2. 单击已创建的日志集 ID，进入“基本信息”页面。
3. 选择日志主题所在行右侧的【管理】，进入日志主题“基本信息”页面。
4. 在日志主题“基本信息”页面，单击【索引配置】。如下图所示：
      ![](https://main.qcloudimg.com/raw/49bd80b80664830aac2f03a0b444bbb8.png)
5. 单击右上角的【编辑】，开启“键值索引”后按照下表添加“字段名称”、“字段类型”。
 >? 对于配置了日志服务的函数，为保证云函数控制台日志展示效果，请在键值索引配置中为字段打开“开启统计”能力。如下图所示：
 >![](https://main.qcloudimg.com/raw/989273eed3d2405f59cc35ff648b8422.png)

<table>
<thead>
<tr>
<th>字段名称</th>
<th>字段类型</th>
<th>字段含义</th>
</tr>
</thead>
<tbody><tr>
<td>SCF_FunctionName</td>
<td>text</td>
<td>函数名称。</td>
</tr>
<tr>
<td>SCF_Namespace</td>
<td>text</td>
<td>函数所在命名空间。</td>
</tr>
<tr>
<td>SCF_StartTime</td>
<td>long</td>
<td>调用开始时间。</td>
</tr>
<tr>
<td>SCF_LogTime</td>
<td>long</td>
<td>日志产生时间。</td>
</tr>
<tr>
<td>SCF_RequestId</td>
<td>text</td>
<td>请求 ID。</td>
</tr>
<tr>
<td>SCF_Duration</td>
<td>long</td>
<td>函数运行时间。</td>
</tr>
<tr>
<td>SCF_Alias</td>
<td>text</td>
<td>别名。</td>
</tr>
<tr>
<td>SCF_Qualifier</td>
<td>text</td>
<td>版本。</td>
</tr>
<tr>
<td>SCF_MemUsage</td>
<td>double</td>
<td>函数运行内存。</td>
</tr>
<tr>
<td>SCF_Level</td>
<td>text</td>
<td>Log4J 日志级别，默认为 INFO。</td>
</tr>
<tr>
<td>SCF_Message</td>
<td>text</td>
<td>日志内容。</td>
</tr>
<tr>
<td>SCF_Type</td>
<td>text</td>
<td>日志类型，Platform 指平台日志，Custom 指用户日志。</td>
</tr>
<tr>
<td>SCF_StatusCode</td>
<td>long</td>
<td>函数运行 <a href="https://intl.cloud.tencent.com/document/product/583/35311">状态码</a>。</td>
</tr>
<tr>
<td>SCF_RetryNum</td>
<td>long</td>
<td>重试次数。</td>
</tr>
</tbody></table>


如需使用更多功能，例如日志实时检索、日志投递和消费等，请参考 [日志服务文档](https://intl.cloud.tencent.com/document/product/614) 并前往 [日志服务控制台](https://console.cloud.tencent.com/cls) 开始使用。


### 实时检索示例

>?在使用实时检索功能前，请确保您的函数服务日志已接入日志服务平台，并且需检索的日志主题已开启索引。

1. 登录日志服务控制台，选择左侧导航栏中的【[检索分析](https://console.cloud.tencent.com/cls/search)】。
2. 在“检索分析”页面选择需检索的日志主题和时间，并在输入框中填写检索语法，本文以 `START` 为例。
   检索语法支持关键词检索、模糊检索、范围检索等方式，详情请参考 [日志服务语法与规则](https://intl.cloud.tencent.com/document/product/614/37882)。
3. 单击【检索分析】即可查看实时日志信息。

