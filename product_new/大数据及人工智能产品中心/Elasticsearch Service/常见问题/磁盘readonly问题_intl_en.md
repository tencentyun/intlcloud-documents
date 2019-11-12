Elasticsearch 5.6.4 does not have a disk capacity threshold that helps prevent the disk capacity from being used up. Therefore, if you use Elasticsearch 5.6.4, you are recommended to pay close attention to the disk utilization and delete useless indices or expand the disk capacity in a timely manner.

Elasticsearch 6.4.3 introduces the disk watermark threshold. When the disk utilization reaches `99%`, the indices on the disk that have shards will become read-only, and you won't be able to write data to these indices. You are recommended to clear indices or expand the disk capacity promptly when you find that the disk utilization is high.

### Issues

#### Creation of an index pattern timed out

After your cluster's disk status changes to read-only, you cannot create an index pattern on Kibana. This is because when the disk capacity is used up, ES will automatically set the block level of the index to `readonly_allow_delete`.

#### Error writing to an index

After your cluster's disk status changes to read-only, you cannot write data to an index even after clearing indices or expanding the disk capacity. The error is as follows:
* Index read-only error:
```
Elasticsearch exception [
    type=cluster_block_exception, 
    reason=blocked by: [FORBIDDEN/12/index read-only / allow delete (api)];
]
```

* Cluster read-only error:
```
Elasticsearch exception [
    type=cluster_block_exception, 
    reason=blocked by: [FORBIDDEN/13/cluster read-only / allow delete (api)];
]
```

### Solutions

You need to clear useless indices to free up storage space or expand the disk capacity first, and then run the following command in **Dev Tools** in the Kibana UI:
* Turn off index read-only status:
```
PUT _all/_settings
{
  "index.blocks.read_only_allow_delete": null
}
```

* Turn off cluster read-only status:
```
PUT _cluster/settings
{
  "persistent": {
    "cluster.blocks.read_only_allow_delete": null
  }
}
```
