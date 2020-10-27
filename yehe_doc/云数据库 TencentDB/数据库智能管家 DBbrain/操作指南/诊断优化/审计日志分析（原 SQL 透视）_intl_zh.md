审计日志分析（原 SQL 透视）对数据库实例进行深层次的 SQL 分析，以数据库一段时间内产生的审计日志为基础，对全量的 SQL 以及执行信息（来源信息、次数、执行时间、返回集合、扫描集合等）进行统计、抽样、聚合。

针对聚合后的 SQL 语句，根据其执行计划的结果，综合资源消耗、扫描和返回集合大小、索引使用合理性等，对 SQL 的性能进行分析，并针对低质量 SQL 结合索引情况、库表设计，给出优化建议。本文将介绍如何进行全量 SQL 分析，及查看分析详情。
>?审计日志分析目前支持云数据库 MySQL（不含基础版）。

## 前提条件
实例需要开通数据库审计功能。
![](https://main.qcloudimg.com/raw/767fcbcdcb5cfdc6d14ee4b4159d5dba.png)

## SQL 视图
登录 [DBbrain 控制台](https://console.cloud.tencent.com/dbbrain/slow-sql)，在左侧导航选择【诊断优化】，在上方选择【审计日志分析】页，可以查看所选数据库实例的 QPS 、慢查询次数、CPU 使用率。鼠标拖动下面的灰色滚动条，可拉伸该时间段的诊断视图，查看更细粒度的视图详情。
![](https://main.qcloudimg.com/raw/48b60d99ce8dfb1ca4199aa7d6433382.png)

## 创建任务
1. 选择所需时间段，单击视图右上角的【创建分析任务】。
![](https://main.qcloudimg.com/raw/a28ea22fd07b90ee1c1d12a86708f82d.png)
2. 选择任务开始时间和时间间隔，其中时间间隔支持分钟级别的粒度，单击【确定】。
![](https://main.qcloudimg.com/raw/23ea17396f234f8ae920076f0994a61d.png)
3. 创建完成后，可在任务列表查看分析结果和删除任务，单击操作列的【查看SQL分析】，进入 SQL 分析页。
![](https://main.qcloudimg.com/raw/77c67b4c07fc8ac44df6d7c41141f68d.png)

## SQL 分析
1. 在 SQL 分析页，可选择 SQL Type、Host、User 或 SQL Code 维度的视图，并可选择时间段拉伸视图来查看具体时间点的数据。下面表格中会展示该时间段内 SQL 的聚合详情以及执行信息（包括执行次数、总延迟、最大延迟、最小延迟、总影响行数、最大影响行数、最小影响行数等）。
 - 若对图中时间进行部分拉伸选中，表格中的 SQL 数据会随之变化，只显示图中时间范围内的 SQL 分析结果，拉伸后，单击右上角的【重置】，可以恢复原视图。
 - 图中“SQL Type”和“图例”均可进行单击筛选，表格中的 SQL 数据会随之变化，例如，只想查看 Select 请求，可将其余类型的图例点暗。
 - 在视图单击图表曲线可查看某时刻的监控数据，包括 Other、Select、Insert、Update、Delete、Replace 等不同的请求。
![](https://main.qcloudimg.com/raw/5b14b4fabbec59c0d6641f6b422884eb.png)
2. 单击某行 SQL 模板，在右侧会弹出 SQL 语句的详情。
 - 在分析页，可查看和复制具体 SQL 语句，根据给出的优化建议或说明来优化 SQL 语句。
 ![](https://main.qcloudimg.com/raw/9b6da50c4eaa6563662bad04a39291d6.png)
 在【分析】弹窗中，单击右上角的【优化对比】，可以查看 SQL 执行计划、索引建议、表结构以及 SQL 优化前后代价对比，SQL 代价通过可视化图表清晰反映了优化前后开销的变化。
 SQL 代价通过分析 SQL 相关库表的统计信息、OPTIMIZER_SWITCH 配置、及索引字段区分度进行估算，对优化后的 SQL 语句代价进行整体估计，使用可视化图表直观呈现 SQL 优化后降低的效果，您也可通过优化前后的执行计划比对进一步验证优化的效果。
 - 在统计页，可查看该类 SQL 在 Host、User、SQL Code 维度的统计分析和执行时间轨迹。
 ![](https://main.qcloudimg.com/raw/eafba7f6e63371511824abf00d03dbf3.png)

