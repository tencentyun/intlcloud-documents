## Directions

This document uses the SDK for PHP as an example to describe how to connect the client to TDMQ for CMQ and send/receive messages.

## Prerequisites

- [You have installed PHP 5.6 or later.](https://www.php.net/manual/en/install.php)
- [You have downloaded the demo.](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/cmq/tdmq-cmq-php-sdk-demo.zip)

## Queue Model
### Directions
1. Create a queue service in the console as instructed in [Queue Management](https://intl.cloud.tencent.com/document/product/1111/42994).
<dx-alert infotype="explain" title="">
You can create a message queue in the console or via TencentCloud API. To use TencentCloud API, you need to install the SDK 3.0 for PHP.
</dx-alert>
2. Add dependencies.
<dx-codeblock>
:::  shell
composer require tencentcloud/tencentcloud-sdk-php
:::
</dx-codeblock>
3. Add references.
<dx-codeblock>
:::  php
require '/path/to/vendor/autoload.php';
:::
</dx-codeblock>
4. Create a message queue.
<dx-codeblock>
:::  php
   $cred = new Credential($secretId, $secretKey);
   $httpProfile = new HttpProfile();
   $httpProfile->setEndpoint($endPoint);
   
   $clientProfile = new ClientProfile();
   $clientProfile->setHttpProfile($httpProfile);
   $client = new TdmqClient($cred, "ap-guangzhou", $clientProfile);
   
   $req = new CreateCmqQueueRequest();
   
   $params = array(
       "QueueName" => "queue_api",  // Message queue name
       // Below is the dead letter queue configuration
       "DeadLetterQueueName" => "dead_queue_api", // Dead letter queue name
       "Policy" => 0,  // Dead letter policy. 0: Message has been consumed multiple times but not deleted. 1: `Time-To-Live` has elapsed
       "MaxReceiveCount" => 3  // Maximum receipts. Value range: 1–1000
       // MaxTimeToLive: Maximum period in seconds before an unconsumed message expires, which is required if `policy` is 1. Value range: 300–43200. This value should be smaller than `msgRetentionSeconds` (maximum message retention period)
   );
   $req->fromJsonString(json_encode($params));
   
   $resp = $client->CreateCmqQueue($req);
:::
</dx-codeblock>
<table>
    <thead>
    <tr>
        <th>Parameter</th>
        <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>$endPoint</td>
        <td>API call address, which can be copied from <strong>Queue Service</strong> &gt; <strong>API Request Address</strong> in the <a href='https://console.intl.cloud.tencent.com/tdmq'>TDMQ for CMQ console</a>. <img src="https://main.qcloudimg.com/raw/397c634ac38494666e878caf69cf55e7.png"
            <strong>API 请求地址</strong>处复制。<img src="https://main.qcloudimg.com/raw/397c634ac38494666e878caf69cf55e7.png"
                                             referrerpolicy="no-referrer" alt="img"></td>
    </tr>
    <tr>
        <td>$secretId, $secretKey</td>
        <td>TencentCloud API key, which can be copied on the <strong>Access Key</strong> &gt; <strong>API Key Management</strong> page in the <a href='https://console.intl.cloud.tencent.com/cam/overview'>CAM console</a>. <img src="https://main.qcloudimg.com/raw/867837e2b1e6d347ecb04d7085938c08.png"
            <strong>API 密钥管理</strong>页面复制。<img src="https://main.qcloudimg.com/raw/867837e2b1e6d347ecb04d7085938c08.png"
                                              referrerpolicy="no-referrer" alt="img"></td>
    </tr>
    </tbody>
</table>
5. Import [CMQ files](https://github.com/tencentyun/cmq-php-sdk) into the project.
6. Send messages.
<dx-codeblock>
:::  php
// Message queue name
$queue_name = "php_queue";
// Authentication information
$my_account = new Account($this->endpoint, $this->secretId, $this->secretKey);

$my_queue = $my_account->get_queue($queue_name);

$queue_meta = new QueueMeta();
$queue_meta->queueName = $queue_name;
$queue_meta->pollingWaitSeconds = 10;
$queue_meta->visibilityTimeout = 10;
$queue_meta->maxMsgSize = 1024;
$queue_meta->msgRetentionSeconds = 3600;

try {
    // Message content
    $msg_body = "I am test message.";
    $msg = new Message($msg_body);
    // Send messages
    $re_msg = $my_queue->send_message($msg);
    echo "Send Message Succeed! MessageBody:" . $msg_body . " MessageID:" . $re_msg->msgId . "\n";
} catch (CMQExceptionBase $e) {
    echo "Create Queue Fail! Exception: " . $e;
    return;
}
:::
</dx-codeblock>
<table>
<thead>
<tr><th >Parameter</th><th >Description</th></tr></thead>
<tbody><tr><td >endpoint</td><td >API call address, which can be copied from <strong>Queue Service</strong> &gt; <strong>API Request Address</strong> in the <a href='https://console.intl.cloud.tencent.com/tdmq'>TDMQ for CMQ console</a>. <img src="https://main.qcloudimg.com/raw/397c634ac38494666e878caf69cf55e7.png" referrerpolicy="no-referrer" alt="img"></td></tr><tr><td >secretId, secretKey</td><td >TencentCloud API key, which can be copied on the <strong>Access Key</strong> &gt; <strong>API Key Management</strong> page in the <a href='https://console.intl.cloud.tencent.com/cam/overview'>CAM console</a>. <img src="https://main.qcloudimg.com/raw/867837e2b1e6d347ecb04d7085938c08.png" referrerpolicy="no-referrer" alt="img"></td></tr><tr><td style='text-align:left;' >$queue_name</td><td style='text-align:left;' >Queue name, which can be obtained on the <strong>Queue Service</strong> page in the <a href='https://console.intl.cloud.tencent.com/tdmq'>TDMQ for CMQ console</a>.</td></tr></tbody>
</table>
7. Consume messages.
<dx-codeblock>
:::  php
// Message queue name
$queue_name = "php_queue";
// Authentication result
$my_account = new Account($this->endpoint, $this->secretId, $this->secretKey);

$my_queue = $my_account->get_queue($queue_name);

$queue_meta = new QueueMeta();
$queue_meta->queueName = $queue_name;
$queue_meta->pollingWaitSeconds = 10;
$queue_meta->visibilityTimeout = 10;
$queue_meta->maxMsgSize = 1024;
$queue_meta->msgRetentionSeconds = 3600;

try {
    // Obtain messages
    $recv_msg = $my_queue->receive_message(3);
    echo "Receive Message Succeed! " . $recv_msg . "\n";
    // Successfully consumed messages are deleted
    $my_queue->delete_message($recv_msg->receiptHandle);
} catch (CMQExceptionBase $e) {
    echo "Create Queue Fail! Exception: " . $e;
    return;
}
:::
</dx-codeblock>
<table>
<thead>
<tr><th >Parameter</th><th >Description</th></tr></thead>
<tbody><tr><td >endpoint</td><td >API call address, which can be copied from <strong>Queue Service</strong> &gt; <strong>API Request Address</strong> in the <a href='https://console.intl.cloud.tencent.com/tdmq'>TDMQ for CMQ console</a>. <img src="https://main.qcloudimg.com/raw/397c634ac38494666e878caf69cf55e7.png" referrerpolicy="no-referrer" alt="img"></td></tr><tr><td >secretId, secretKey</td><td >TencentCloud API key, which can be copied on the <strong>Access Key</strong> &gt; <strong>API Key Management</strong> page in the <a href='https://console.intl.cloud.tencent.com/cam/overview'>CAM console</a>. <img src="https://main.qcloudimg.com/raw/867837e2b1e6d347ecb04d7085938c08.png" referrerpolicy="no-referrer" alt="img"></td></tr><tr><td >$queue_name</td><td >Queue name, which can be obtained on the <strong>Queue Service</strong> page in the <a href='https://console.intl.cloud.tencent.com/tdmq'>TDMQ for CMQ console</a>.</td></tr></tbody>
</table>

## Topic Model
### Directions
1. Prepare the required resources and create a topic subscription and a subscriber.
   1. Create a topic subscription in the console or via TencentCloud API. To use TencentCloud API, you need to install the SDK 3.0 for PHP.
   <dx-codeblock>
   :::  php
      $cred = new Credential($secretId, $secretKey);
      $httpProfile = new HttpProfile();
      $httpProfile->setEndpoint($endPoint);
      
      $clientProfile = new ClientProfile();
      $clientProfile->setHttpProfile($httpProfile);
      $client = new TdmqClient($cred, "ap-guangzhou", $clientProfile);
      
      $req = new CreateCmqTopicRequest();
      
      $params = array(
          "TopicName" => "topic_api1", // Topic name, which must be unique in the same region under the same account
          "FilterType" => 2, // Used to specify the message match policy for the topic. 1: Tag matching policy. 2: Routing matching policy
          "MsgRetentionSeconds" => 86400 // Message retention period. Value range: 60–86400 seconds (i.e., 1 minute–1 day)
      );
      $req->fromJsonString(json_encode($params));
      
      // Create a topic
      $resp = $client->CreateCmqTopic($req);
   :::
   </dx-codeblock>
<table>
<thead>
<tr><th >Parameter</th><th >Description</th></tr></thead>
<tbody><tr><td >$endPoint</td><td >API call address, which can be copied from <strong>Queue Service</strong> &gt; <strong>API Request Address</strong> in the <a href='https://console.intl.cloud.tencent.com/tdmq'>TDMQ for CMQ console</a>. <img src="https://main.qcloudimg.com/raw/397c634ac38494666e878caf69cf55e7.png" referrerpolicy="no-referrer" alt="img"></td></tr><tr><td >$secretId, $secretKey</td><td >TencentCloud API key, which can be copied on the <strong>Access Key</strong> &gt; <strong>API Key Management</strong> page in the <a href='https://console.intl.cloud.tencent.com/cam/overview'>CAM console</a>. <img src="https://main.qcloudimg.com/raw/867837e2b1e6d347ecb04d7085938c08.png" referrerpolicy="no-referrer" alt="img"></td></tr></tbody>
</table>
   2. Create a subscriber in the console or via TencentCloud API. To use TencentCloud API, you need to install the SDK 3.0 for PHP.
<dx-codeblock>
:::  php
      $cred = new Credential($secretId, $secretKey);
      $httpProfile = new HttpProfile();
      $httpProfile->setEndpoint($endPoint);
      
      $clientProfile = new ClientProfile();
      $clientProfile->setHttpProfile($httpProfile);
      $client = new TdmqClient($cred, "ap-guangzhou", $clientProfile);
      
      $req = new CreateCmqSubscribeRequest();
      
      $params = array(
          // Name of the topic for which to create a subscription
          "TopicName" => "topic_api1",
          // Subscription name
          "SubscriptionName" => "sub1",
          // Subscription protocol. Currently, two protocols are supported: HTTP and queue. To use the HTTP protocol, you need to build your own web server to receive messages. With the queue protocol, messages are automatically pushed to a CMQ queue and you can pull them concurrently.
          "Protocol" => "queue",
          // Endpoint that receives notifications, which varies by protocol: for HTTP, the endpoint must start with `http://`, and the `host` can be a domain or IP; for queue, `QueueName` should be entered.
          "Endpoint" => "topic_queue_api",
          // CMQ push server retry policy. Valid values: 1) BACKOFF_RETRY; 2) EXPONENTIAL_DECAY_RETRY.
          "NotifyStrategy" => "BACKOFF_RETRY",
          // The number of `BindingKey` cannot exceed 5, and the length of each `BindingKey` cannot exceed 64 bytes. This field indicates the filtering policy for subscribing to and receiving messages.
          "BindingKey" => array("a.b"),
          // Message filter tag (used for message filtering). The number of tags cannot exceed 5.
          // "FilterTag" => array("TAG"),
          // Push content format. Valid values: 1. JSON; 2. SIMPLIFIED, i.e., the raw format. If `Protocol` is `queue`, this value must be `SIMPLIFIED`. If `Protocol` is `http`, both options are acceptable, and the default value is `JSON`.
          "NotifyContentFormat" => "SIMPLIFIED"
      );
      $req->fromJsonString(json_encode($params));
      
      // Create a subscription
      $resp = $client->CreateCmqSubscribe($req);
:::
</dx-codeblock>
<dx-alert infotype="notice" title="">
`BindingKey` and `FilterTag` should be set according to the type of subscribed topic; otherwise, they will be invalid.
</dx-alert>
<table>
<thead>
<tr><th >Parameter</th><th >Description</th></tr></thead>
<tbody><tr><td >$endPoint</td><td >API call address, which can be copied from <strong>Queue Service</strong> &gt; <strong>API Request Address</strong> in the <a href='https://console.intl.cloud.tencent.com/tdmq'>TDMQ for CMQ console</a>. <img src="https://main.qcloudimg.com/raw/397c634ac38494666e878caf69cf55e7.png" referrerpolicy="no-referrer" alt="img"></td></tr><tr><td >$secretId, $secretKey</td><td >TencentCloud API key, which can be copied on the <strong>Access Key</strong> &gt; <strong>API Key Management</strong> page in the <a href='https://console.intl.cloud.tencent.com/cam/overview'>CAM console</a>. <img src="https://main.qcloudimg.com/raw/867837e2b1e6d347ecb04d7085938c08.png" referrerpolicy="no-referrer" alt="img"></td></tr></tbody>
</table>
2. Import [CMQ files](https://github.com/tencentyun/cmq-php-sdk) into the project.
3. Create `my_topic` to publish messages.
<dx-codeblock>
:::  php
   // Topic subscription name
   $topic_name = "php_topic_tag";
   // Authentication information
   $my_account = new Account($this->endpoint, $this->secretId, $this->secretKey);
   $my_topic = $my_account->get_topic($topic_name);
:::
</dx-codeblock>
<table>
<thead>
<tr><th >Parameter</th><th >Description</th></tr></thead>
<tbody><tr><td >endpoint</td><td >API call address, which can be copied from <strong>Queue Service</strong> &gt; <strong>API Request Address</strong> in the <a href='https://console.intl.cloud.tencent.com/tdmq'>TDMQ for CMQ console</a>. <img src="https://main.qcloudimg.com/raw/397c634ac38494666e878caf69cf55e7.png" referrerpolicy="no-referrer" alt="img"></td></tr><tr><td >secretId, secretKey</td><td >TencentCloud API key, which can be copied on the <strong>Access Key</strong> &gt; <strong>API Key Management</strong> page in the <a href='https://console.intl.cloud.tencent.com/cam/overview'>CAM console</a>. <img src="https://main.qcloudimg.com/raw/867837e2b1e6d347ecb04d7085938c08.png" referrerpolicy="no-referrer" alt="img"></td></tr><tr><td >$topic_name</td><td >Topic subscription name, which can be obtained on the <strong>Topic Subscription</strong> page in the <a href='https://console.intl.cloud.tencent.com/tdmq'>TDMQ for CMQ console</a>.</td></tr></tbody>
</table>
4. Send tag messages.
<dx-codeblock>
:::  php
   // Send tag messages
   $msg = "this is a test message for tag.";
   $msgid = $my_topic->publish_message($msg, array("TAG","TAG1"));
:::
</dx-codeblock>
5. Send route messages.
<dx-codeblock>
:::  php
   // Send route messages.
   $msg = "this is a test message for route.";
   $msgid = $my_topic->publish_message($msg, array(), "a.b.c");
:::
</dx-codeblock>
6. The consumer can consume messages in the message queue subscribed to by the subscriber.

>?Above is a brief introduction to message production and consumption in two models. For more information, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/cmq/tdmq-cmq-php-sdk-demo.zip) or [TDMQ for CMQ code repository](https://github.com/tencentyun/cmq-php-sdk).
