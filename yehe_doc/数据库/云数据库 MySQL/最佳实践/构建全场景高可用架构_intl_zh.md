﻿云数据库 MySQL 基于跨可用区部署、异地备份保障与配套生态工具，搭配数据库代理和弹性 CPU 等多项功能，全方位保障您的业务安全稳定运行。本文为您介绍通过云数据库 MySQL 构建全场景高可用架构。
## 背景
数据库在企业的核心业务中扮演着至关重要的角色，数据是企业的基础资源和生命线。因此，为保证企业的稳定生产运营，一个高可用的数据库架构是不可或缺的。对于企业来说，如果数据库出现宕机、数据丢失或不可用等问题，将会产生重大的影响和经济损失。因此，云数据库 MySQL 推出全场景高可用性架构（All-Scenario High Availability Architecture，AS-HAA），全方位全流程保障业务稳定运行。
## 前提条件
已注册腾讯云账号并完成实名认证。
- [注册腾讯云账号](https://cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F)
- [完成实名认证](https://console.cloud.tencent.com/developer)

## 优势
- 高稳定性：快速扩容、均衡负载、自动弹性扩缩容、就近访问能力提供扩展性强、平稳运行、低网络延时的环境。
- 高可用性：全组件实现跨可用区/跨地域部署，降低单点故障风险，通过备份、数据同步等机制，减少业务停机时间和数据丢失率。
- 高数据处理能力和响应速度：数据库代理将负载分布到多个数据库节点上，从而提高数据处理能力和响应速度。
- 高故障诊断和恢复效率：数据库智能管家 DBbrain 7*24h监控，帮助 DBA 快速定位问题解决问题；同时，备份、数据同步等机制也有助于故障恢复和数据恢复，缩短故障修复时间。

## 构建全场景高可用架构指引
### 步骤一：高可用架构部署
#### 一、创建三节点架构实例[](id:BZYI)
1. 登录 [MySQL 购买页](https://buy.cloud.tencent.com/cdb)，完成**基础配置**和**实例配置**，单击**下一步**，设置网络和数据库。
**基础配置**
 - **计费模式**：支持包年包月和按量计费。
 - **地域**：选择您业务需要部署 MySQL 的地域。建议您选择与云服务器同一个地域，不同地域的云产品内网不通，购买后不能更换。
 - **数据库版本**：云数据库 MySQL 目前支持以下版本：MySQL 8.0、MySQL 5.7、MySQL 5.6、MySQL 5.5（需白名单）。
 - **引擎**：支持选择 InnoDB 和 RocksDB 引擎。
 - **架构**：选择三节点。
 - **硬盘类型**：云数据库 MySQL 支持本地盘和云盘两种硬盘类型。
 - **可用区**：主可用区和备可用区选择不同的可用区。

 **实例配置**
 - **筛选**：快捷筛选所需实例的 CPU 和内存，默认展示全部 CPU、全部内存。
 - **类型**：提供通用型与独享型两种实例类型，详情请参见 [隔离策略](https://intl.cloud.tencent.com/document/product/236/39794)。
 - **实例规格**：根据业务需要选择对应规格。
 - **硬盘**：用于存放 MySQL 运行时所必须的文件，选择硬盘空间大小。

2. 完成**网络和其他**、**数据库设置**配置，单击**下一步**，确认配置信息。
**网络和其他**
 - **网络**：支持私有网络环境，可选择实例的所属网络和子网。[](id:HXBZ)
 - **自定义端口**：数据库的访问端口，默认为3306。
 - **安全组**：安全组创建与管理请参见 [云数据库安全组](https://intl.cloud.tencent.com/document/product/236/14470)。
>?安全组入站规则需要放通 MySQL 实例的3306端口。MySQL 内网默认端口为3306，同时支持自定义端口，若修改过默认端口号，安全组中需放通 MySQL 新端口信息。
 - **指定项目**：选择数据库实例所属的项目，缺省设置为默认项目。
 - **标签**：便于分类管理实例资源。
 - **告警策略**：创建告警用于在云产品状态改变时触发警报并发送相关消息。

 **数据库设置**
 - **实例名**：可选择创建后命名或立即命名。
 - **数据复制方式**：提供异步复制、半同步复制、强同步复制三种方式。
 - **参数模板**：除提供的系统参数模板外，您也可以创建自定义参数模板，请参见 [使用参数模板](https://intl.cloud.tencent.com/document/product/236/31906)。
 - **字符集**：支持 LATIN1 、GBK、UTF8 、UTF8MB4 字符集，默认字符集编码格式是 UTF8。
 - **排序规则**：实例字符集为系统数据提供的排序规则，即区分大小写属性和重音属性。
 - **表名大小写敏感**：表名是否大小写敏感。
>!MySQL 8.0 版本仅支持在购买页设置表名大小写敏感，其他版本可通过修改 lower_case_table_names 参数来设置，操作方法参见 [设置实例参数](https://intl.cloud.tencent.com/document/product/236/35793)。
 - **密码复杂度**：支持设置密码复杂度以提升数据库安全性，默认为关闭。
 - **root 密码**：新创建的 MySQL 数据库的用户名默认为 root，此处用来设置该 root 账号的密码。选择**创建后设置**时，可在创建完实例后再 [重置密码](https://intl.cloud.tencent.com/document/product/236/31901)。
3. 确认所选配置（如需修改，可单击**编辑**回到对应步骤进行调整），阅读并勾选服务条款，确认购买时长和数量后单击**立即购买**。
4. 支付完成后，返回实例列表，会看到实例显示**发货中**（大概需要3min - 5min中，请耐心等待），待实例状态变为**运行中**，即可进行正常操作。

#### 二、设置本地备份和跨地域备份
**设置本地备份**
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击**实例 ID** 进入管理页面，选择**备份恢复** > **自动备份设置**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/eC3T338_13.png)
2. 在弹出的备份设置对话框，选择各备份参数，单击**确定**。

**开启跨地域备份**
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击**实例 ID** 或**操作**列的**管理**，进入实例管理页面。
2. 在实例管理页面，选择**备份恢复** > **跨地域备份**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5iYI567_14.png)
3. 在跨地域备份设置窗口完成配置后，单击**确定**开启跨地域备份， 阅读并**勾选**跨地域备份空间收费说明，单击**确定**。
 - 跨地域备份开关：默认为关闭，这里选择开启。
 - 备份 binlog：当开启跨地域备份时自动打开，开启后可单独关闭备份 binlog。
 - 备份地域：备份地域最少选择一个与主实例不同的地域，最多可选择两个。
 - 备份地域保留时长：默认为7天，支持设置为3天 - 1830天，到期后备份集会自动删除。
4. 跨地域备份完成后，备份会同步到目标地域，可在源实例备份列表查询。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Pcuj721_15.png)
跨地域备份的文件在**备份地域**项下面会展示所有您选择备份的地域。

#### 三、创建异地灾备实例
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb/)，在实例列表，单击**实例 ID** 或**操作**列的**管理**，进入详情页。
2. 在实例详情页的基本信息中确认 GTID 功能开启，在实例架构图中单击**添加灾备实例**，进入灾备实例购买页。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ceT9482_16.png)
3. 在购买页中，设置灾备实例的**计费模式**、**地域**等基本信息，地域请选择与步骤一中 [创建的三节点架构实例](#BZYI) 不同的地域。
 >?
>- 创建时长受数据量的影响，期间主实例的控制台操作会被锁定，请妥善安排。
>- 同步策略为立即同步，即创建完灾备实例后会立即同步数据。
>- 暂只支持整个实例的数据同步，请确保磁盘空间充足。
>- 请确保主实例状态为运行中并且没有任何运行相关变更任务执行，如升降配、重启等，否则同步任务有可能失败。 
>
4. 确认无误后，单击**立即购买**，待灾备实例发货。
5. 返回实例列表，待实例状态变为**运行中**，即可进行后续操作。

### 步骤二：开通数据库代理
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，选择需要开启代理的主实例，单击实例 ID 或**操作**列的**管理**，进入实例管理页面。
2. 在实例管理页面，选择**数据库代理**页，单击**立即开启**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/nrk6026_17.png)
3. 在弹出的对话框，完成如下配置，单击**确定**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Qkau876_18.png)
<table>
<thead><tr><th>参数</th><th>说明</th></tr></thead>
<tbody><tr>
<td>网络</td>
<td>选择数据库代理的网络，仅支持私有网络 VPC。</td></tr>
<tr>
<td>代理规格</td>
<td>支持选择规格为2核4000MB内存、4核8000MB内存、8核16000MB内存。</td></tr>
<tr>
<td>可用区及节点个数</td>
<td>1. 选择数据库代理可用区，支持单击<strong>新增可用区</strong>来多选，可选择的可用区数量与当前地域可选可用区数量相关，最多支持选择三个可用区。<br>2. 选择节点个数，推荐的代理节点个数为主实例和只读实例 CPU 核数的之和的1/8（向上取整），例如主实例为4核 CPU，只读实例为8核 CPU，则推荐代理数量 = (4 + 8) / 8 ≈ 2。<blockquote class="rno-document-tips rno-document-tips-notice">    <div class="rno-document-tips-body">        <i class="rno-document-tip-icon"></i>        <div class="rno-document-tip-title">注意</div>        <div class="rno-document-tip-desc"><ol><li>如果所选数据库代理与主实例不在同一可用区，通过数据库代理连接时，写入性能可能会下降。</li><li>若计算推荐节点个数后所需代理节点数量超过购买限制，建议选择更高规格代理。</li></ol></div>    </div></blockquote></td></tr>
<tr>
<td>安全组</td>
<td>默认选择的安全组与主实例保持一致，也可根据需要选择已有安全组或新建安全组。<blockquote class="rno-document-tips rno-document-tips-notice">    <div class="rno-document-tips-body">        <i class="rno-document-tip-icon"></i>        <div class="rno-document-tip-title">注意</div>        <div class="rno-document-tip-desc"><p>访问数据库代理需要开通配置安全策略，放通内网访问端口（当前内网端口为：3306），具体详见 <a href="https://intl.cloud.tencent.com/document/product/236/14470">MySQL 安全组配置</a>。</p></div>    </div></blockquote></td></tr>
<tr>
<td>备注</td>
<td>非必填项，可为要开通的数据库代理服务进行备注。</td></tr>
</tbody></table>
4. 开通成功后，支持通过**数据库代理**页 > **概览** > **连接地址**下的内网访问地址直接访问数据库代理，支持对数据库代理地址的访问策略进行配置，在**数据库代理** > **概览** > **连接地址**下找到目标访问地址，单击其**操作**列的**调整配置**。
5. 在跳转的窗口下，设置具体策略的配置，单击**确定。**
<table>
<thead><tr><th>参数</th><th>说明</th></tr></thead>
<tbody><tr>
<td>读写属性</td>
<td>修改此代理访问地址的读写属性，支持选择读写分离或只读。</td></tr>
<tr>
<td>只读实例延迟剔除</td>
<td>设置只读实例延迟剔除策略，此项开启，可设置延迟剔除阈值和只读实例最小保留数。无论此项是否启用，只读实例故障时均会尝试剔除和恢复。<ul><li>延迟剔除阈值：输入大于1或等于1的整数，单位为秒。</li><li>只读实例最小保留数：数量与主实例拥有只读实例数相关，设置为0时，当只读节点全部被剔除后，所有访问会转发到主实例上，直至只读实例重新加入。</li></ul></td></tr>
<tr>
<td>连接池状态</td>
<td>连接池功能主要用于减少短连接业务频繁建立新连接带来的实例负载。此项开启后，可选择支持的连接池类型，目前默认仅支持会话级连接池。</td></tr>
<tr>
<td>事务拆分</td>
<td>设置是否开启，开启后，在一个事务中拆分读和写到不同的实例上去执行，读请求转发到只读实例，降低主实例负载。</td></tr>
<tr>
<td>读权重分配</td>
<td>支持选择系统自动分配或自定义，如开通数据库代理时配置了多个可用区，则支持对不同可用区下的代理节点访问数据库的权重进行分别配置。</td></tr>
<tr>
<td>故障转移（读写属性为读写分离）</td>
<td>设置是否开启，开启后，数据库代理出现故障时，连接地址将会路由到主实例。</td></tr>
<tr>
<td>自动添加只读实例</td>
<td>设置是否开启，开启后，若您购买新的只读实例，会自动添加到数据库代理中。<ul><li>当读权重为系统自动分配时，新购只读实例按照规格大小默认权重分配。</li><li>当读权重为自定义时，新购只读实例默认加入时权重为0，可通过数据库代理页，连接地址下的调整配置来修改。</li></ul></td></tr>
</tbody></table>

### 步骤三：开启性能弹性管理-自动扩缩容
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb/instance)，在实例列表，单击实例 ID 或操作列的**管理**，进入实例详情页。
2. 在**实例详情** > **配置信息** > **性能弹性管理**后，单击**配置**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9GMV182_20.png)
3. 在性能弹性管理窗口下，完成如下配置，确认扩容费用，单击**立即扩容**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/JI4j630_21.png)
<table>
<thead><tr><th>参数</th><th>说明</th></tr></thead>
<tbody>
<tr>
<td>性能扩容类型</td><td>选择自动扩容。</td></tr>
<tr>
<td>CPU 自动弹性扩容阈值</td><td>设置 CPU 平均利用率触发自动弹性扩容的阈值，系统支持选项为70%、80%、90%。</td></tr>
<tr>
<td>观测周期</td><td>设置观测周期，系统支持选项为1分钟、3分钟、5分钟、10分钟、15分钟、30分钟，表示指定时间周期内，系统会观测实例的 CPU 平均利用率是否达到设置的扩容阈值，如达到，则会触发系统自动弹性扩容。</td></tr>
<tr>
<td>CPU 自动弹性回缩阈值</td><td>设置 CPU 平均利用率触发自动弹性回缩的阈值，系统支持选项为30%、20%、10%。</td></tr>
<tr>
<td>观测周期</td><td>设置观测周期，系统支持选项为5分钟、10分钟、15分钟、30分钟，表示指定时间周期内，系统会观测实例的 CPU 平均利用率是否达到设置的回缩阈值，如达到，则会触发系统自动弹性缩容。</td></tr>
</tbody></table>
4. 待实例状态/任务从**配置弹性扩容策略中**变为**运行中**，即成功开启自动扩容。
>?开启自动扩容后，如需修改性能弹性扩容策略，您可在**实例详情** > **配置信息** > **性能弹性管理**后单击**修改**，进行重新配置。

