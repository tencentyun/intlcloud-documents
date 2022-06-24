## 功能描述

性能趋势实时监控数据库实例、Redis 节点以及 Proxy 节点关键性能指标，包括：CPU、内存、Key 信息、网络使用量、网络使用率、请求、响应等，秒级监控数据采集粒度，以图形化方式动态展示各个指标的变化趋势，以表格形式统计各个指标的最大值、最小值及平均值，多节点指标对比查看、不同时间段指标对比分析，随意调大拖动监控视图。
其强大的数据统计分析能力，丰富多样的展示方式，极高的实时性，可满足数据库实例日常运维、异常定位的各种场景，帮助运维人员快速地掌握数据库性能状况的全貌，及时预防风险。

## 监控指标

当前支持的监控指标分为3个维度，包括：实例、Redis 节点、Proxy 节点。

### 实例维度

<table>
<thead>
<tr><th width="15%">指标类别</th><th width="25%">指标中文名</th><th width="10%">指标英文名</th><th width="5%">单位</th><th width="45%">指标含义</th></tr>
</thead>
<tbody><tr>
<td rowspan="2">CPU</td>
<td>CPU 使用率</td>    <td>cpu_util</td><td>%</td><td>平均 CPU 使用率</td></tr>
<tr>
<td>节点最大 CPU 使用率</td><td>cpu_max_util</td><td>%</td><td>实例中节点（分片或者副本）最大 CPU 使用率</td></tr>    
<tr>
<td rowspan="3">内存信息</td> 
<td>内存使用量</td><td>mem_used</td><td>MB</td><td>实际使用内存容量，包含数据和缓存部分</td></tr>
<tr>   
<td>内存使用率</td><td>mem_util</td><td>%</td><td>实际使用内存和申请总内存之比</td></tr>
<tr>    
<td>节点最大内存使用率</td><td>mem_max_util</td><td>%</td><td>实例中节点（分片或者副本）最大内存使用率</td></tr>
<tr>
<td rowspan="3">Key 信息</td>  
<td>Key 总个数</td><td>keys</td><td>个</td><td>实例存储的总 Key 个数（一级 Key）</td></tr>
<tr>
<td>Key 过期数</td><td>expired</td><td>个</td><td>时间窗内被淘汰的 Key 个数，对应 info 命令输出的 expired_keys</td></tr>
<tr> 
<td>Key 驱逐数</td><td>evicted</td><td>个</td><td>时间窗内被驱逐的 Key 个数，对应 info 命令输出的 evicted_keys</td></tr>
<tr>
<td rowspan="3">网络使用量</td> 
<td>连接数</td><td>connections</td><td>个</td><td>连接到实例的 TCP 连接数量</td></tr>    
<tr>   
<td>入流量</td><td>in_flow</td><td>Mb/s</td><td>内网入流量</td></tr>
<tr>    
<td>出流量</td><td>out_flow</td><td>Mb/s</td><td>内网出流量</td></tr>
<tr>
<td rowspan="3">网络使用率</td>     
<td>连接使用率</td><td>connections_util</td><td>%</td><td>实际 TCP 连接数量和最大连接数比</td></tr>    
<tr> 
<td>入流量使用率</td><td>in_bandwidth_util</td><td>%</td><td>内网入流量实际使用和最大流量比</td></tr>    
<tr>  
<td>出流量使用率</td><td>out_bandwidth_util</td><td>%</td><td>内网出流量实际使用和最大流量比</td></tr>
<tr>
<td rowspan="7">请求</td>    
<td>总请求</td><td>commands</td><td>次/秒</td><td>QPS，命令执行次数</td></tr>
<tr> 
<td>读请求</td>    <td>cmd_read</td><td>次/秒</td><td>每秒读命令执行次数</td></tr>
<tr>
<td>写请求</td><td>cmd_write</td><td>次/秒</td><td>每秒写命令执行次数</td></tr>
<tr>
<td>其他请求</td> <td>cmd_other</td><td>次/秒</td><td>每秒读写命令之外的命令执行次数</td></tr>
<tr> 
<td>大 Value 请求</td>    <td>cmd_big_value</td><td>次/秒</td><td>每秒请求命令大小超过32KB的执行次数</td></tr>
<tr> 
<td>Key 请求数</td>    <td>cmd_key_count</td><td>次/秒</td><td>每秒请求 Key 数量</td></tr>
<tr> 
<td>Mget 请求数</td>    <td>cmd_cmget</td><td>次/秒</td><td>每秒通过 Mget 请求的数量</td></tr>    
<tr>
<td rowspan="4">响应</td>
<td>慢查询</td><td>cmd_slow</td><td>次</td><td>执行时延大于 slowlog - log - slower - than 配置的命令次数</td></tr>
<tr>
<td>读请求命中</td>    <td>cmd_hits</td><td>次</td><td>读请求 Key 存在的个数，对应 info 命令输出的 keyspace_hits 指标</td></tr>
<tr>
<td>读请求 Miss</td>    <td>cmd_miss</td><td>次</td><td>读请求 Key 不存在的个数，对应 info 命令输出的 keyspace_misses 指标</td></tr>
<tr>   
<td>读请求命中率</td><td>cmd_hits_ratio</td><td>%</td><td>Key 命中 / (Key 命中 + KeyMiss)，该指标可以反应 Cache Miss 的情况，当访问为0时，该值为 null</td></tr>
<tr>
<td>执行错误</td>
<td>执行错误</td>   <td>cmd_err</td><td>次</td><td>命令执行错误的次数，例如命令不存在、参数错误等情况</td></tr>
<tr>
<td rowspan=6>时延</td>
<td>平均执行时延</td><td>latency_avg</td><td>ms</td><td>Proxy 到 Redis Server 的执行时延平均值</td></tr>
<tr>
<td>最大执行时延</td><td>latency_max</td><td>ms</td><td>Proxy 到 Redis Server 的执行时延最大值</td></tr>
<tr>
<td>P99执行时延</td><td>latency_p99</td><td>ms</td><td>Proxy 到 Redis Server 99%的执行时延</td></tr>
<tr>
<td>读平均时延</td><td>latency_read</td><td>ms</td><td>Proxy 到 Redis Server 的读命令平均执行时延，读命令分类，请参见 <a href="https://intl.cloud.tencent.com/document/product/239/38743">命令分类</a></td></tr>
<tr>
<td>写平均时延</td><td>latency_write</td><td>ms</td><td>Proxy 到 Redis Server 的写命令平均执行时延，写命令分类，请参见 <a href="https://intl.cloud.tencent.com/document/product/239/38743">命令分类</a></td></tr>
<tr>
<td>其他命令平均时延</td><td>latency_other</td><td>ms</td><td>Proxy 到 Redis Server 的读写命令之外的命令平均执行时延</td></tr>
</tbody></table>

