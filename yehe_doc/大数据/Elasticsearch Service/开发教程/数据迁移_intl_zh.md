用户在腾讯云上自建的 ES 集群或者在其它云厂商购买的 ES 集群，如果要迁移至腾讯云 ES，用户可以根据自己的业务需要选择合适的迁移方案。如果业务可以停服或者可以暂停写操作，可以使用以下几种方式进行数据迁移：

* elasticsearch-dump
* snapshot
* reindex
* logstash

## elasticsearch-dump

### 适用场景

适用于数据量不大，迁移索引个数不多的场景。

### 使用方式
elasticsearch-dump 是一款开源的 ES 数据迁移工具，[github 地址](https://github.com/taskrabbit/elasticsearch-dump)。
1. 安装 elasticsearch-dump
	elasticsearch-dump 使用 node.js 开发，可使用 npm 包管理工具直接安装：
```
npm install elasticdump -g
```
2. 主要参数说明
```
  --input: 源地址，可为 ES 集群 URL、文件或 stdin,可指定索引，格式为：{protocol}://{host}:{port}/{index}
  --input-index: 源 ES 集群中的索引
  --output: 目标地址，可为 ES 集群地址 URL、文件或 stdout，可指定索引，格式为：{protocol}://{host}:{port}/{index}
  --output-index: 目标 ES 集群的索引
  --type: 迁移类型，默认为 data，表明只迁移数据，可选 settings, analyzer, data, mapping, alias
```
3. 迁移单个索引
 以下操作通过 elasticdump 命令将集群172.16.0.39中的 companydatabase 索引迁移至集群172.16.0.20。
 >第一条命令先将索引的 settings 先迁移，如果直接迁移 mapping 或者 data 将失去原有集群中索引的配置信息如分片数量和副本数量等，当然也可以直接在目标集群中将索引创建完毕后再同步 mapping 与 data。
 >
```
	elasticdump --input=http://172.16.0.39:9200/companydatabase --output=http://172.16.0.20:9200/companydatabase --type=settings
	elasticdump --input=http://172.16.0.39:9200/companydatabase --output=http://172.16.0.20:9200/companydatabase --type=mapping
	elasticdump --input=http://172.16.0.39:9200/companydatabase --output=http://172.16.0.20:9200/companydatabase --type=data
```
4. 迁移所有索引
以下操作通过 elasticdump 命令将集群172.16.0.39中的所有索引迁移至集群172.16.0.20。 
>此操作并不能迁移索引的配置，例如分片数量和副本数量，必须对每个索引单独进行配置的迁移，或者直接在目标集群中将索引创建完毕后再迁移数据。
>
```
elasticdump --input=http://172.16.0.39:9200 --output=http://172.16.0.20:9200
```

## snapshot
### 适用场景
适用数据量大的场景。

### 使用方式
snapshot api 是 ES 用于对数据进行备份和恢复的一组 api 接口，可以通过 snapshot api 进行跨集群的数据迁移，原理就是从源 ES 集群创建数据快照，然后在目标 ES 集群中进行恢复。
>目标 ES 集群的主版本号（如5.6.4版本中的5为主版本号）要大于等于源 ES 集群的主版本号。1.x 版本的集群创建的快照不能在 5.x 版本中恢复。

1. 源 ES 集群中创建 repository
创建快照前必须先创建 repository 仓库，一个 repository 仓库可以包含多份快照文件，repository 主要有以下几种类型：
 - fs：共享文件系统，将快照文件存放于文件系统中。
 - url：指定文件系统的 URL 路径，支持协议：http、https、ftp、file、jar。
 - s3：AWS S3 对象存储，快照存放于 S3 中，以插件形式支持，安装插件 [repository-s3](https://www.elastic.co/guide/en/elasticsearch/plugins/current/repository-s3.html)。
 - hdfs：快照存放于 hdfs 中，以插件形式支持，安装插件 [repository-hdfs](https://www.elastic.co/guide/en/elasticsearch/plugins/current/repository-hdfs.html)。
 - cos：快照存放于腾讯云 COS 对象存储中，以插件形式支持，安装插件 [elasticsearch-repository-cos](https://github.com/tencentyun/elasticsearch-repository-cos)。

 **从自建 ES 集群迁移至腾讯云 ES 集群**，可直接使用 fs 类型仓库，但需要在 ES 配置文件 elasticsearch.yml 中设置仓库路径。
```	
path.repo: ["/usr/local/services/test"]
```
然后调用 snapshot api 创建 repository。
```
curl -XPUT http://172.16.0.39:9200/_snapshot/my_backup -H 'Content-Type: application/json' -d '{
      "type": "fs",
  	"settings": {
   		"location": "/usr/local/services/test" 
   		"compress": true
	  }
}'
```
**从其它云厂商的 ES 集群迁移至腾讯云 ES 集群，或腾讯云内部的 ES 集群迁移**，可使用对应云厂商提供的仓库类型，例如 AWS 的 S3、阿里云的 OSS 和腾讯云的 COS 等。
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
2. 源 ES 集群中创建 snapshot
调用 snapshot api 在创建好的仓库中创建快照。创建快照可以指定索引，也可以指定快照中包含的内容，具体的 api 接口参数可以查阅 [官方文档](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/modules-snapshots.html)。
```	
curl -XPUT http://172.16.0.39:9200/_snapshot/my_backup/snapshot_1?wait_for_completion=true
```
3. 目标 ES 集群中创建 repository
目标 ES 集群中创建仓库和在源 ES 集群中创建仓库类似，用户可在腾讯云上创建 COS 对象 bucket，把仓库建在 COS 的某个 bucket 下。
4. 移动源 ES 集群 snapshot 至目标 ES 集群的仓库
把源 ES 集群创建好的 snapshot 上传至目标 ES 集群创建好的仓库中。
5. 从快照恢复
```
curl -XPUT http://172.16.0.20:9200/_snapshot/my_backup/snapshot_1/_restore
```
6. 查看快照恢复状态
```
curl http://172.16.0.20:9200/_snapshot/_status
```

## reindex
reindex 是 ES 提供的一个 api 接口，可以把数据从源 ES 集群导入到当前 ES 集群，实现数据的迁移。但仅限于 ES 的实现方式，当前版本不支持 reindex 操作。下面简单介绍 reindex 接口的使用方法：
1. 配置 reindex.remote.whitelist 参数
需要在目标 ES 集群中配置该参数，指明能够 reindex 的远程集群的白名单。
2. 调用 reindex api
以下操作表示从源 ES 集群中查询名为 test1 的索引，查询条件为 title 字段为 elasticsearch，将结果写入当前集群的 test2 索引。
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
logstash 支持从一个 ES 集群中读取数据然后写入到另一个 ES 集群，因此可以使用 logstash 进行数据迁移，具体的配置文件如下：
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
上述配置文件将源 ES 集群的所有索引同步到目标集群中，同时也可以设置只同步指定的索引，logstash 的更多功能可查阅 [logstash 官方文档](https://www.elastic.co/guide/en/logstash/6.4/configuration.html)。

## 总结
1. elasticsearch-dump 和 logstash 做跨集群数据迁移时，都要求用于执行迁移任务的机器可以同时访问到两个集群，因为网络无法连通的情况下无法实现迁移。而使用 snapshot 的方式则没有这个限制，因为 snapshot 方式是完全离线的。因此 elasticsearch-dump 和 logstash 迁移方式更适合于源 ES 集群和目标 ES 集群处于同一网络的情况下进行迁移。而需要跨云厂商的迁移，可以选择使用 snapshot 的方式进行迁移，例如从阿里云 ES 集群迁移至腾讯云 ES 集群，也可以通过打通网络实现集群互通，但是成本较高。
2. elasticsearchdump 工具和 MySQL 数据库用于做数据备份的工具 mysqldump 类似，都是逻辑备份，需要将数据一条一条导出后再执行导入，所以适合数据量小的场景下进行迁移。
3. snapshot 的方式适合数据量大的场景下进行迁移。
