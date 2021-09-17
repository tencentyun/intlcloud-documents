## Overview

This document describes the schemes for migrating a self-built Kafka cluster to a CKafka cluster. You can choose an appropriate scheme according to your own business scenarios.

## Scheme Description

### Scheme 1. Single-Producer dual-consumer

This scheme is simple, clear, and easy to implement, with no data heap for smooth transition.

![](https://main.qcloudimg.com/raw/51d15605b01dd1095239001a966b2671.png)



**Scheme ideas:**

1. [Migrate the topic metadata](https://intl.cloud.tencent.com/document/product/597/41380).
2. Keep the original consumer in the self-built Kafka cluster intact.
3. Start a new consumer in CKafka and configure the bootstrap-server of the new CKafka cluster for consumption.
4. Wait for all consumers to listen on the new CKafka cluster.
5. Switch the production of the self-built cluster to the new CKafka cluster (by configuring the bootstrap-server of the new CKafka cluster).
6. Deactivate the original consumer in the self-built Kafka cluster after it finishes consuming the remaining data in the cluster.

**Pros and cons of the scheme:**

- Pros: the overall migration process is simple, clear, and easy to implement, with no data heap for smooth transition.
- Cons: an additional consumer is required.



### Scheme 2. Single-Producer single-consumer

This scheme is simple, clear, and easy to implement.

![](https://main.qcloudimg.com/raw/d25503d1d258cc9266c816daded70029.png)

**Scheme ideas:**

1. [Migrate the topic metadata](https://intl.cloud.tencent.com/document/product/597/41380).
2. Switch the production of the self-built Kafka cluster to the new CKafka cluster (by configuring the bootstrap-server of the new CKafka cluster).
3. Wait for the consumer in the self-built cluster to consume the remaining data.
4. Switch the old consumer to the new CKafka cluster for consumption (by configuring the bootstrap-server of the new CKafka cluster).

**Pros and cons of the scheme:**

- Pros: the overall migration process is simple, clear, and easy to implement for smooth transition.
- Cons: after the production is switched to the CKafka cluster, before the old consumer is switched to the CKafka cluster, there will be a certain amount of data heap in the CKafka cluster.



### Scheme 3. Migration with MirrorMaker

This scheme migrates the existing data in the self-built Kafka cluster to CKafka.

![](https://main.qcloudimg.com/raw/faa4c766dfd74e86da605ffdb0410b24.png)

**Scheme ideas:**

1. [Migrate the topic metadata](https://intl.cloud.tencent.com/document/product/597/41380).
2. Keep the original consumer in the self-built Kafka cluster intact.
3. Start the data sync feature of [MirrorMaker](https://intl.cloud.tencent.com/document/product/597/41381).
4. Wait for the data sync to complete, modify the consumer configuration, and switch the consumer.
5. Wait for the data sync to complete, modify the producer configuration, and switch the producer.
6. The migration is completed.

**Pros and cons of the scheme:**

- Pros: the overall migration process is simple, clear, and easy to implement, where historical data can be synced to the CKafka cluster.
- Cons: the consumer needs to consume data from the beginning after switch to the destination cluster, so consumption idempotency must be ensured.
