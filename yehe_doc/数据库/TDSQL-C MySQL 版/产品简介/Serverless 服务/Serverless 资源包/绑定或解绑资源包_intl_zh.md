如需使用资源包，您需要在购买资源包后进行绑定，已绑定资源包的集群也支持解绑资源包。本文为您介绍绑定或解绑资源包。
>?一个资源包支持绑定多个 Serverless 版集群，但一个 Serverless 版集群只能绑定最多一个计算资源包和一个存储资源包。
## 前提条件
- 已 [创建 Serverless 版集群](https://www.tencentcloud.com/document/product/1098/51976)。
- 已 [购买资源包](https://www.tencentcloud.com/document/product/1098/55247)。

## 绑定资源包[](id:BDZYB)
### 场景一：创建 Serverless 版集群时绑定资源包
1. 登录 [购买页](https://buy.tencentcloud.com/cynosdb?product=package)，根据实际需求完成**数据库配置**设置。
<table>
<thead><tr><th width=13%>参数</th><th>说明</th></tr></thead>
<tbody>
<tr>
<td>数据库引擎</td>
<td>选择 MySQL。</td></tr>
<tr>
<td>数据库形态</td>
<td>选择 Serverless。</td></tr>
<tr>
<td>地域</td>
<td>选择您的数据库部署地域。<dx-alert infotype="explain" title="">
目前 Serverless 仅支持广州、上海、北京、南京、香港、硅谷、新加坡地域，如以上地域不满足您的需求，可 [提交工单](https://console.cloud.tencent.com/workorder/category)。
</dx-alert></td></tr>
<tr>
<td>主可用区</td>
<td>选择部署可用区，实际可用区以购买页展示为准。</td></tr>
<tr>
<td>多可用区部署</td>
<td>当前 Serverless 实例不支持多可用区部署。</td></tr>
<tr>
<td>网络</td>
<td>出于性能安全考虑，目前仅支持私有网络（VPC）部署，云服务器需要与 TDSQL-C 在同一 <a href="https://www.tencentcloud.com/document/product/215">VPC</a> 下方可通信。</td></tr>
<tr>
<td>兼容数据库</td>
<td>支持 MySQL 5.7、8.0。</td></tr>
<tr>
<td>算力配置</td>
<td>选择算力配置 CCU（TDSQL-C Compute Unit）上下限，实例会根据选择资源范围自动进行弹性扩缩容。<dx-alert infotype="explain" title="">
CCU（TDSQL-C Compute Unit）为 Serverless 的计算计费单位，一个 CCU 近似等于1个 CPU 和 2GB 内存的计算资源，每个计费周期的 CCU 使用数量为：数据库所使用的 CPU 核数与内存大小的1/2 二者中取最大值。算力配置可参考 <a href="https://www.tencentcloud.com/document/product/1098/51975">服务算力配置</a>。</td></tr>。
</dx-alert></td></tr>
<tr>
<td>自动暂停</td>
<td>配置实例自动暂停时间，在设定时间内无连接访问数据库时，会自动暂停实例，实例暂停后计算将不再计费。</td></tr>
</tbody></table>


2. 完成**规格计费**配置，单击**下一步**。
>?**Serverless 版集群总费用 = 计算节点费用 + 存储空间费用 = Serverless 算力价格 × CCU 量 + 存储空间价格 × 存储空间**
<table>
<thead><tr><th width=13%>参数</th><th>说明</th></tr></thead>
<tbody>
<tr>
<td>计算计费模式</td>
<td>选择资源包模式。<dx-alert infotype="explain" title="">
计算资源固定额度的资源包，用来优先抵扣按量计费产品中实际产生的用量，资源包额度消耗完毕后，会继续按照按量计费模式计费。计算资源包会按照每秒实际使用的 CCU 量进行抵扣，相比于按量付费模式更为划算，使用更为灵活。
</dx-alert></td></tr>
<tr>
<td>计算资源包</td>
<td>绑定资源包，可绑定当前账户下，在有效期内的，集群所选地域的所有计算资源包。若无可用资源包，可先 <a href="https://www.tencentcloud.com/document/product/1098/55247">购买资源包</a>。</td></tr>
<tr>
<td>存储计费模式</td>
<td>选择资源包模式。<dx-alert infotype="explain" title="">
存储资源固定额度的资源包，用来优先抵扣按量计费产品中实际产生的用量，资源包额度消耗完毕后，会继续按照按量计费模式计费。存储资源包会按照每小时实际使用的存储量进行抵扣，相比于按量付费模式更为划算，使用更为灵活。
</dx-alert></td></tr>
<tr>
<td>存储资源包</td>
<td>绑定资源包，可绑定当前账户下，在有效期内的，集群所选地域的所有存储资源包。若无可用资源包，可先 <a href="https://www.tencentcloud.com/document/product/1098/55247">购买资源包</a>。</td></tr>
</tbody></table>


3. 选择集群数量，支持批量购买同规格多个集群，然后单击**下一步**。
4. 完成**基础信息**设置和**高级配置**设置，确认费用后单击**立即购买**。
 - **基础信息**
<table>
<thead><tr><th width=13%>参数</th><th>说明</th></tr></thead>
<tbody><tr>
<td>集群名</td>
<td>可选择创建后命名或立即命名。支持长度小于60的中文、英文、数字、<code>-</code>、<code>_</code>、<code>.</code>。</td></tr>
<tr>
<td>管理员用户名</td>
<td>默认为 root。</td></tr>
<tr>
<td>密码</td>
<td>8 - 64个字符，包含大小写英文字母、数字和符号 <code>~!@#$%^&amp;*_-+=|\(){}[]:;'&lt;&gt;,.?/</code> 中的任意三种。</td></tr>
<tr>
<td>默认字符集</td>
<td>支持 UTF8、GBK、LATIN1、UTF8MB4。</td></tr>
<tr>
<td>自定义端口</td>
<td>默认为3306，支持自定义输入。</td></tr>
</tbody></table>
 - **高级配置**
<table>
<thead><tr><th width=13%>参数</th><th>说明</th></tr></thead>
<tbody><tr>
<td>安全组</td>
<td>选择或新建安全组。</td></tr>
<tr>
<td>参数模板</td>
<td>选择或新建参数模板。</td></tr>
<tr>
<td>表名大小写敏感</td>
<td>可选择为不敏感或敏感。</td></tr>
<tr>
<td>指定项目</td>
<td>为您要新建的集群指定所属项目。</td></tr>
<tr>
<td>告警策略</td>
<td>选择或新建告警策略。</td></tr>
<tr>
<td>标签</td>
<td>添加标签，方便您进行资源分类和管理。</td></tr>
<tr>
<td>协议条款</td>
<td>阅读并勾选协议条款。</td></tr>
</tbody></table>
5. 购买成功后，返回 [集群列表](https://console.cloud.tencent.com/cynosdb/mysql/ap-beijing/cluster/cynosdbmysql-4fyuay8e/detail)，待集群状态显示为**运行中**，即可正常使用。
>?
>- 若资源包仅绑定了计算资源包，则 Serverless 版集群的计算节点为资源包抵扣模式，存储节点为后付费模式。
>- 若资源包仅绑定了存储资源包，则  Serverless 版集群的存储节点为资源包抵扣模式，计算节点为后付费模式。
>- 若资源包绑定了计算和存储资源包。则 Serverless 版集群计算节点为资源包抵扣模式，存储节点也为资源包抵扣模式。

### 场景二：为已有 Serverless 版集群绑定资源包
#### 从资源包列表绑定已有 Serverless 版集群
购买资源包后，支持在资源包列表，将目标资源包绑定于已有的 Serverless 版集群。
1. 登录 [TDSQL-C MySQL 版控制台](https://console.cloud.tencent.com/cynosdb/mysql#/)。
2. 在左侧导航栏选择**资源包**，进入**资源包管理页**。
3. 在下方直接找到目标资源包，或在右侧搜索栏快捷筛选出目标资源包，单击其操作列的**绑定/解绑**。
4. 在弹窗下，选择地域，然后选择资源包需绑定的 Serverless 版集群，支持多选，单击**确定**。

#### 从集群管理页为已有 Serverless 版集群绑定资源包
1. 登录 [TDSQL-C MySQL 版控制台](https://console.cloud.tencent.com/cynosdb/mysql#/)。
2. 在左侧集群列表，单击**目标集群**，进入**集群管理页**。
3. 在集群管理页选择**资源包**，然后单击**资源包绑定**。
4. 在弹窗下，选择所需资源包，单击**确定**。
>?
>- 支持仅选择一个计算资源包或存储资源包，则对应存储或计算节点为按量计费模式。
>- 支持最多选择一个计算资源包和存储资源包。

## 解绑资源包
资源包过期、资源使用完毕时，此资源包会自动解绑，除此之外，您还可以手动解绑。
#### 从资源包列表解绑已有 Serverless 版集群
1. 登录 [TDSQL-C MySQL 版控制台](https://console.cloud.tencent.com/cynosdb/mysql#/)。
2. 在左侧导航栏选择**资源包**，进入**资源包管理页**。
3. 在下方直接找到有绑定集群的目标资源包，或在右侧搜索栏快捷筛选出目标资源包，单击其操作列的**绑定/解绑**。
4. 在弹窗下，选择地域，然后在右侧删除已绑定的 Serverless 版集群，单击**确定**。

#### 从集群管理页为已有 Serverless 版集群解绑资源包
1. 登录 [TDSQL-C MySQL 版控制台](https://console.cloud.tencent.com/cynosdb/mysql#/)。
2. 在左侧集群列表，单击**目标集群**，进入**集群管理页**。
3. 在集群管理页选择**资源包**。
4. 在下方找到需要解绑的资源包，单击其操作列的**解绑**。
5. 在弹窗下单击**确定**。
