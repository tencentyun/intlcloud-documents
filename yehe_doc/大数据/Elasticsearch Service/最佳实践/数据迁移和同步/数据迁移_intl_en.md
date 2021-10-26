If you want to migrate your Elasticsearch cluster built in Tencent Cloud or purchased from another cloud vendor to Tencent Cloud ES, you can choose a suitable migration solution based on your business needs. If your business can be paused for write operations, you can migrate your data using the following tools:
- COS snapshot
- Logstash
- elasticsearch-dump

The migration methods are compared as follows:

<table>
<tr>
<th>Migration Method</th>
<th>Use Case</th>
</tr>
<tr>
<td>COS snapshot</td>
<td><li>Scenarios with high volumes of data (gigabyte, terabyte, or petabyte scale)</li><li>Scenarios with higher requirement for migration speed</li> </td>
</tr>
<tr>
<td>Logstash</td>
<td><li>Scenarios where full or incremental data is migrated with a lower requirement for real-timeliness</li><li>Scenarios where data to be migrated needs to be simply filtered with query operations of Elasticsearch</li><li>Scenarios where data to be migrated requires complicated filtering and processing</li><li>Scenarios where data is migrated across versions with a large gap, such as migration from 5.x to 6.x or 7.x</td>
</tr>
<tr>
<td>elasticsearch-dump</td>
<td>Scenarios with small volumes of data</td>
</tr>
</table>

## COS Snapshot
COS snapshot-based migration is to use the snapshot API of ES for migration. Its basic process is to create an index snapshot from the source Elasticsearch cluster and then restore it to the target ES cluster. If you migrate data with snapshot, you should pay special attention to the Elasticsearch version:
```
The major version number of the target cluster (such as 5 in 5.6.4) should be greater than or equal to that of the source cluster.
A snapshot created from a 1.x cluster cannot be restored to a 5.x cluster.
```