### Redis 节点

<table>
<thead>
<tr><th width="15%">指标类别</th><th width="25%">指标中文名</th><th width="10%">指标英文名</th><th width="5%">单位</th><th width="45%">指标含义</th></tr>
</thead>
<tbody>
<tr>
<td>CPU</td>
<td>CPU 使用率</td><td>cpu_util</td><td>%</td><td>平均 CPU 使用率</td></tr>
<tr>
<td  rowspan=2>网络使用量</td>
<td>连接数</td><td>connections</td><td>个</td><td>Proxy 连接到节点的连接数</td></tr>
<tr>
<td>连接使用率</td><td>connections_util</td><td>%</td><td>节点连接数使用率</td></tr>
<tr>
<td  rowspan=2>内存信息</td>
<td>内存使用量</td><td>mem_used</td><td>MB</td><td>实际使用内存容量，包含数据和缓存部分</td></tr>
<tr>
<td>内存使用率</td><td>mem_util</td><td>%</td><td>实际使用内存和申请总内存之比</td></tr>
<tr>
<td rowspan=3>Key 信息</td>
<td>Key 总个数</td><td>keys</td><td>个</td><td>实例存储的总 Key 个数（一级 Key）</td></tr>
<tr>
<td>Key 过期数</td><td>expired</td><td>个</td><td>时间窗内被淘汰的 Key 个数，对应 info 命令输出的 expired_keys</td></tr>
<tr>
<td>Key 驱逐数</td><td>evicted</td><td>个</td><td>时间窗内被驱逐的 Key 个数，对应 info 命令输出的 evicted_keys</td></tr>
<tr>
<td>复制延迟</td><td>复制延迟</td><td>repl_delay</td><td>Byte</td><td>副本节点的相对主节点命令延迟长度</td></tr>
<tr>
<td  rowspan=4>请求</td>
<td>总请求</td><td>commands</td><td>次/秒</td><td>QPS，命令执行次数</td></tr>
<tr>
<td>读请求</td><td>cmd_read</td><td>次/秒</td><td>读命令执行次数，读命令分类，请参见 <a href="https://intl.cloud.tencent.com/document/product/239/38743">命令分类</a></td></tr>
<tr>
<td>写请求</td><td>cmd_write</td><td>次/秒</td><td>写命令执行次数，写命令分类，请参见 <a href="https://intl.cloud.tencent.com/document/product/239/38743">命令分类</a></td></tr>
<tr>
<td>其他请求</td><td>cmd_other</td><td>次/秒</td><td>读写命令之外的命令执行次数</td></tr>
<tr>
<td  rowspan=4>响应</td>
<td>慢查询</td><td>cmd_slow</td><td>次</td><td>执行时延大于 slowlog-log-slower-than 配置的命令次数</td></tr>
<tr>
<td>读请求命中</td><td>cmd_hits</td><td>次</td><td>读请求 Key 存在的个数，对应 info 命令输出的 keyspace_hits 指标</td></tr>
<tr>
<td>读请求 Miss</td><td>cmd_miss</td><td>次</td><td>读请求 Key 不存在的个数，对应 info 命令输出的 keyspace_misses 指标</td></tr>
<tr>
<td>读请求命中率</td><td>cmd_hits_ratio</td><td>%</td><td>Key 命中 / (Key命中 + KeyMiss)，该指标可以反应 Cache Miss 的情况</td></tr>
</tbody></table>

