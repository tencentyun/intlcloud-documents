Stream Connector provides a Sink plug-in for Flume through which data in Flume can be uploaded to Stream Connector. 

First, install the standard Flume (1.7.0 or above), then create a plugins.d directory under the Flume root directory, and decompress the Sink plug-in to the plugins.d directory. After decompression, you can find the flume-datapipeline-sink directory under the plugins.d directory, with lib and libtext in it.

The specific configuration of Stream Connector's Flume Sink component is described below:
type: Must be configured as  com.tencent.cloud.datapipeline.flume.sink.DataPipelineSink
datapipeline.appID: AppId in Tencent Cloud
datapipeline.secretID: SecretId in Tencent Cloud
datapipeline.secretKey: SecretKey in Tencent Cloud
datapipeline.endPoint: URL for uploading data
Datapipeline.project: Project name
Datapipeline.topic: Topic name
batchSize: Pieces of data uploaded at a time

Here is an example of the complete configuration of Flume (the third paragraph shows the specific configurations of the plug-in):
```
agent-1.channels.ch-1.type = memory
agent-1.channels.ch-1.capacity = 100000
agent-1.channels.ch-1.transactionCapacity = 100000
	
agent-1.sources.avro-source1.channels = ch-1
agent-1.sources.avro-source1.type = avro
agent-1.sources.avro-source1.bind = 0.0.0.0
agent-1.sources.avro-source1.port = 41414
agent-1.sources.avro-source1.threads = 50

//Specific configuration of the plug-in
agent-1.sinks.log-sink1.channel = ch-1
agent-1.sinks.log-sink1.type = com.tencent.cloud.datapipeline.flume.sink.DataPipelineSink
agent-1.sinks.log-sink1.datapipeline.appID = 1251966477
agent-1.sinks.log-sink1.datapipeline.secretID = sfhwu4545654634n3nf3f34t4g
agent-1.sinks.log-sink1.datapipeline.secretKey = fegreghgrfbrj5u7674wh4h54hg
agent-1.sinks.log-sink1.datapipeline.endPoint = http://10.66.89.217
agent-1.sinks.log-sink1.datapipeline.project = internal_test
agent-1.sinks.log-sink1.datapipeline.topic = internal
agent-1.sinks.log-sink1.batchSize = 5000
  
agent-1.channels = ch-1
agent-1.sources = avro-source1
agent-1.sinks = log-sink1
```	

Besides using Flume mentioned above, you can also call SDK to transfer data to Stream Connector. 

