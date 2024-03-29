## 操作场景

本文为您介绍从零开始创建一个队列服务并使用 Java SDK 进行收发消息测试的方法，帮助您快速了解客户端接入 TDMQ CMQ 版所需的基本操作。

## 前提条件

已 [注册腾讯云账号](https://intl.cloud.tencent.com/document/product/378/17985)。

## 操作步骤

### 步骤1：创建队列服务

1. 登录 [TDMQ CMQ 版控制台](https://console.cloud.tencent.com/tdmq/cmq-queue)。
2. 在左侧导航栏选择**队列服务**，选择地域后，单击**新建**，配置队列服务相关属性值。
   <img src="https://qcloudimg.tencent-cloud.cn/raw/bca2e55dcc0172d192894f345fcfc291.png" width="550px">
<table>
    <thead>
    <tr>
        <th>属性</th>
        <th>说明</th>
        <th>取值</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>队列名称</td>
        <td>QueueName，为队列的名称。</td>
        <td>作为资源的唯一标识，调用 API 接口进行操作时，以 Queue name
            为准，创建成功后无法修改。不区分大小写，相同字母即会判定为同名，并不能以 -retry 和 -dlq 结尾。
        </td>
    </tr>
    <tr>
        <td>
            <nobr>资源标签</nobr>
        </td>
				<td>选填，标签可以帮助您从各种维度方便地对 TDMQ CMQ 版资源进行分类管理，具体使用方法可参见 <a href = "https://intl.cloud.tencent.com/document/product/1111/43007">标签管理</a>。</td>
        <td>-</td>
    </tr>		
    <tr>
        <td>消息最长未确认时间</td>
        <td>如果消费客户端在获取到消息后超过此时间仍未进行消息的确认，则服务端会自动确认该消息。</td>
        <td>范围在30秒到12小时</td>
    </tr>
    <tr>
        <td>消息接收长轮询等待时间</td>
        <td>PollingWaitSeconds，长轮询等待时，一个消息消费请求只会在取到有效消息或长轮询超时时才返回响应，类似于 Ajax 请求的长轮询。</td>
        <td>范围在0秒到30秒，推荐设置为3秒，设置过高可能造成消息重复的概率提升。</td>
    </tr>
    <tr>
        <td>取出消息隐藏时长</td>
        <td>
            该项为队列的 VisibilityTimeout 属性，每条 Message 都有个默认的VisibilityTimeout，Worker 在接收到消息后，timeout 就开始计时了。如果 Worker 在 timeout 时间内没能处理完 Message，那么消息就有可能被其他 Worker 接收到并处理。
        </td>
        <td>范围在1秒到12小时</td>
    </tr>
    <tr>
        <td>不可见消息数量上限</td>
        <td>不可见消息过多一般是客户端未及时 ACK 导致的，产生不可见消息会消耗一定的内存，因此为每个队列设置了一定的容量上限。</td>
        <td>100000条，如需提升额度，请联系技术支持。</td>
    </tr>
     <tr>
        <td>消息堆积容量上限</td>
        <td>消息堆积一般是生产速率大于消费速率或者消费出现阻塞导致的，产生堆积会消耗一定的磁盘存储，因此为每个队列设置了一定的容量上限。</td>
        <td>10GB，如需提升额度，请联系技术支持。</td>
    </tr>
    <tr>
        <td>死信队列</td>
        <td>死信队列用于处理无法被正常消费的消息。达到最大重试次数后，若消费依然失败，则表明消费者在正常情况下无法正确地消费该消息，此时，MQ 不会立刻将消息丢弃，而是将其发送到该消费者对应的特殊队列中。
        </td>
        <td>-</td>
    </tr>
    <tr>
        <td>消息回溯</td>
        <td>若未开启“消息回溯”能力，则消费者已消费，且确认删除的消息，会立即删除，开启该功能时，须指定回溯的“可回溯周期”。</td>
        <td>“可回溯周期”的范围，必须小于等于消息的生命周期。建议将回溯周期与消息的生命周期设置为相同的值，便于定位问题。</td>
    </tr>
    <tr>
        <td>可回溯时间范围</td>
        <td>若开启“消息回溯”能力，则消费者确认删除的消息不会立即删除，会持续保存到此处配置的最大时间。</td>
        <td>时间范围：1天 - 15天，设置较长可能会产生昂贵的存储费用。最大可回溯时间点 = 当前时间 - 设置的可回溯时间范围。消息生产时间在这个值之前的不可回溯。</td>
    </tr>
    <tr>
        <td>可回溯存储空间</td>
        <td>开启回溯消息后，如果持久存储的消息超过此最大存储空间，则会从后向前删除（优先删除旧数据）。</td>
        <td>存储空间范围：1GB - 10GB，设置较大可能会产生昂贵的存储费用。</td>
    </tr>
    </tbody>
</table>
3. 单击**提交**，在队列服务列表可以看到创建好的队列服务。

### 步骤2：使用 SDK 收发消息

> ?以下示例以 Java 语言客户端说明，其他语言客户端接入请参见 [SDK 文档](https://intl.cloud.tencent.com/document/product/1111/46396)。

1. [下载 Demo ](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/cmq/tdmq-cmq-Java-sdk-demo.zip)并解压。
2. 引入 CMQ 客户端相关依赖
<dx-codeblock>
:::  xml
<!-- cmq sdk --><!-- cmq sdk -->
<dependency>
​    <groupId>com.qcloud</groupId>
​    <artifactId>cmq-http-client</artifactId>
​    <version>1.0.7</version>
</dependency>

<!-- 云API sdk -->
<dependency>
​    <groupId>com.tencentcloudapi</groupId>
​    <artifactId>tencentcloud-sdk-java</artifactId>
​    <version>3.1.423</version>
</dependency>
:::
</dx-codeblock>
3. 发送消息
<dx-codeblock>
:::  java
Account account = new Account(SERVER_ENDPOINT, SECRET_ID, SECRET_KEY);
Queue queue = account.getQueue(queueName);
String msg = "hello client, this is a message. Time:" + new Date();
CmqResponse response = queue.send(msg);
:::
</dx-codeblock>
<table>
<tr>
<th>参数</th>
<th>说明</th>
</tr>
<tr>
<td>SERVER_ENDPOINT</td>
<td>API 调用地址，在 <a href = "https://console.cloud.tencent.com/tdmq">TDMQ CMQ 版控制台</a> 的<b>队列服务</b> > <b>API 请求地址</b>处复制。
<img src="https://qcloudimg.tencent-cloud.cn/raw/fc16b1951c00d63b0f86cf8f4c25691c.png">
</td>
</tr>
<tr>
<td>SECRET_ID、SECRET_KEY</td>
<td>云 API 密钥，登录 <a href = "https://console.cloud.tencent.com/cam/overview">访问管理控制台</a>，在<b>访问密钥</b> > <b>API 密钥管理</b>页面复制。
<img src = "https://qcloudimg.tencent-cloud.cn/raw/0def1c292b3dc79a320e3fc9921a979e.png">
</td>
</tr>
<tr>
<td>queueName</td>
<td>队列名称，在 <a href = "https://console.cloud.tencent.com/tdmq">TDMQ CMQ 版控制台</a> 的<b>队列服务</b>列表页面获取。</td>
</tr>
</table>
4. 消费消息
<dx-codeblock>
:::  java
   Account account = new Account(SERVER_ENDPOINT, SECRET_ID, SECRET_KEY);
   Queue queue = account.getQueue(queueName);
   Message message = queue.receiveMessage();
   // 消费成功，删除消息。未删除的消息，将在一定时间后可重新投递
   queue.deleteMessage(message.receiptHandle);
:::
</dx-codeblock>
<table>
<tr>
<th>参数</th>
<th>说明</th>
</tr>
<tr>
<td>SERVER_ENDPOINT</td>
<td>API 调用地址，在 <a href = "https://console.cloud.tencent.com/tdmq">TDMQ CMQ 版控制台</a> 的<b>队列服务</b> > <b>API 请求地址</b>处复制。
<img src = "https://qcloudimg.tencent-cloud.cn/raw/fc16b1951c00d63b0f86cf8f4c25691c.png">
</td>
</tr>
<tr>
<td>SECRET_ID、SECRET_KEY</td>
<td>云 API 密钥，登录 <a href = "https://console.cloud.tencent.com/cam/overview">访问管理控制台</a>，在<b>访问密钥</b> > <b>API 密钥管理</b>页面复制。
<img src = "https://qcloudimg.tencent-cloud.cn/raw/0def1c292b3dc79a320e3fc9921a979e.png">
</td>
</tr>
<tr>
<td>queueName</td>
<td>队列名称，在 <a href = "https://console.cloud.tencent.com/tdmq">TDMQ CMQ 版控制台</a>的<b>队列服务</b>列表页面获取。</td>
</tr>
</table>


>?以上是 CMQ 的生产和消费方式的简单介绍，更多操作可参见 [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/cmq/tdmq-cmq-Java-sdk-demo.zip)。
