腾讯云 TDSQL-C MySQL 版提供数据库审计能力，记录对数据库的访问及 SQL 语句执行情况，帮助企业进行风险控制，提高数据安全等级。本文为您介绍通过控制台开通审计服务相关操作。

## 前提条件
已 [创建集群](https://www.tencentcloud.com/document/product/1098/52634)。

## 操作步骤
1. 登录 [TDSQL-C MySQL 版控制台](https://console.cloud.tencent.com/cynosdb/mysql#/)。
2. 在左侧导航栏选择**数据库审计**。
3. 在审计状态后单击**未开启**过滤出未开启审计服务的实例。
4. 在审计实例列表里找到目标实例（也可在搜索框通过资源属性筛选快速查找），在其**操作**列单击**开通审计服务**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/6Mfa017_31.png)
>?支持批量开通审计服务。在审计实例列表页勾选多个目标实例，单击上方**开通审计服务**即可进入设置界面。
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/XXvD744_32.png)
5. 在开通审计服务界面，依次完成审计实例选择、审计规则设置、审计服务设置，阅读并勾选腾讯云服务协议，单击**确定**。
 1. **审计实例选择**
在审计实例选择项下面，系统默认勾选**步骤4**中所选择的实例，同时支持在此窗口下修改目标实例（选择其他实例、多选实例），也可在搜索框根据实例 ID / 名称快速查找目标实例，完成实例选择后进入审计规则设置。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5NNs172_33.png)
 2. **审计规则设置**
在审计规则设置项下面，您需要选择规则为**全审计**或者**规则审计**，两者详细对比说明见下表。
<table>
<thead><tr><th>参数</th><th>说明</th></tr></thead>
<tbody><tr>
<td>全审计</td>
<td>全面记录对数据库的所有访问及 SQL 语句执行情况。</td></tr>
<tr>
<td>规则审计</td>
<td>对 TDSQL-C MySQL 版数据库的<strong>客户端 IP、用户名、数据库名、SQL 命令详情、SQL 类型</strong>属性设置审计规则，根据自定义的审计规则记录对数据库的访问及 SQL 语句执行情况。</td></tr>
</tbody></table>
<ul><li>若您选择的审计规则为<b>全审计</b>，可直接进入审计服务设置。</li>
<li>若您选择的审计规则为<b>规则审计</b>，则需选择创建新规则或者从规则模板中选择规则，若从规则模板中选择了一个已有的规则，则可直接进入审计服务设置，若规则模板中没有合适的规则，您可以新建规则模板后刷新，即可选择新建的规则模板，详细操作可参考 <a href="https://www.tencentcloud.com/document/product/1098/53392">新建规则模板</a>。
</li>
<li>您也可以选择创建新规则直接对规则内容进行新建，以下为您介绍创建新规则操作。
您需要选择规则内容的参数字段、匹配类型以及设置对应参数字段的特征串，具体配置说明详见下表。
>?
>- 可以配置单个或多个规则。
>- 不同规则之间，是与的关系，表示需同时满足。
>- 一个规则内不同特征串之间是或的关系，表示多者间只需满足其中一个。
>- 同一个规则只可加一条，例如同是数据库名，在一个模板中要么仅支持包含，要么仅支持不包含。
</li></ul>
<table>
<thead><tr><th>参数字段</th><th>匹配类型</th><th>特征串</th></tr>
</thead>
<tbody><tr>
<td>客户端 IP</td>
<td>包含、不包含、等于、不等于</td>
<td>最多可配置5个客户端 IP，使用英文竖线分隔。</td></tr>
<tr>
<td>用户名</td>
<td>包含、不包含、等于、不等于</td>
<td>最多可配置5个用户名，使用英文竖线分隔。</td></tr>
<tr>
<td>数据库名</td>
<td>包含、不包含、等于、不等于</td>
<td>最多可配置5个数据库名，使用英文竖线分隔。</td></tr>
<tr>
<td>SQL 命令详情</td>
<td>包含、不包含、等于、不等于</td>
<td>最多可配置5句 SQL 命令，使用英文竖线分隔。</td></tr>
<tr>
<td>SQL 类型</td>
<td>包含、不包含</td>
<td>可选类型：Alter、Changeuser、Create、delete、drop、execute、insert、login、logout、other、replace、select、set、update，最多可选择5个 SQL 类型。</td></tr>
</tbody></table>

<b>示例</b>：若用户设置的规则内容为：数据库名，包含 a、b、c，客户端 IP 包含 IP1、IP2、IP3，则该规则过滤出的审计日志为：数据库名包含 a 或 b 或 c 且客户端 IP 包含 IP1 或 IP2 或 IP3 的审计日志。
 3. **审计服务设置**
在审计服务设置项下面，您需要设置审计日志保存时长及高低频存储时长，阅读并勾选腾讯云服务协议，然后单击**确定**开通审计服务。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/AQLR881_34.png)
<table>
<thead><tr><th>参数</th><th>说明</th></tr></thead>
<tbody><tr>
<td>日志保存时长</td>
<td>设置审计日志的保存时长，单位：天，支持选择7、30、90、180、365、1095、1825天。</td></tr>
<tr>
<td>高频存储时长</td>
<td>高频存储代表超高性能存储介质，拥有最佳的查询性能；单位：天，设定存储时长后，指定时长范围内审计数据会存储在高频存储中，超过高频存储时长部分数据会自动落冷至低频存储中。不同存储支持的审计能力完全相同，仅性能差异。例如：日志保存时长设置为30天，高频存储时长设置为7天，则低频存储时长默认为23天。</td></tr>
</tbody></table>
