腾讯云 Elasticsearch Service 提供了包括开源 ES 支持插件和自研插件在内的10余款插件，为您提供丰富的插件功能。当您购买了腾讯云 ES 实例后，您可以根据需求在插件列表页面安装或者卸载这些插件。本文介绍安装或卸载腾讯云 ES 插件的方法。

>!安装或者卸载插件将触发集群滚动重启，请确认后操作。

### 操作步骤
1. 登录 [腾讯云 Elasticsearch Service 控制台](https://console.cloud.tencent.com/es)。
2. 在集群列表页，单击集群 ID 进入集群详情页。
3. 单击【插件列表】，进入插件列表管理页面。
![](https://main.qcloudimg.com/raw/7c320711d9f98d7f754e79251ce378df.jpg)
4. 单击对应插件右侧操作栏下的安装或者卸载。
5. 在弹出的对话框中，阅读注意事项，确认无误后单击确认。确认后，插件变更操作开始，集群将会重启，可以在【集群变更记录】中查看变更进度。

### 插件信息

腾讯云 Elasticsearch Service 支持的插件如下：

| 插件名称           | 默认状态 | 描述                                                         | 支持的操作           |
| ------------------ | -------- | ------------------------------------------------------------ | -------------------- |
| analysis-icu       | 未安装   | Elasticsearch Unicode 文本分析插件                            | 安装、卸载           |
| analysis-ik        | 已安装   | Elasticsearch IK 分析插件，默认不能卸载。                     | 更新词典             |
| analysis-kuromoji  | 未安装   | Elasticsearch 日文分析插件                                    | 安装、卸载           |
| analysis-nori  | 未安装   | Elasticsearch 韩文分析插件                                   | 安装、卸载         |
| analysis-phonetic  | 未安装   | Elasticsearch 音标分析插件                                    | 安装、卸载           |
| analysis-pinyin    | 已安装   | Elasticsearch 拼音分析插件                                    | 安装、卸载           |
| analysis-qq        | 未安装   | Elasticsearch QQ 分析插件                                     | 安装、卸载、更新词典 |
| analysis-smartcn   | 未安装   | Elasticsearch 智能中文分析插件                                | 安装、卸载           |
| analysis-stconvert | 已安装   | Elasticsearch 繁简体分析插件                                  | 安装、卸载           |
| ingest-attachment  | 未安装   | Apache Tika 信息提取插件                                      | 安装、卸载           |
| ingest-geoip       | 未安装   | IP 地址解析插件，6.8.2以上版本已集成在 es 模块中，不需安装      | 安装、卸载           |
| ingest-user-agent  | 未安装   | 浏览器 user agent 信息提取插件，6.8.2以上版本已集成在 es 模块中，不需安装 | 安装、卸载           |
| mapper-murmur3     | 未安装   | 插件用于在创建索引时计算并存储字段的 hash 值                   | 安装、卸载           |
| mapper-size        | 未安装   | 插件用于在创建索引时记录文档压缩前的大小                     | 安装、卸载           |
| repository-cos     | 已安装   | 插件用于存储 Elasticsearch Snapshot 到腾讯云 COS，详见 [使用 COS 进行备份及恢复](https://intl.cloud.tencent.com/document/product/845/19549)，默认不能卸载 | 无                   |
| repository-hdfs    | 未安装   | 插件提供了对 Hadoop 分布式文件系统（HDFS）存储库的支持      | 安装、卸载           |
| sql             | 未安装   | 开源 SQL 解析插件，基础版、白金版集群已带 sql 解析功能，不需安装 | 安装、卸载           |

