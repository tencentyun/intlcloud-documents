## 功能描述

Redis 性能趋势支持多种性能指标的选择，实例（Redis 数据库实例）、Redis 节点（节点间，如A节点 - B节点之间）、Proxy（中间件集群节点）节点切换，性能指标选择，实时/历史视图切换，监控粒度切换，单个或对比视图切换，实例、Redis 节点、Proxy 节点的多种视图及对比视图等。

## 支持的性能指标

DBbrain 当前支持的腾讯云 Redis 数据库性能指标监控如下：

<table>
<tr><th>类别</th><th>类别子项</th><th>指标名称</th></tr>
    <tr><td rowspan=7>资源监控</td>
<td>CPU</th><td>CPU</td></tr>
<tr>
<td rowspan=2 >内存</td>
<td>内存</td></tr>
<tr><td>内存占用</td></tr>
<tr>
<td rowspan=2>存储空间</td>
<td>存储利用率</td></tr>
<tr><td>存储使用空间</td></tr>
<tr>
<td rowspan=2>流量</td>
<td>输出流量</td></tr>
<tr><td>输入流量</td></tr>
<tr>
<tr><td rowspan=13>Redis</td>
<td>Key 信息</th><td>Key 信息（总数、过期数、驱逐数）</td></tr>
<tr>
<td rowspan=2 >内存</td>
<td>内存使用量</td></tr>
<tr><td>内存使用率</td></tr>
<tr>
<td rowspan=1>复制延迟</td>
<td>复制延迟情况</td></tr>
<tr>
<td rowspan=1>网络用量</td>
<td>网络使用量</td></tr>
<tr>
<td rowspan=4>请求</td>
<td>总请求</td></tr>
<tr><td>读请求</td></tr>
<tr><td>写请求</td></tr>
<tr><td>其他请求</td></tr>
<tr>
<td rowspan=4>响应</td>
<td>慢查询</td></tr>
<tr><td>读请求命中</td></tr>
<tr><td>读请求 Miss</td></tr>
<tr><td>读请求命中率</td></tr>
<tr>
<tr><td rowspan=23>proxy</td>
<td>CPU</th><td>CPU 使用率</td></tr>
<tr>
<td rowspan=2 >流量</td>
<td>入流量</td></tr>
<tr><td>出流量</td></tr>
<tr>
<td rowspan=5>请求</td>
<td>总请求</td></tr>
<tr><td>Key 请求</td></tr>
<tr><td>Mget 请求</td></tr>
<tr><td>执行错误</td></tr>
<tr><td>大 Value 请求</td></tr>
<tr>
<td rowspan=4>网络用量</td>
<td>连接数</td></tr>
<tr><td>每秒建连数</td></tr>
<tr><td>每秒断连数</td></tr>
<tr><td>每秒异常连数</td></tr>
<tr>
<td rowspan=5>网络用率</td>
<td>连接使用率</td></tr>
<tr><td>入流量使用率</td></tr>
<tr><td>出流量使用率</td></tr>
<tr><td>入流量限流触发</td></tr>
<tr><td>出流量限流触发</td></tr>
<tr>
<td rowspan=6>时延</td>
<td>平均执行时延</td></tr>
<tr><td>最大执行时延</td></tr>
<tr><td>P99 执行时延</td></tr>
<tr><td>读平均时延</td></tr>
<tr><td>写平均时延</td></tr>
<tr><td>其他命令平均时延</td></tr>
</tbody></table>

## 查看性能趋势

1. 登录 [DBbrain 控制台](https://console.cloud.tencent.com/dbbrain)，在左侧导航选择**诊断优化**，在上方选择对应数据库，选择**性能趋势**页。
   
2. 设置监控指标。  
   - 指标分类：CPU、内存、网络、时延、请求、响应。
   - 性能指标选择方式：提供了全部指标、自定义指标，也支持多种视图的查看。
     - 全局指标过滤
       ![](https://qcloudimg.tencent-cloud.cn/raw/2f57f8179bc1a0bb5254f12775ee6302.png)
     - 单个指标过滤
       ![](https://qcloudimg.tencent-cloud.cn/raw/c8c0b91ba2546aa97d1a960a061c21fa.png)
     - 图表视图切换
       ![](https://qcloudimg.tencent-cloud.cn/raw/c9c080f6f598bf0ebcadcae9522b45a5.png)   
3. 设置监控维度。
   监控维度支持 Redis 实例监控、Redis 节点监控、Proxy 节点监控。 
    - 实例：展现整个实例的监控视图。
    - Redis 节点：展示节点间，各指标的趋势对比查看。
    - Proxy 节点维度：展现各个 Proxy 里，有相关性的指标对比趋势查看。  
   当选择 Proxy 节点维度时，支持选择聚合视图和节点视图模式。
   - **聚合视图**模式中，显示所有 Proxy 节点信息，需要在左上方选择具体查看的指标，然后展示所有节点的单个指标信息。单击每个指标的**详情**可以跳转到**节点视图**。
     ![](https://qcloudimg.tencent-cloud.cn/raw/4ddbcd931e487408ae55d4a9ee4f9df0.png)
   - **节点视图**模式中，展示单个节点的所有监控指标信息。
      ![](https://qcloudimg.tencent-cloud.cn/raw/c549143800cc6366654d482e86bcac90.png)
4. 切换实时/历史视图。
   DBbrain 提供实时/历史切换，根据时间视图的不同，也提供不同的监控粒度切换，同时也支持单个或对比视图的查看。
5. 开启图表联动。  
   针对单个实例、单个节点、单个 Proxy，提供相关指标的联动对比趋势查看，也可添加自定义指标，还支持性能指标趋势的时间对比查看。
   开启图表联动后，鼠标悬浮在任一监控图上的数据点，其他监控图会显示同一个时间的数据。单击后可固定数据显示，如需取消固定，单击图片上的**撤销固定**即可。
![](https://qcloudimg.tencent-cloud.cn/raw/f306800350c58f544135f622ff098f47.png)  
6. 显示统计分析。
   指标监控图中支持同步展示具体的监控数据，开启**显示统计分析**，每个监控图下会展示相应的表数据。
   ![](https://qcloudimg.tencent-cloud.cn/raw/54733e708e0e6617ba45ef22d11c2de1.png)
7. 切换单列/双列显示模式，自由拖动监控图位置，放大监控图。
   - **切换单列/双列显示模式**：单击右上角的图标联动右侧的按钮，可切换单列模式和双列模式的显示。
     ![](https://qcloudimg.tencent-cloud.cn/raw/ca4757c9f39a3ee954710cd041269692.png)
   - **自由拖动监控图位置**：不同监控图之间可以随意拖动位置，鼠标单击监控图的边框部位即可拖动。
   - **放大监控图**：拉动监控图右下小角的图标，可以放大图片，对单性能指标趋势进行更加清晰的细粒度查看。
   ![](https://qcloudimg.tencent-cloud.cn/raw/66a644cc813bd68c20320f63f3008573.png)

