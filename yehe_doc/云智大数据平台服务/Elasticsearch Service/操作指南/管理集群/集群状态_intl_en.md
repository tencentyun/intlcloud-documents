In the basic information section on the cluster list page and cluster details page, you can view the status information of your cluster.
![](https://main.qcloudimg.com/raw/fc9882d5985397c260d7441117fe8d60.jpg)
![](https://main.qcloudimg.com/raw/279b5c35b2bcc5a1ada5118aa61f3459.jpg)
Cluster status indicates whether a cluster is under change (Processing) or in normal use (Normal). The specific definitions are as follows:

| Status | Description | 
|---------|---------|
| Normal | The cluster has been created and can be normally accessed or used, and there are no ongoing operations such as configuration change or cluster restart. |
| Processing | There is an ongoing operation that takes a certain period of time to be processed, such as cluster creation, cluster restart, or cluster configuration change. During this period, access to some services, such as Kibana, data storage, and data query, will be affected. |

Health status is one of the key monitoring metrics of an ES cluster, which indicates whether the cluster works normally as a whole. It has the following possible values:

| Color | Health Status |
|-------|-------------|
| Green | All primary and replica shards are running normally. |
| Yellow | All primary shards are running normally, while some replica shards are exceptional. |
| Red | A primary shard is exceptional. |

For more information, please see [Cluster Health](https://www.elastic.co/guide/en/elasticsearch/reference/5.6/_cluster_health.html).
