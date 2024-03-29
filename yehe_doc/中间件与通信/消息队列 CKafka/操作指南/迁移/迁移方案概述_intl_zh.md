## 操作场景

本文档为您总体介绍将自建 Kafka 集群迁移到 CKafka 集群的可行方案，您可以根据自身业务场景选择合适您的迁移方案。

## 方案说明

### 方案1：单写双消费

该方案的整体简单清晰便于操作，且无数据积压，过渡平滑。

![](https://main.qcloudimg.com/raw/51d15605b01dd1095239001a966b2671.png)



**方案思路：**

1. [完成 Topic 元数据的迁移](https://intl.cloud.tencent.com/document/product/597/41380)。
2. 自建 Kafka 集群中原有的消费者保持不动。
3. CKafka 消费端新起消费者，配置新的 CKafka 集群的 bootstrap-server，消费新的 CKafka 集群。
4. 等待所有消费端都已经监听了新的 CKafka 集群。
5. 将自建集群的生产切到 CKafka 新集群上（配置新的 CKafka 集群的 bootstrap-server）。
6. 自建 Kafka 集群中原有的消费者继续消费自建 Kafka 集群中剩余的数据，直到消费干净后方可下线原消费者。

**方案优劣：**

- 优点：整体迁移流程简单清晰便于操作，无数据积压，平滑过渡。
- 缺点：需要额外多起一套消费者。



### 方案2：单写单消费

该方案的整体简单清晰便于操作。

![](https://main.qcloudimg.com/raw/d25503d1d258cc9266c816daded70029.png)

**方案思路：**

1. [完成 Topic 元数据的迁移](https://intl.cloud.tencent.com/document/product/597/41380)。
2. 将自建 Kafka 集群的生产切到 CKafka 新集群上 (配置新的 CKafka 集群的 bootstrap-server)。
3. 等待自建集群中的消费者消费完剩余数据。
4. 将老的消费者切到 CKafka 新集群消费（配置新的 CKafka 集群的 bootstrap-server）。

**方案优劣：**

- 优点：整体迁移流程简单清晰便于操作，过渡平滑。
- 缺点：在生产切到 CKafka 集群后，旧消费切到 CKafka 集群之前， CKafka 集群会存在一定量的堆积。



### 方案3：Mirrormaker 迁移

该方案会把自建集群 Kafka 中的存量数据迁移到 CKafka。

![](https://main.qcloudimg.com/raw/faa4c766dfd74e86da605ffdb0410b24.png)

**方案思路：**

1. [完成 Topic 元数据的迁移](https://intl.cloud.tencent.com/document/product/597/41380)。
2. 自建 Kafka 集群中原有的消费者保持不动。
3. 启动[ Mirrormaker 工具](https://intl.cloud.tencent.com/document/product/597/41381)的数据同步功能。
4. 等待数据同步完成，修改消费者配置并切换消费者。
5. 等待数据同步完成，修改生产者配置并切换生产者。
6. 迁移完成。

**方案优劣：**

- 优点：整体迁移流程简单清晰便于操作、可以把历史数据同步到 CKafka 集群。
- 缺点：消费者切换到目的集群上需要从头开始消费，需要做好消费幂等。
