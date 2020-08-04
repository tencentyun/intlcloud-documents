If you want to migrate your Elasticsearch cluster built in Tencent Cloud or purchased from another cloud vendor to Tencent Cloud ES, you can choose a suitable migration solution based on your business needs. If your business can be paused for write operations, you can migrate your data using the following tools:

* elasticsearch-dump
* snapshot
* reindex
* logstash

## elasticsearch-dump

### Use cases

Applicable to scenarios where the amount of data is small and there are only a few indices to be migrated.

### How to use
elasticsearch-dump is an open-source Elasticsearch data migration tool available on [GitHub](https://github.com/taskrabbit/elasticsearch-dump).
1. Install elasticsearch-dump
elasticsearch-dump is developed using Node.js and can be installed directly using the npm package manager:
```
npm install elasticdump -g
```
2. Main Parameters
```
  --input: the source address in the format of {protocol}://{host}:{port}/{index}, which can be an Elasticsearch cluster URL, file, or stdin and allows you to specify an index
  --input-index: the index in the source cluster
  --output: the target address in the format of {protocol}://{host}:{port}/{index}, which can be an Elasticsearch cluster URL, file, or stdout and allows you to specify an index
  --output-index: the index in the target cluster
  --type: the migration type, which is data by default, indicating that only data will be migrated. Value range: settings, analyzer, data, mapping, alias
```
3. Migrate a single index
 The following operation migrates the `companydatabase` index in the `172.16.0.39` cluster to the `172.16.0.20` cluster by running the `elasticdump` command.
 > The first command migrates the settings of the index. If you directly migrate the mapping or data, the configuration information of the index in the source cluster will be lost, such as the number of shards and number of replicas. Of course, you can also directly create an index in the target cluster first before syncing the mapping and data.
 >
```
elasticdump --input=http://172.16.0.39:9200/companydatabase --output=http://172.16.0.20:9200/companydatabase --type=settings
elasticdump --input=http://172.16.0.39:9200/companydatabase --output=http://172.16.0.20:9200/companydatabase --type=mapping
elasticdump --input=http://172.16.0.39:9200/companydatabase --output=http://172.16.0.20:9200/companydatabase --type=data
```
4. Migrate all indices
The following operation migrates all the indices in the `172.16.0.39` cluster to the `172.16.0.20` cluster by running the `elasticdump` command.
> This operation cannot migrate the configurations of indices, such as the number of shards and number of replicas. You must migrate the configuration of each index separately, or directly create an index in the target cluster first before migrating the data.
>
```
elasticdump --input=http://172.16.0.39:9200 --output=http://172.16.0.20:9200
```

## snapshot
### Use cases
Suitable for migrating a large amount of data.

### How to use
The snapshot API is an API used by Elasticsearch to back up and restore data. You can use it to migrate data from one cluster to another by creating a snapshot of the data in the source cluster and then restoring it to the target cluster.
>The major version number of the target cluster (such as 5 in 5.6.4) should be greater than or equal to that of the source cluster. A snapshot created from a 1.x cluster cannot be restored to a 5.x cluster.

1. Create a repository in the source cluster
Before creating a snapshot, you must create a repository, which can contain multiple snapshot files. There are several types of repositories as detailed below:
 - fs: a shared file system where snapshot files are stored.
 - url: the URL path to a specified file system, which supports HTTP, HTTPS, FTP, file, and jar protocols.
 - s3: AWS S3. The snapshot is stored in S3, which is supported as a plugin, so the [repository-s3](https://www.elastic.co/guide/en/elasticsearch/plugins/current/repository-s3.html) plugin should be installed.
 - hdfs: the snapshot is stored in HDFS, which is supported as a plugin, so the [repository-hdfs](https://www.elastic.co/guide/en/elasticsearch/plugins/current/repository-hdfs.html) plugin should be installed.
 - cos: the snapshot is stored in COS, which is supported as a plugin, so the [elasticsearch-repository-cos](https://github.com/tencentyun/elasticsearch-repository-cos) plugin should be installed.

 **To migrate your data from a self-built Elasticsearch cluster to a Tencent Cloud ES cluster**, you can directly use an fs repository, but you need to set the repository path in the `elasticsearch.yml` configuration file.
```
path.repo: ["/usr/local/services/test"]
```
Then, call the snapshot API to create a repository.
```
curl -XPUT http://172.16.0.39:9200/_snapshot/my_backup -H 'Content-Type: application/json' -d '{
      "type": "fs",
  "settings": {
   "location": "/usr/local/services/test"
   "compress": true
  }
}'
```
**To migrate your data from an Elasticsearch cluster provided by another cloud vendor to a Tencent Cloud ES cluster or between ES clusters**, you can use the corresponding repository type provided by the cloud vendor, such as S3 by AWS, OSS by Alibaba Cloud, and COS by Tencent Cloud.
```
curl -XPUT http://172.16.0.39:9200/_snapshot/my_s3_repository
{
  "type": "s3",
"settings": {
  "bucket": "my_bucket_name",
  "region": "us-west"
}
}
```
2. Create a snapshot in the source cluster
You can call the snapshot API to create a snapshot in the created repository. When creating a snapshot, you can specify an index or the contents of the snapshot. For more information on API parameters, please see [Snapshot and Restore](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/modules-snapshots.html).
```
curl -XPUT http://172.16.0.39:9200/_snapshot/my_backup/snapshot_1?wait_for_completion=true
```
3. Create a repository in the target cluster
Creating a repository in the target cluster is similar to creating a repository in the source cluster. You can create a COS bucket in Tencent Cloud for storing the repository.
4. Move the snapshot created in the source cluster to the repository in the target cluster
Upload the snapshot created in the source cluster to the repository created in the target cluster.
5. Restore data from the snapshot
```
curl -XPUT http://172.16.0.20:9200/_snapshot/my_backup/snapshot_1/_restore
```
6. View the status of snapshot restoration
```
curl http://172.16.0.20:9200/_snapshot/_status
```

## reindex
The reindex API provided by Elasticsearch allows you to migrate data by importing data from the source cluster to the current cluster; however, this can be implemented only in Elasticsearch and is not supported by the current version. The following describes how to use the reindex API:
1. Configure the `reindex.remote.whitelist` parameter
You need to configure this parameter in the target cluster to specify the allowlist of remote clusters that can be reindexed.
2. Call the reindex API
The following operation involves querying the index named `test1` by `elasticsearch` in the `title` field from the source cluster and writing the result to the `test2` index of the current cluster.
```
POST _reindex
{
"source": {
   "remote": {
  "host": "http://172.16.0.39:9200"
   },
   "index": "test1",
   "query": {
  "match": {
       "title": "elasticsearch"
  }
    }
},
    "dest": {
    "index": "test2"
}
}
```

## logstash
Logstash allows you to read data from an Elasticsearch cluster and then write it to another cluster; therefore, you can use Logstash for data migration. The specific configuration file is as follows:
```
input {
elasticsearch {
hosts => ["http://172.16.0.39:9200"]
index => "*"
docinfo => true
}
}
output {
elasticsearch {
hosts => ["http://172.16.0.20:9200"]
index => "%{[@metadata][_index]}"
}
}
```
The above configuration file syncs all the indices in the source cluster to the target cluster, and it can also be set to only sync specified indices. For more information on the features of Logstash, please see [Configuring Logstash](https://www.elastic.co/guide/en/logstash/6.4/configuration.html).

## Summary
1. When elasticsearch-dump or Logstash is used to migrate data from one cluster to another, the machine used to perform the migration task is required to have access to both clusters at the same time, because migration cannot be performed if there is no network connection. This limitation does not apply if snapshot is used, as it is completely offline. Therefore, elasticsearch-dump and Logstash are more suitable for migrating data between clusters on the same network. If you want to migrate your data between cloud vendors, such as from an Alibaba Cloud Elasticsearch cluster to a Tencent Cloud ES cluster, you can use snapshot or establish a connection between the vendors to achieve cluster connectivity, which, however, is costly.
2. elasticsearchdump is similar to MySQL's mysqldump which is used for data backup, and both of them perform logical backup that involves exporting data entries one by one and then importing them. Therefore, this tool is suitable for migrating a small amount of data.
3. Snapshot is suitable for migrating a large amount of data.
