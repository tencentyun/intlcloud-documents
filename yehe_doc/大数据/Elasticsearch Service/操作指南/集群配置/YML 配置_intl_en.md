### Viewing Configuration Items

On the cluster list page, click a cluster ID to enter the cluster details page and click **Advanced Configuration** to view the YML configuration.
![](https://main.qcloudimg.com/raw/ef01a6daf2bed529adb747a8566c6ec1.jpg)

| Configuration Item | Description | Value Range |
| ----------------------------------- | ------------------------------------------ | ------------------------------------ |
| action.destructive_requires_name | Specifies whether it is required to specify the index name when deleting an index | true or false. Default value: true |
| indices.fielddata.cache.size | Specifies the percentage of Java heap space allocated to the field data | Percentage in the format of 1-100%. Default value: 15% |
| indices.query.bool.max_clause_count | Specifies the maximum number of clauses allowed in a Lucene Boolean query | Positive integer. Default value: 1024 |

For more information on the configuration items, please see [Elasticsearch official documentation](https://www.elastic.co/guide/en/elasticsearch/reference/5.6/index.html).

### Modifying Configuration Item
Click **Batch Modify** to modify configuration items. Applicable restrictions are as described above.  
![](https://main.qcloudimg.com/raw/1e866568aacfb0ee160c31038142ab40.jpg)
>!If the cluster health status is YELLOW or RED, or there is an index in the cluster that has no replicas, you will be prompted to force restart if you try to modify the configuration items. In this case, there will be a high risk if you update the configuration, and you are recommended to repair the cluster status first by adding replicas to all indices.

If you are aware of the risk and still want to update the configuration, you can check the "Force Restart" box and click **OK** to restart. For more information, please see the figure below:
![](https://main.qcloudimg.com/raw/f9607265bdd9dc0fc0517a49fa87b574.jpg)
Click **Batch Modify** to modify the corresponding configuration items. Applicable restrictions are as described above.  
![](https://main.qcloudimg.com/raw/b6ac02245130fe6751a73b4c16f23c71.jpg)
If you want to customize other configuration items, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).