### Proxy 节点

<table>
<thead><tr><th width="20%">指标类别</th><th width="30%">指标中文名</th><th width="20%">指标英文名</th><th width="5%">单位</th><th width="25%">指标含义</th></tr></thead>
<tbody>
<tr>
<td>CPU</td>
<td>CPU 使用率</td><td>cpu_util</td><td>%</td><td>Proxy CPU 使用率</td></tr>
<tr>
<td rowspan=5>请求</td>
<td>总请求</td><td>proxy_commands</td><td>次/秒</td><td>Proxy 执行的命令数</td></tr>
<tr>
<td>Key 请求数</td><td>cmd_key_count</td><td>个/秒</td><td>命令访问的 Key 个数</td></tr>
<tr>
<td>Mget 请求数</td><td>cmd_mget</td><td>次/秒</td><td>Mget 命令执行次数</td></tr>
<tr>
<td>执行错误</td><td>cmd_err</td><td>次/秒</td><td>Proxy 命令执行错误的次数，例如，命令不存在、参数错误等情况</td></tr>
<tr>
<td>大 Value 请求</td><td>cmd_big_value</td><td>次/秒</td><td>请求命令大小超过32KB的执行次数</td></tr>
<tr>
<td rowspan=2>流量</td>
<td>入流量</td><td>in_flow</td><td>Mb/s</td><td>内网入流量</td></tr>
<tr>
<td>出流量</td><td>out_flow</td><td>Mb/s</td><td>内网出流量</td></tr>
<tr>   
<td rowspan=4>网络使用量</td>
<td>连接数</td><td>connections</td><td>个</td><td>连接到实例的 TCP 连接数量</td></tr>
<tr>
<td>每秒建连数</td><td>client_connections_received_per_second</td><td>个</td><td>每秒建立的 TCP 连接的数量</td></tr>
<tr>
<td>每秒断连数</td><td>client_connections_closed_per_second</td><td>个</td><td>每秒断开的 TCP 连接的数量</td></tr>
<tr>
<td>每秒异常断连数</td><td>client_connections_aborted_per_second</td><td>个</td><td>每秒异常断开的 TCP 连接的数量</td></tr> 
<tr>
<td rowspan=5>网络使用率</td>
<td>连接使用率</td><td>connections_util</td><td>%</td><td>实际 TCP 连接数量和最大连接数比</td></tr>
<tr>
<td>入流量使用率</td><td>in_bandwidth_util</td><td>%</td><td>内网入流量实际使用和最大流量比</td></tr>
<tr>
<td>入流量限流触发</td><td>in_flow_limit</td><td>次</td><td>入流量触发限流的次数</td></tr>
<tr>
<td>出流量使用率</td><td>out_bandwidth_util</td><td>%</td><td>内网出流量实际使用和最大流量比</td></tr>
<tr>
<td>出流量限流触发</td><td>out_flow_limit</td><td>次</td><td>出流量触发限流的次数</td></tr>
<tr>
<td rowspan=6>时延</td>
<td>平均执行时延</td><td>latency_avg</td><td>ms</td><td>Proxy 到 Redis Server 的执行时延平均值</td></tr>
<tr>
<td>最大执行时延</td><td>latency_max</td><td>ms</td><td>Proxy 到 Redis Server 的执行时延最大值</td></tr>
<tr>
<td>P99执行时延</td><td>latency_p99</td><td>ms</td><td>Proxy 到 Redis Server 99%的执行时延</td></tr>
<tr>
<td>读平均时延</td><td>latency_read</td><td>ms</td><td>Proxy 到 Redis Server 的读命令平均执行时延，读命令分类，请参见 <a href="https://intl.cloud.tencent.com/document/product/239/38743">命令分类</a></td></tr>
<tr>
<td>写平均时延</td><td>latency_write</td><td>ms</td><td>Proxy 到 Redis Server 的写命令平均执行时延，写命令分类，请参见 <a href="https://intl.cloud.tencent.com/document/product/239/38743">命令分类</a></td></tr>
<tr>
<td>其他命令平均时延</td><td>latency_other</td><td>ms</td><td>Proxy 到 Redis Server 的读写命令之外的命令平均执行时延</td></tr>
</tbody></table>

