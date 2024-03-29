 TDMQ CMQ 版提供类似于 Kafka 的消息回溯能力，使用消息回溯功能您可在业务成功消费并删除消息后重新消费已删除的消息。

本文为您介绍 TDMQ CMQ 版消息回溯功能的概念，应用场景和使用方法。

## 功能说明

![](https://qcloudimg.tencent-cloud.cn/raw/683c8ba135048e68c88d93eb3a2ebb0f.png)
如上图，消息的生命周期为蓝色框内的片段。开启消息回溯能力后，已被消费者消费且确认删除的消息会进入**消息可回溯**区域，TDMQ CMQ 版后端还会保存该信息。但消息超过 Queue 的消息生命周期时（假设为1天），达到生命周期后，该消息会自动删除，不可回溯。

### 产品逻辑

- **开启：**若未开启消息回溯能力，则消费者已消费且确认删除的消息会立即删除。开启该功能时，须指定回溯的可回溯周期，可回溯周期的范围必须小于等于消息的生命周期。

- **里程碑：**根据上一条策略，开启消息回溯后，随着消费者的不断消费及删除，可回溯的消息数量会不断增多。

- **关闭：**关闭消息回溯后，消息可回溯区域的消息将被立即删除，且不可回溯。

- **队列属性：**消息回溯是 Queue 的属性，可在创建时或在修改配置处进行设置。指定回溯（rewind）的时间点后，所有消费者都会从该时间点的消息往后消费。

- **计费：**开启消息回溯能力后，可回溯部分的消息会产生一定的堆积费用，单位价格与消息堆积的费用共同计算。

- **指定回溯时间点：**消费者发起回溯消费，需要指定 Queue Name 及具体的回溯时间。且从最远的时间点，往回回溯。时间为 key，不可逆向消费。 如图所示，只能从 timeA 到 timeB/timeC 消费，不支持反向消费。

- **指定回溯时间范围：**0 - 15天，控制台开启该能力后，删除的消息才可被回溯。建议关键应用，长期开启消息回溯能力。且消息回溯周期，与消息生命周期设成一致。

- **不可指定堆积中的消息回溯：**若消息仍在堆积中，未被消费，则无法指定某一个具体的位置进行消费。

### 可回溯范围

消息可回溯范围以消息生产的时间为排序标准，与被删除的先后无关。

1. 最远可回溯时间点 = current_time - rewind_seconds（消息回溯保留周期）
2. 最近可回溯时间点 = min_msg_time （队列最小未消费消息）
3. 最远时间点 ≤ start_consume_time ≤ 最近时间点

## 应用场景

此功能便于核心金融业务做业务对账、业务系统重试等操作。

## 典型案例

这里结合一个场景来描述消息回溯的使用：

假设有 A/B 两个业务，正常的生产消费场景，A 生产消息投递到队列中，B 从队列中消费消息，A/B 这时已经实现互相解耦，双方互不关心。A 只需要生产消息投递即可，B 从队列中拿到消息，然后将消息从队列中删除，接着在本地消费消息。

如果出现了异常，例如 B 业务虽然进行了消费，但是在一段时间内消费情况都出现了异常。这时，已经删除的消息已经被删除，无法重新消费，会对业务造成影响，且需要暂停 B 业务，等开发运维人员修复 Bug 之后才能重新上线 B 业务。而且运维人员也无法实时监控 B 业务的情况，等到发现异常场景，可能已经过去一段时间。

为了防止这种情况出现，A 业务需要关心 B 业务的处理情况，需要对生产消息进行备份，确保 B 业务正常才能删除备份，保证现网正常。

这种情况下，您可以使用 **消息回溯** 的功能，开发人员对 B 业务进行修复，然后根据 B 业务消费正常的最近一个时间点，将消息回溯到该时间点。这时候，B 业务获取到的消息就会从指定的时间点开始，A 业务完全不用关心 B 业务的异常情况。这里 B 需要注意要对消费进行幂等处理。

### 开启消息回溯功能

在 [TDMQ CMQ 版控制台](https://console.cloud.tencent.com/tdmq/cmq-queue) 新建队列的时候，您可以开启消息回溯功能。

![](https://qcloudimg.tencent-cloud.cn/raw/69ecb7ca62406731c997e8da0b99d5e3.png)



您也可以在队列详情页面开启消息回溯功能。

![](https://qcloudimg.tencent-cloud.cn/raw/b080265f5e8da66d67f0dc18e9d511e2.png)

在客户端设置消息回溯相关参数。

```java
endpoint='' //TDMQ CMQ 版的域名
secretId ='' // 用户的 ID 和 key
secretKey = ''
account = Account(endpoint,secretId,secretKey)
queueName = 'QueueTest'
my_queue = account.get_queue(queueName)
queue_meta = QueueMeta()
queue_meta.rewindSeconds = 43200 //消息允许回溯的时间，单位为秒
my_queue.create(queue_meta)
```

### 使用消息回溯

```java
my_queue.rewindQueue(1488718862) //指定本次消息回溯的时间点，为 Unix 时间戳
```

