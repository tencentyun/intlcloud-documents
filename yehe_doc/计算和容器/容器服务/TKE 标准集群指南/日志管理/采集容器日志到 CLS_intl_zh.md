本文将介绍如何在容器服务控制台配置日志采集规则并投递到 [腾讯云日志服务 CLS](https://www.tencentcloud.com/zh/products/cls)。

## 操作步骤
### 创建日志采集规则

1. 登录 [容器服务控制台](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的**运维中心** > **日志规则**。
2. 在“日志规则”页面上方选择地域和需要配置日志采集规则的集群，单击**新建**。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/AMJP139_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221226153528.png)
3. 在“新建日志采集规则”页面中配置日志服务消费端，在**消费端 > 类型**中选择 **CLS**。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/zCY5744_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221226153647.png)
  - 收集规则名称：您可以自定义日志收集规则名称。
  - 日志所在地域：CLS 支持跨地域日志投递，您可通过单击“修改”选择日志投递的目标地域。
  - 日志集：根据日志所在地域展示您已经创建的日志集，若现有日志集不合适，您可以在 [日志服务控制台](https://console.cloud.tencent.com/cls) 新建日志集。操作详情见 [创建日志集](https://intl.cloud.tencent.com/document/product/614/34238)。
  - 日志主题：选择日志集下对应的日志主题，支持“自动创建”和“选择已有”日志主题两种模式。
  - 高级设置：
     - 默认元数据：CLS 默认将元数据 `pod_name`、`namespace`、`container_name` 设为索引用于日志检索。
     - 自定义元数据：支持自定义元数据及日志索引。
>?
>- CLS 不支持国内和海外地域之间跨地域日志投递；针对 CLS 未开通日志服务的地域仅支持就近投递，如深圳集群采集的容器日志仅支持投递到广州，天津集群采集的容器日志仅支持投递到北京；详情可通过控制台查看。
>- 一个日志主题目前仅支持配置一类日志，即日志、审计、事件不可采用同一个 topic，会产生覆盖情况，请确保所选日志主题没有被其他采集配置占用；若日志集下已存在500个日志主题，则不能新建日志主题。
>- 自定义元数据和基于元数据开启索引创建后不能修改，您可前往 [日志服务控制台](https://console.cloud.tencent.com/cls) 修改。
>
4. 选择采集类型并配置日志源，目前采集类型支持**容器标准输出**[](id:stout)、**容器文件路径**[](id:insideDocker)和**节点文件路径**[](id:inside)。
<dx-tabs>
::: 容器标准输出日志
日志源支持**所有容器**、**指定工作负载**、**指定 Pod Lables** 三种类型。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/RXIn726_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221226154431.png)
![](https://staticintl.cloudcachetci.com/yehe/backend-news/XpPd027_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221226154553.png)
![](https://staticintl.cloudcachetci.com/yehe/backend-news/QhCS274_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221226154637.png)

:::
::: 容器内文件日志 
- 日志源支持**指定工作负载**、**指定Pod Lables** 两种类型。
- 采集文件路径支持文件路径和通配规则，例如当容器文件路径为 `/opt/logs/*.log`，可以指定采集路径为 `/opt/logs`，文件名为 `*.log`。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/HV7r317_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221226154816.png)
![](https://staticintl.cloudcachetci.com/yehe/backend-news/M2z4825_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221226154907.png)
<dx-alert infotype="notice" title="">
“容器文件路径” <b>不能为软链接</b>，否则会导致软链接的实际路径在采集器的容器内不存在，采集日志失败。
</dx-alert>

:::
::: 节点文件日志
- 采集路径支持以文件路径和通配规则的方式填写，例如当需要采集所有文件路径形式为 `/opt/logs/service1/*.log`，`/opt/logs/service2/*.log`，可以指定采集路径的文件夹为 `/opt/logs/service*`，文件名为 `*.log`。
- 您可根据实际需求自定义添加 Key-Value 形式的 “metadata” ，metadata 将会添加到日志记录中。
![](https://main.qcloudimg.com/raw/7c5c8341315408c5668add566a3ff550.png)
<dx-alert infotype="explain" title="">
一个节点日志文件只能被一个日志主题采集。
</dx-alert>
:::
</dx-tabs>
<dx-alert infotype="explain" title="">
对于“容器的标准输出”及“容器内文件”（不包含“节点文件路径”即 hostPath 挂载），除了原始的日志内容， 还会带上容器或 kubernetes 相关的元数据（例如：产生日志的容器 ID）一起上报到 CLS，方便用户查看日志时追溯来源或根据容器标识、特征（例如：容器名、labels）进行检索。
容器或 kubernetes 相关的元数据请参考下方表格：
<table>
	<tr>
		<th>字段名</th> <th>含义</th>
	</tr>
	<tr>
		<td>container_id</td> <td>日志所属的容器 ID。</td>
	</tr>
	<tr>
		<td>container_name</td> <td>日志所属的容器名称。</td>
	</tr>
	<tr>
		<td>image_name</td> <td>日志所属容器的镜像名称 IP。</td>
	</tr>
	<tr>
		<td>namespace</td> <td>日志所属 pod 的 namespace。</td>
	</tr>
	<tr>
		<td>pod_uid</td> <td>日志所属 pod 的 UID。</td>
	</tr>
	<tr>
		<td>pod_name</td> <td>日志所属 pod 的名字。</td>
	</tr>
	<tr>
		<td>pod_lable_{label name}</td> <td>日志所属 pod 的 label（例如一个 pod 带有两个 label：app=nginx，env=prod，
则在上传的日志会附带两个 metedata：pod_label_app:nginx，pod_label_env:prod）。
</td>
	</tr>
</table>

</dx-alert>
5. 配置采集策略。您可以选择**全量**或者**增量**。
	- 全量：全量采集指从日志文件的开头开始采集。
	- 增量：增量采集指从距离文件末尾1M处开始采集（若日志文件小于1M，等价于全量采集）。
6. 单击**下一步**，选择日志解析方式。如下图所示：
    ![](https://staticintl.cloudcachetci.com/yehe/backend-news/KL5a497_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221226155828.png)

  - 编码模式：支持**UTF-8**和**GBK**。
  - 提取模式：支持多种类型的提取模式，详情如下：
  <table>
  <thead>
  <tr>
  <th>解析模式</th>
  <th>说明</th>
  <th>相关文档</th>
  </tr>
  </thead>
  <tbody><tr>
  <td>单行全文</td>
  <td>一条日志仅包含一行的内容，以换行符 \n 作为一条日志的结束标记，每条日志将被解析为键值为 <strong>CONTENT</strong> 的一行完全字符串，开启索引后可通过全文检索搜索日志内容。日志时间以采集时间为准。</td>
  <td><a href="https://intl.cloud.tencent.com/document/product/614/32287">单行全文格式</a></td>
  </tr>
  <tr>
  <td>多行全文</td>
  <td>指一条完整的日志跨占多行，采用首行正则的方式进行匹配，当某行日志匹配上预先设置的正则表达式，就认为是一条日志的开头，而下一个行首出现作为该条日志的结束标识符，也会设置一个默认的键值 <strong>CONTENT</strong>，日志时间以采集时间为准。支持自动生成正则表达式。</td>
  <td><a href="https://intl.cloud.tencent.com/document/product/614/32284">多行全文格式</a></td>
  </tr>
  <tr>
  <td>单行 - 完全正则</td>
  <td>指将一条完整日志按正则方式提取多个 key-value 的日志解析模式，您需先输入日志样例，其次输入自定义正则表达式，系统将根据正则表达式里的捕获组提取对应的 key-value。支持自动生成正则表达式。</td>
  <td><a href="https://intl.cloud.tencent.com/document/product/614/39589">单行 - 完全正则格式</a></td>
  </tr>
  <tr>
  <td>多行 - 完全正则</td>
  <td>适用于日志文本中一条完整的日志数据跨占多行（例如 Java 程序日志），可按正则表达式提取为多个 key-value 键值的日志解析模式，您需先输入日志样例，其次输入自定义正则表达式，系统将根据正则表达式里的捕获组提取对应的 key-value。支持自动生成正则表达式。</td>
  <td><a href="https://intl.cloud.tencent.com/document/product/614/39590">多行-完全正则格式</a></td>
  </tr>
  <tr>
  <td>JSON</td>
  <td>JSON 格式日志会自动提取首层的 key 作为对应字段名，首层的 value 作为对应的字段值，以该方式将整条日志进行结构化处理，每条完整的日志以换行符 \n 为结束标识符。</td>
  <td><a href="https://intl.cloud.tencent.com/document/product/614/32286">JSON 格式</a></td>
  </tr>
  <tr>
  <td>分隔符</td>
  <td>指一条日志数据可以根据指定的分隔符将整条日志进行结构化处理，每条完整的日志以换行符 \n 为结束标识符。日志服务在进行分隔符格式日志处理时，您需要为每个分开的字段定义唯一的 key，无效字段即无需采集的字段可填空，不支持所有字段均为空。</td>
  <td><a href="https://intl.cloud.tencent.com/document/product/614/32285">分隔符格式</a></td>
  </tr>
  </tbody></table>
  - 过滤器：LogListener 仅采集符合过滤器规则的日志，Key 支持完全匹配，过滤规则支持正则匹配，如仅采集 `ErrorCode = 404` 的日志。您可以根据需求开启过滤器并配置规则。
    <dx-alert infotype="explain" title="">
    一个日志主题目前仅支持一个采集配置，请保证选用该日志主题的所有容器的日志都可以接受采用所选的日志解析方式。若在同一日志主题下新建了不同的采集配置，旧的采集配置会被覆盖。
    </dx-alert>
7. 单击**完成**，完成投递到 CLS 的容器日志采集规则创建。 

### 更新日志规则
1. 登录 [容器服务控制台](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的**日志管理** > **日志规则**。
2. 在“日志规则”页面上方选择地域和需要更新日志采集规则的集群，单击右侧的**编辑收集规则**。如下图所示：
![](https://main.qcloudimg.com/raw/31dad4c82bdb27197873b5141dcfa3b0.png)
3. 根据需求更新相应配置，单击**完成**。
>! 日志集和日志主题不可更新。

## 相关文档
您不仅可以使用控制台配置日志采集，还可以通过自定义资源（CustomResourceDefinitions，CRD）的方式配置日志采集。详情见 [通过 YAML 使用 CRD 配置日志采集](https://intl.cloud.tencent.com/document/product/457/43936)。
