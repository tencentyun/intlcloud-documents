You can configure common parameters by modifying the YML parameter configuration of your Tencent Cloud Elasticsearch Service (ES) instance.

## Directions
### Viewing configuration item
Log in to the [ES Console](https://console.cloud.tencent.com/es), click the **ID/name of the cluster** for which to modify the configuration to enter the cluster details page, and then click **Advanced configuration** to view configuration item parameters.
![](https://main.qcloudimg.com/raw/ef01a6daf2bed529adb747a8566c6ec1.jpg)

### Modifying configuration item
Click **Modify Configuration** to modify the corresponding configuration item. For restrictions on the configuration item input, please see the "Value Description" column in the table. **More Configurations** support YML syntax, so you can customize the settings of other configuration items.
![](https://main.qcloudimg.com/raw/1e866568aacfb0ee160c31038142ab40.jpg)
Click **Confirm** and the new configuration item parameter will be applied to your cluster. Checking "Aware of the risks but still want to force restart" will restart the cluster. If there are replicas of the indices in your cluster, although the restart will not affect your business, we recommend you perform the restart during off-peak hours.
> !If the cluster health status is YELLOW or RED, or there is an index in the cluster that has no replicas, you will be prompted to force restart if you try to modify the configuration items. In this case, there will be a high risk if you update the configuration, and you are recommended to repair the cluster status first by adding replicas to all indices.
> 
If you are aware of the risk and still want to update the configuration, you can check the "Force Restart" box and click **Confirm** to restart. For more information, please see the figure below:
![](https://main.qcloudimg.com/raw/f9607265bdd9dc0fc0517a49fa87b574.jpg)
Then, the Tencent Cloud ES instance will restart. During the restart, you can check the progress in the cluster change history. After the restart succeeds, the YML file configuration will be completed.

## Supported Parameters

| Parameter | Description | Default Value |
| ----------------------------------- | ------------------------------------------ | ------ |
| indices.fielddata.cache.size | Specifies the percentage of Java heap space allocated to the field data | 15% |
| indices.query.bool.max_clause_count | Specifies the maximum number of clauses allowed in a Lucene Boolean query | 1024 |

## Hot Update-Enabled Parameters

| Parameter | Description | Valid Values |
| -------------------------------- | ------------------------------ | ------------------------------ |
| action.destructive_requires_name | Specifies whether it is required to specify the index name when deleting an index | true or false. Default value: true |

## Reindex Allowlist Configuration

| Parameter | Description | Default Value |
| ------------------------ | ------------------------ | ------ |
| reindex.remote.whitelist | Allowlist of remote ES cluster access addresses | `[]` |

## Custom Queue Size

| Parameter | Description | Default Value |
| ----------------------------- | --------------------------------------- | ------ |
| thread_pool.bulk.queue_size | Document write queue size, which is applicable to v5.6.4 | 1024 |
| thread_pool.write.queue_size | Document write queue size, which is applicable to v6.4.3 and above | 1024 |
| thread_pool.search.queue_size | Document search queue size | 1024 |

## Custom CORS Access Configuration

| Parameter | Description | Default Value |            
| --------------------------- | ------------------------------------------------------------ | ---------------------------------------------- | 
| http.cors.enabled | Cross-origin resource sharing (CORS) configuration item. `true` indicates to enable CORS, while `false` indicates to disable it | false |                          
| http.cors.allow-origin | Origin resource configuration item, which indicates the domain names allowed for access requests | `""` | 
| http.cors.max-age | Cache period of the obtained CORS configuration information in the browser | 1728000 (20 days) | 
| http.cors.allow-methods | Allowed request methods for CORS | `OPTIONS,HEAD,GET,POST,PUT,DELETE` |              
| http.cors.allow-headers | Request header information allowed for CORS | `X-Requested-With,Content-Type,Content-Length` |                          
| http.cors.allow-credentials | Specifies whether to allow `Access-Control-Allow-Credentials` information to be returned in the response header | false |                   

## Watcher Configuration

| Parameter | Description | Default Value |
| --------------------- | --------------------------------- | ------ |
| xpack.watcher.enabled | `true` indicates to enable the Watcher feature of X-Pack | true |

For more information on the configuration items, please see [Elasticsearch official documentation](https://www.elastic.co/guide/en/elasticsearch/reference/5.6/index.html). If you want to customize other configuration items, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
