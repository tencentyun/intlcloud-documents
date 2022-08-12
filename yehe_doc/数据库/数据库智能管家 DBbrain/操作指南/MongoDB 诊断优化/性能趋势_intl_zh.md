## 功能描述

性能趋势为您提供 MongoDB 数据库的如下实时监控信息，通过这些信息，帮您定位到耗时命令、耗时命令执行时间、总体延迟分布等。
- 资源监控：CPU、内存、存储空间、流量。
- 请求统计：请求耗时分布、请求类型分布、延时10 - 50毫秒请求类型分布、延时50 - 100毫秒请求类型分布、延时100毫秒以上请求类型分布、TTL 请求统计、活跃 Session 数量、请求延迟。
- MongoDB 主从复制：从节点复制延迟、oplog 保存时长。
- 存储引擎：Cache、qr/qw、ar/aw。

## 查看性能趋势

1. 登录 [DBbrain 控制台](https://console.cloud.tencent.com/dbbrain)，在左侧导航选择**诊断优化**，在上方选择对应数据库，然后选择**性能趋势**页。
2. 设置性能趋势监控维度和指标。  
   - 监控维度：支持 MongoDB 实例监控、MongoDB 节点监控。
![](https://qcloudimg.tencent-cloud.cn/raw/f3ca724dfe9f42a98f210445902b8ec8.png)
      - 实例维度：展现实例的监控视图。
      - 节点维度：MongoDB 节点间，各指标的趋势对比查看。
   - 指标分类：CPU、内存、磁盘、连接、流量、请求统计。
   - 性能指标选择方式：提供了全部指标、自定义指标，也支持多种视图的查看。
     - 全局指标过滤
       ![](https://qcloudimg.tencent-cloud.cn/raw/c73bd25a48ff2ded73da46b541716777.png)
     - 单个指标过滤
       ![](https://qcloudimg.tencent-cloud.cn/raw/7a4a58d54c5e8a9a948b4315f2ea5b25.png)
     - 图表视图切换
      ![](https://qcloudimg.tencent-cloud.cn/raw/ac31c930d5e9d030e0e940573fe1e52a.png)
3. 切换实时/历史视图。
   DBbrain 提供实时/历史切换，根据时间视图的不同，也提供不同的监控粒度切换，同时也支持单个或多个对比视图的查看。
   自定义多节点对比图。
    ![](https://qcloudimg.tencent-cloud.cn/raw/0741af9306a6324fdc78230ee24fbad5.png)
4. 开启图表联动。
   针对单个实例、单个节点、单个 Proxy，提供相关指标的联动对比趋势查看，也可添加自定义指标，还支持性能指标趋势的时间对比查看。
   开启图表联动后，鼠标悬浮在任一监控图上的数据点，其他监控图会显示同一个时间的数据。单击后可固定数据显示，如需取消固定，单击图片上的**撤销固定**即可。
   ![](https://qcloudimg.tencent-cloud.cn/raw/c548dde8155b9dde7c3ed9eed2ebb40b.png)
5. 切换单列/双列显示模式，自由拖动监控图位置，放大监控图。
   - **切换单列/双列显示模式**：单击右上角的图标联动右侧的按钮，可切换单列模式和双列模式的显示。
   - **自由拖动监控图位置**：不同监控图之间可以随意拖动位置，鼠标单击监控图的边框部位即可拖动。
   - **放大监控图**：拉动监控图右下小角的图标，可以放大图片，对单性能指标趋势进行更加清晰的细粒度查看。
6. 查看 MongoDB 节点状态，详情请参考 [MongoStaus](https://intl.cloud.tencent.com/document/product/1035/48617) 、[MongoTop](https://intl.cloud.tencent.com/document/product/1035/48616)。
7. 查看延迟分析数据。
    性能趋势查询结果示例如下，单击图中的数据点均可显示详细的指标数据。
   - 请求耗时分布示例：
     ![](https://qcloudimg.tencent-cloud.cn/raw/4636f59f739bf4bcf05737135e478e28.png)
   - 延时100毫秒以上请求类型分布示例：
     ![](https://qcloudimg.tencent-cloud.cn/raw/a0e7481925609b55dd7bb0aa4a74331a.png)
   - 请求延迟示例：
     ![](https://qcloudimg.tencent-cloud.cn/raw/99b790fa508daafa72e0e88d4ee61bb8.png)
     
     