### Creating repository in source cluster
Before creating a snapshot, you must create a repository, which can contain multiple snapshot files. There are several types of repositories as detailed below:
- fs: a shared file system where snapshot files are stored.
- url: the URL path to a specified file system, which supports HTTP, HTTPS, FTP, file, and JAR protocols.
- s3: the snapshot is stored in AWS S3, which is supported as a plugin. You can install the plugin as instructed in [S3 Repository Plugin](https://www.elastic.co/guide/en/elasticsearch/plugins/current/repository-s3.html).
- hdfs: the snapshot is stored in HDFS, which is supported as a plugin. You can install the plugin as instructed in [Hadoop HDFS Repository Plugin](https://www.elastic.co/guide/en/elasticsearch/plugins/current/repository-hdfs.html).
- cos: the snapshot is stored in COS, which is supported as a plugin. You can install the plugin as instructed in [COS Repository for Elasticsearch](https://github.com/tencentyun/elasticsearch-repository-cos).
	
If you want to migrate data from your Elasticsearch cluster to a Tencent Cloud ES cluster, you can directly use a COS repository, but you need to install the cos-repository plugin in your Elasticsearch cluster first (the plugin can be used only after the cluster is restarted). Then, back up the data of your Elasticsearch cluster to COS and restore the backup to the Tencent Cloud ES cluster to complete data migration.

If it is inconvenient to install the cos-repository plugin in your Elasticsearch cluster, but the repository-s3 or repository-hdfs plugin has already been installed, you can back up the data to S3 or HDFS first, upload the backup files from S3 or HDFS to COS, and then restore the data to the Tencent Cloud ES cluster.
	
To migrate data with COS snapshot, you need to create a COS repository first by running the following command:
```
PUT _snapshot/my_cos_backup
{
    "type": "cos",
    "settings": {
        "app_id": "xxxxxxx",
        "access_key_id": "xxxxxx",
        "access_key_secret": "xxxxxxx",
        "bucket": "xxxxxx",
        "region": "ap-guangzhou",
        "compress": true,
        "chunk_size": "500mb",
        "base_path": "/"
    }
}
```
	
- app_id: APPID of your Tencent Cloud account.
- access\_key\_id: `SecretId` of your TencentCloud API key.
- access\_key\_secret: `SecretKey` of your TencentCloud API key.
- bucket: COS bucket name, which should not contain the `-{appId}` suffix.
- region: COS bucket region, which must be same as the region of your ES cluster.
- base_path: backup directory.   
	
### Creating snapshot in source cluster
You can call the snapshot API to create a snapshot so as to back up the index data. When creating a snapshot, you can specify to back up certain or all indices. For more information on specific API parameters, please see [Snapshot and Restore](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/modules-snapshots.html).

#### Backing up all indices
Back up all indices in the source cluster to the `my_cos_backup` repository and name the snapshot `snapshot_1`:
```
PUT _snapshot/my_cos_backup/snapshot_1
```
This command will be returned immediately and executed asynchronously in the background until the end. If you want to block the execution of the snapshot creating command, you can add the `wait_for_completion` parameter:
```
PUT _snapshot/my_cos_backup/snapshot_1?wait_for_completion=true
```
>!The time it takes to execute the command depends on the index size.

#### Backing up specified index
You can specify the index to be backed up when creating a snapshot:
```
PUT _snapshot/my_cos_backup/snapshot_2
{
    "indices": "index_1,index_2"
}
```
>!If the value of the parameter `indices` contains multiple indices, they should be separated by `,` with no spaces.


### Viewing snapshot status
You can run the following command to check whether the snapshot backup has been completed. If the `state` field is `SUCCESS` in the returned result, the backup has been completed:
```
GET _snapshot/my_cos_backup/snapshot_1
```

### Creating repository in target cluster
Creating a repository in the target cluster is exactly the same as that in the source cluster.
	
### Restoring data from snapshot
Restore all indices backed up in the snapshot to the ES cluster:
```
POST _snapshot/my_cos_backup/snapshot_1/_restore
```
If snapshot_1 contains 5 indices, then all of them will be restored to the ES cluster. You can also rename the indices through an additional option which allows you to match the index name by pattern and provide a new name through the restoration process. Use this option if you want to restore old data to verify the content or perform other operations without replacing existing data. Restore a single index from a snapshot and provide an alternate name:
```
POST /_snapshot/my_cos_backup/snapshot_1/_restore
{
    "indices": "index_1",
    "rename_pattern": "index_(.+)",
    "rename_replacement": "restored_index_$1"
}
```
- indices: only restores `index_1` and ignores other indices in the snapshot.
- rename_pattern: finds the index being restored that can be matched by the specified pattern.
- rename_replacement: renames the matching index to the name specified in this parameter.   

	
### Viewing index restoration status
You can call the `_recovery` API to view the restoration progress of the specified index:
```
GET index_1/_recovery
```
In addition, you can call the following API to view the status of the specified index. If `status` is `green` in the returned result, the index has been completely restored:
```
GET _cluster/health/index_1
```

## Logstash
Logstash allows you to read data from an Elasticsearch cluster and then write it to another cluster; therefore, you can use Logstash for data migration. Before using Logstash to migrate data, you need to pay attention to the following:
- You need to create a CVM instance for Logstash deployment in the same VPC as the Tencent Cloud ES cluster and make sure that the CVM instance can access the source Elasticsearch cluster.
- You'd better choose a high-specced CVM instance to deploy Logstash; for example, you can use a CVM instance with 16 CPU cores and 32 GB memory.
- The major version number of Logstash should be the same as that of the target ES cluster; for example, if the target ES cluster version is 6.8.2, the Logstash version should also be 6.8.
- You need to pay special attention to the index type. As Elasticsearch's constraints on index type vary by version, during migration across major versions, problems such as failure in writing data to the target cluster may occur due to index type issues. For more information, please see the description of the [`document_type`](https://www.elastic.co/guide/en/logstash/current/plugins-outputs-elasticsearch.html#plugins-outputs-elasticsearch-document_type) parameter in the `logstash-output-elasticsearch` plugin.

A common configuration file for cross-cluster data migration with Logstash is as follows:
```
input {
    elasticsearch {
        hosts => "1.1.1.1:9200"
        index => "*"
        docinfo => true
        size => 5000
        scroll => "5m"
      }
}

output {
    elasticsearch {
        hosts => ["http://2.2.2.2:9200"]
        user => "elastic"
        password => "your_password"
        index => "%{[@metadata][_index]}"
        document_type => "%{[@metadata][_type]}"
        document_id => "%{[@metadata][_id]}"
    }
}
```
The above configuration file syncs all the indices in the source cluster to the target cluster, and it can also be set to only sync specified indices. For more information on migration with Logstash, please see [Elasticsearch input plugin](https://www.elastic.co/guide/en/logstash/current/plugins-inputs-elasticsearch.html) and [Elasticsearch output plugin](https://www.elastic.co/guide/en/logstash/current/plugins-outputs-elasticsearch.html).

## elasticsearch-dump
elasticsearch-dump is an open-source Elasticsearch data migration tool available on [GitHub](https://github.com/taskrabbit/elasticsearch-dump).
1. Install elasticsearch-dump
elasticsearch-dump is developed using Node.js and can be installed directly using the npm package manager:
```
npm install elasticdump -g
```
2. Main parameters
```
--input: the source address in the format of {protocol}://{host}:{port}/{index}, which can be an Elasticsearch cluster URL, file, or stdin and allows you to specify an index
--input-index: the index in the source cluster
--output: the target address in the format of {protocol}://{host}:{port}/{index}, which can be an Elasticsearch cluster URL, file, or stdout and allows you to specify an index
--output-index: the index in the target cluster
--type: the migration type, which is data by default, indicating that only data will be migrated. Value range: settings, analyzer, data, mapping, alias
```
3. If the cluster requires security authentication, you can use reindex to authenticate it as instructed below:
Add `user:password@` after the corresponding `http`. Please refer to the sample `elasticsearch-dump --input=http://192.168.1.2:9200/my_index --output=http://user:password@192.168.1.2:9200/my_index --type=data`.
3. Migrate a single index
 The following operation migrates the `companydatabase` index in the `172.16.0.39` cluster to the `172.16.0.20` cluster by running the `elasticdump` command.
>!The first command migrates the settings of the index. If you directly migrate the mapping or data, the configuration information of the index in the source cluster will be lost, such as the number of shards and number of replicas. Of course, you can also directly create an index in the target cluster first before syncing the mapping and data.
>
```
elasticdump --input=http://172.16.0.39:9200/companydatabase --output=http://172.16.0.20:9200/companydatabase --type=settings
elasticdump --input=http://172.16.0.39:9200/companydatabase --output=http://172.16.0.20:9200/companydatabase --type=mapping
elasticdump --input=http://172.16.0.39:9200/companydatabase --output=http://172.16.0.20:9200/companydatabase --type=data
```
4. Migrate all indices
The following operation migrates all indices in the `172.16.0.39` cluster to the `172.16.0.20` cluster by running the `elasticdump` command. 
>!This operation cannot migrate the configurations of indices, such as the number of shards and number of replicas. You must migrate the configuration of each index separately, or directly create an index in the target cluster first before migrating the data.
>
```
elasticdump --input=http://172.16.0.39:9200 --output=http://172.16.0.20:9200
```

## Summary
1. When elasticsearch-dump or Logstash is used to migrate data from one cluster to another, the machine used to perform the migration task is required to have access to both clusters at the same time, because migration cannot be performed if there is no network connection. This limitation does not apply if snapshot is used, as it is completely offline. Therefore, elasticsearch-dump and Logstash are more suitable for migrating data between clusters on the same network. If you want to migrate your data between cloud vendors, such as from an Alibaba Cloud Elasticsearch cluster to a Tencent Cloud ES cluster, you can use snapshot or establish a connection between the vendors to achieve cluster connectivity, which, however, is costly.
2. elasticsearch-dump is similar to MySQL's mysqldump which is used for data backup, and both of them perform logical backup that involves exporting data entries one by one and then importing them. Therefore, this tool is suitable for migrating a small amount of data.
3. Snapshot is suitable for migrating a large amount of data.