## 生态工具使用指引
### DBbrain 智能管家监测定位问题
运用数据库智能管家，实现数据库性能监控、安全检测和优化诊断，通过智能分析和建议，协助您快速解决数据库性能和安全问题，提升数据库效率。
<table>
<thead><tr><th>分类</th><th>诊断优化功能</th><th>描述</th></tr></thead>
<tbody>
<tr>
<td rowspan="5">诊断分析</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/48640" target="_blank">异常诊断</a></td><td>为用户的数据库实例提供实时的性能监控、健康巡检、故障诊断和优化，让用户既可以直观地感知数据库实例实时的运行状况，也可以定位实时出现的性能异常，并根据优化建议进行系统优化。</td>
</tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/48637" target="_blank">慢 SQL 分析</a></td><td>对慢 SQL 的性能进行分析，并给出优化建议。</td>
</tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/48636" target="_blank">空间分析</a></td><td>可查看实例空间的使用率，包括数据空间和日志空间的大小、空间使用率的日均增长量、预估的可用天数，以及查看实例下表空间、库空间所占用的空间详情及变化趋势。</td>
</tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/48635" target="_blank">SQL 优化</a></td><td>为用户提供一键优化 SQL 语句功能，并给出对应执行计划解析和优化建议。</td>
</tr>
<td>审计日志分析</td><td>对 SQL 的性能进行分析，并针对低质量 SQL 结合索引情况、库表设计，给出优化建议。</td>
</tr>
<tr>
<td rowspan="3">定位和处理数据库会话连接问题</td>
<td>KILL 会话</td><td>KILL 当前会话和持续 KILL 会话。</td>
</tr>
<td>SQL 限流</td><td>通过创建 SQL 限流任务，自主设置 SQL 类型、最大并发数、限流时间、SQL 关键词，来限制数据库的请求访问量和 SQL 并发量，进而达到服务的可用性，不同的任务之间不会发生冲突。</td>
</tr>
<td>热点更新保护</td><td>针对于频繁更新或秒杀类业务场景，大幅度优化对于热点行数据的 UPDATE 操作的性能。</td>
</tr>
<tr><td>数据库自治</td><td>自治服务</td><td>支持自动 SQL 限流与异常 SQL KILL 功能，当满足触发条件时，自动触发 SQL 限流和异常 SQL KILL 自治任务，解决数据库异常问题，全程无需人工干预。</td></tr>
</tbody></table>


