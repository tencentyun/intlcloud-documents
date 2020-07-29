### 查看配置项

在集群列表页单击集群 ID 进入集群详情页，单击【高级配置】可以看到YML配置。
![](https://main.qcloudimg.com/raw/ef01a6daf2bed529adb747a8566c6ec1.jpg)

| 配置项                              | 说明                                       | 取值限制                             |
| ----------------------------------- | ------------------------------------------ | ------------------------------------ |
| action.destructive_requires_name    | 删除索引时是否需要明确索引名称             | true 或者 false，默认值为 true       |
| indices.fielddata.cache.size        | 指定分配到字段数据的 Java 堆空间的百分比   | 百分数，格式：1% - 100%，默认值为15% |
| indices.query.bool.max_clause_count | 指定 Lucene 布尔查询中允许的子句的最大数量 | 正整数，默认值为1024                 |

具体配置项详细含义，请查询 [Elasticsearch 官方文档](https://www.elastic.co/guide/en/elasticsearch/reference/5.6/index.html)。

### 修改配置项
单击【批量修改】，可对相应的配项进行修改，配置项的输入限制，见上文的说明。  
![](https://main.qcloudimg.com/raw/1e866568aacfb0ee160c31038142ab40.jpg)
>!如果集群健康状态为 YELLOW 或 RED，或集群存在无副本索引时，修改集群配置项对话框会有强制重启的提示和选项框，此时进行更新配置操作有较大风险，建议修复集群状态，为所有索引添加副本，再进行修改配置操作。

如果用户已了解该操作风险，仍要进行更新配置操作，可以勾选强制重启选项框，单击【确定】进行重启。详情参考下图：
![强制修改配置](https://main.qcloudimg.com/raw/f9607265bdd9dc0fc0517a49fa87b574.jpg)
单击【批量修改】，可对相应的配项就行修改，配置项的输入限制，见上文的说明。  
![](https://main.qcloudimg.com/raw/b6ac02245130fe6751a73b4c16f23c71.jpg)
如果有其他配置项自定义设置需求，请通过 [提交工单](https://console.cloud.tencent.com/workorder/category) 向我们进行反馈。