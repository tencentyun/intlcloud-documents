On the cluster list page and in the basic information section on the cluster details page, you can view the status information of the cluster.
![](https://main.qcloudimg.com/raw/fc9882d5985397c260d7441117fe8d60.jpg)
![](https://main.qcloudimg.com/raw/279b5c35b2bcc5a1ada5118aa61f3459.jpg)
The cluster status is a metric that reflects whether the cluster is being changed or running normally as described below:

| Status | Description |
|---------|---------|
| Normal | The cluster has been created and can be accessed and used normally with no operations such as configuration change or cluster restart in progress. |
| Processing | This is the status when an operation such as cluster creation, cluster configuration change, or cluster restart that takes time to complete is being processed. During this period, access to some services will be affected, such as Kibana, data storage, and query. |

The health status is one of the most important monitoring metrics in the ES cluster, which is used to indicate whether the cluster is working normally. Health status divides into the following:

| Color | Health Status |
|-------|-------------|
| Green | All master and replica shards are running normally. |
| Yellow | All master shards but not all replica shards are running normally. |
| Red | Some master shards are not running normally. |

For more information, please see [Cluster Health](https://www.elastic.co/guide/en/elasticsearch/reference/5.6/_cluster_health.html).