### 混沌演练平台模拟异常场景
[混沌演练平台](https://console.cloud.tencent.com/cfg/exercise) 可以帮助您模拟各种突发事件和异常场景，提高系统的容错能力和可靠性。搭建好真实的数据库架构后，平台会对业务进行全方位的压力测试，对传统的异常场景进行模拟并进行自动化部署管理，从而能够更好地发现和诊断系统中的潜在问题，以提升业务的质量和可靠性。
详细演练创建及过程可参见 [混沌演练快速入门](https://cloud.tencent.com/document/product/1500/61446#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E5.88.9B.E5.BB.BA.E6.BC.94.E7.BB.83.5B.5D(id.3Astep1))。
## 相关文档
- [创建 MySQL 实例](https://intl.cloud.tencent.com/document/product/236/37785)
- [备份数据库](https://intl.cloud.tencent.com/document/product/236/37796)
- [跨地域备份](https://www.tencentcloud.com/document/product/236/50652)
- [创建灾备实例](https://intl.cloud.tencent.com/document/product/236/7272)
- [开通数据库代理](https://www.tencentcloud.com/document/product/236/42052)
- [事物拆分](https://www.tencentcloud.com/document/product/236/51883)
- [防闪断](https://www.tencentcloud.com/document/product/236/51882)
- [设置数据库代理读写属性](https://www.tencentcloud.com/document/product/236/42054)
- [性能弹性管理](https://www.tencentcloud.com/document/product/236/56096)