## 查看监控数据
### 步骤1：选择监控指标
1. 登录 [Redis 控制台](https://console.cloud.tencent.com/redis)。
2. 在左侧导航栏，选择**诊断优化**。
3. 在**数据库智能管家 DBbrain** 的**诊断优化**页面上方，在**实例 ID** 的下拉列表选择需查看的实例。
![](https://qcloudimg.tencent-cloud.cn/raw/471e4894326f328c2648539c861006b4.png)
4. 单击**性能趋势**页签，在指标类别的下拉列表，勾选需分析的性能指标，并**保存**。
如果需要设置性能指标应用于该腾讯云账号下的所有云数据库 Redis 实例，可单击**保存并应用于全部实例**，如下图所示。
![](https://qcloudimg.tencent-cloud.cn/raw/2aed7a308b1a907643325d736b213ae2.png)

### 步骤2：设置采集粒度
在**性能趋势**页签右上方**自动刷新**右侧的下拉列表中，选择监控数据采集粒度，支持5秒、15秒、30秒。请参见下图。
![](https://qcloudimg.tencent-cloud.cn/raw/62c0653020be652ddc4072a971437655.png)

### 步骤3：查看监控指标变化趋势
#### 查看不同维度监控指标
在**性能趋势**页签指标类别下方，您可根据业务运维场景需求，查看实例、Redis 节点、Proxy 节点不同维度的监控指标数据。
![](https://qcloudimg.tencent-cloud.cn/raw/b4a6898a6a71bee1c0800e35073ca8a9.png)
![img](https://qcloudimg.tencent-cloud.cn/raw/b16542ef1ece75dd1c737b728952b289.png)

#### 多节点性能指标对比
1. 在**性能趋势**页签，单击**多节点性能对比**。
2. 在**多节点性能对比**面板，单击**新建多节点性能对比**。
3. 在**新建多节点性能对比**对话框，在**监控时间**后面的选择框，单击<img src="https://qcloudimg.tencent-cloud.cn/raw/a1438740099d1baedaf57020fb2e397b.png" style="zoom: 50%;" />选择监控时间段，在**监控项**的下拉列表中，选择需对比的监控指标，然后单击**确定**。
<img src="https://qcloudimg.tencent-cloud.cn/raw/99cd1e438fbe817a9177a44fb5fb8d86.png" style="zoom:67%;" />
4. 在**多节点性能对比**面板的任务列表中，等待**状态**为**生成成功**。
![](https://qcloudimg.tencent-cloud.cn/raw/475d8977ce18651b964b228515031df0.png)
5. 单击**操作**列的**查看**，查看该指标 Redis 全节点的监控对比数据。下图以连接数指标为例展示。
![](https://qcloudimg.tencent-cloud.cn/raw/87d678d8f47f9f5e0b25165559fa3a5f.png)

#### 切换实时/历史视图
在**性能趋势**页签，默认实时展示监控数据。
- 日常运维监控中，可实时监控数据库实例的各项指标。
- 异常定位时，单击**历史**，可分析历史上某一时间区间的监控数据。
  - 支持直接查看近1小时、近3小时、近7天的监控数据，
  - 单击<img src="https://qcloudimg.tencent-cloud.cn/raw/a1438740099d1baedaf57020fb2e397b.png" style="zoom: 50%;" />，选择查看近30天任意时间段的监控数据。
![](https://qcloudimg.tencent-cloud.cn/raw/fead86e3fbdad4920f39bae59ad40af2.png)

#### 不同时间段监控性能对比
1. 在**性能趋势**页签，单击**历史**，再单击**添加时间对比**。
2. 在时间选择框，选择需对比的两个时间段。
3. 选择需关注的监控指标，将鼠标放在监控视图变化趋势图上，对比两个时间段的监控数据。
![](https://qcloudimg.tencent-cloud.cn/raw/21587e43c6c891a2c90cb01ab073fa2b.png)

#### 以图表形式统计监控指标数据
- 单击下图中的**显示统计分析**后面的<img src="https://qcloudimg.tencent-cloud.cn/raw/dde18545656758e343c3ec19099f62ce.png" style="zoom:50%;" />，以表格形式展示每一个监控指标最大值、最小值、平均值的统计数据。
  ![](https://qcloudimg.tencent-cloud.cn/raw/acbed97fab46af985dfbd18edfa01523.png)
- 在任一监控视图的右上角，单击<img src="https://qcloudimg.tencent-cloud.cn/raw/1ae8fbf920c91e7fc2b1caad2022eecd.png" style="zoom: 50%;" />，以表格形式展示该监控指标最大值、最小值、平均值的统计数据。
请参见下图，以**网络使用量**为例。
![](https://qcloudimg.tencent-cloud.cn/raw/8f8d632745bead98b62dd4e38f6d2184.png)

#### 通过图表联动查看监控数据
开启图表联动功能，适用于分析一个监控视图的数据同步分析与其相关联的监控视图。

1. 在**性能趋势**页签右上方，单击**图表联动**后面的<img src="https://qcloudimg.tencent-cloud.cn/raw/dde18545656758e343c3ec19099f62ce.png" style="zoom:33%;" />。
2. 在需分析的任一监控类别的监控视图上，选择时间点并单击，其他监控视图将固定显示相同时间的监控图表数据。
3. 单击监控视图右上角的**撤销固定**可取消固定。
![img](https://qcloudimg.tencent-cloud.cn/raw/47b690c8cb3c1cd4a4e5fdff8c8ecd76.png)

#### 自定义监控指标对比分析
在任一监控视图右上角，单击<img src="https://qcloudimg.tencent-cloud.cn/raw/b71f9ac5a20130276b98f188345f0db6.png" style="zoom:50%;" />，可添加其他类型的监控指标项进行对比查看分析。
![](https://qcloudimg.tencent-cloud.cn/raw/4c493cf9c9dfd744e46632b5b96fe9b0.png)

#### 切换监控视图单列/双列显示模式。
单击右上角的图标联动右侧的<img src="https://qcloudimg.tencent-cloud.cn/raw/fffff5c980c476e903a35c4b5659b22c.png" style="zoom:50%;" />，可切换单列模式和双列模式的显示。单列模式请参见下图。
![](https://qcloudimg.tencent-cloud.cn/raw/76409901331ba51070907b5710ccfa90.png)

#### 自由拖动监控视图位置
监控视图之间可以随意拖动，您可根据运维场景灵活调整监控视图的先后顺序，便于高效查看分析。

#### 放大监控视图
拉动任一监控视图右下角的图标，可以任意拉伸放大图片，便于更加清晰地投放展示指标的变化趋势图。
![](https://qcloudimg.tencent-cloud.cn/raw/732985ec960628dc9b2885cb23be3d9c.png)
