## Flume Overview
Apache Flume is a highly available, distributed, and configurable tool/service that collects data resources such as logs and events and aggregates large amounts of such data from different sources. It is designed to collect data flows (e.g., log data) from various web servers and store them in centralized data stores like HDFS and HBase.

### Flume Architecture
A Flume event is defined as a unit of data flow. A Flume agent is a JVM process that contains the components required for completing a task. Among them, the three core ones are Source, Channel, and Sink.
![](https://main.qcloudimg.com/raw/886ecba4612fa557b9316b4ff74bd4e3.png)

- **Source**
It consumes an event passed to it by an external source (e.g., web servers or other sources) and save it to one or more channels.
- **Channel**
Located between a source and a sink, a channel is used to cache incoming events. After the sink successfully sends the events to the channel at the next hop or the final destination, the events are removed from the channel.
- **Sink**
A sink is responsible for transferring the events to the next hop or final destination and removing them from the channel upon transfer completion.

## Instructions

### Preparations
- An EMR cluster has been created. When [creating the EMR cluster](https://intl.cloud.tencent.com/document/product/1026/31099), you need to select the Impala component on the software configuration page.
- Impala is installed in the `/usr/local/service/flume` path on the core and task nodes of the EMR cluster.

### Configuring Flume 
```
 # example.conf: A single-node Flume configuration
 
 # Name the components on this agent
 a1.sources = r1
 a1.sinks = k1
 a1.channels = c1
 
 # Describe/configure the source
 a1.sources.r1.type = netcat
 a1.sources.r1.bind = localhost
 a1.sources.r1.port = 44444
 
 # Describe the sink
 a1.sinks.k1.type = logger
 
 # Use a channel which buffers events in memory
 a1.channels.c1.type = memory
 a1.channels.c1.capacity = 1000
 a1.channels.c1.transactionCapacity = 100
 
 # Bind the source and sink to the channel
 a1.sources.r1.channels = c1
 a1.sinks.k1.channel = c1
```

### Starting Flume
```bash
bin/flume-ng agent --conf conf --conf-file example.conf --name a1 -Dflume.root.logger=INFO,console
```

### Configuring a Test Sample
```bash
telnet localhost 44444
Trying 127.0.0.1...
Connected to localhost.localdomain (127.0.0.1).
Escape character is '^]'.
Hello world! <ENTER>
OK
```
After successful configuration, you will see the Flume agent started previously printing to the terminal.
