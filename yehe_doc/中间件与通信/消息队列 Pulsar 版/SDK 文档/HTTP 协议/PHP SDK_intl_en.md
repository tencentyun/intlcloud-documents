## Overview

This document uses PHP as an example to describe how to connect to TDMQ for Pulsar to send and receive messages over the HTTP protocol.



## Prerequisites

- [You have created the required resources](https://intl.cloud.tencent.com/document/product/1110/42915).
- [Install PHP 5.6 or later](https://www.php.net/manual/en/install.php)
- [Install PEAR](https://pear.php.net/manual/en/installation.getting.php)
- [You have downloaded the demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/pulsar/http/tdmq-pulsar-php-http-demo.zip)

## Directions

1. Prepare the environment.
   1. Add dependencies.
   <dx-codeblock>
   :::  shell
   composer require tencentcloud/tencentcloud-sdk-php
   :::
   </dx-codeblock>
   2. Add references.
   <dx-codeblock>
   :::  php
   require '/path/to/vendor/autoload.php';
   :::
   </dx-codeblock>
   <dx-alert infotype="explain" title="">
   For more information, see SDK for PHP 3.0 Installation and Use Guide.
   </dx-alert>
2. Create the TDMQ client.

<dx-codeblock>
:::  php
   // Authentication information
   $cred = new Credential($secretId, $secretKey);
   $httpProfile = new HttpProfile();
   $httpProfile->setEndpoint($endpoint);

   $clientProfile = new ClientProfile();
   $clientProfile->setHttpProfile($httpProfile);
   // Create the TDMQ client
   $client = new TdmqClient($cred, $region, $clientProfile);
:::
</dx-codeblock>
<table>
    <thead>
    <tr>
        <th style='text-align:left;'>Parameter</th>
        <th style='text-align:left;'>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td style='text-align:left;'>$secretId、$secretKey</td>
        <td style='text-align:left;'>TencentCloud API key, which can be copied on the <strong>Access Key</strong> &gt; <strong>API Key Management</strong> page in the <a href='https://console.cloud.tencent.com/cam'>CAM console</a>.
            <img
                    src="https://qcloudimg.tencent-cloud.cn/raw/ba7e9efacb7444d65e24c14ebd864a1a.png"
                    referrerpolicy="no-referrer" alt="img"></td>
    </tr>
    <tr>
        <td style='text-align:left;'>$endpoint</td>
        <td style='text-align:left;'>API request domain: tdmq.tencentcloudapi.com.</td>
    </tr>
    <tr>
        <td style='text-align:left;'>$region</td>
        <td style='text-align:left;'>Cluster region.
        </td>
    </tr>
    </tbody>
</table>
3. Send messages.
<dx-codeblock>
:::  php
   $req = new SendMessagesRequest();
   
   $params = array(
       // Authorized role key
       "StringToken" => $token,
       // Topic name in the following format: cluster (tenant) ID/namespace/topic name
       "Topic" => $fullTopicName,
       // Message content
       "Payload" => "this is a new message.",
       // Authorized role name
       "ProducerName" => $userName,
       // Message sending timeout period
       "SendTimeout" => 3000A
   );
   $req->fromJsonString(json_encode($params));
   
   // Send the message
   $resp = $client->SendMessages($req);
:::
</dx-codeblock>
<table>
    <thead>
    <tr>
        <th style='text-align:left;'>Parameter</th>
        <th style='text-align:left;'>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td style='text-align:left;'>$token</td>
        <td style='text-align:left;'>Role key, which can be copied in the <strong>Key</strong> column on the <strong><a href='https://console.cloud.tencent.com/tdmq/role'>Role Management</a></strong> page.
                <img
                src="https://qcloudimg.tencent-cloud.cn/raw/5a3bd084903926be994e3e1ac2f9631c.png" referrerpolicy="no-referrer"
                alt="img"></td>
    </tr>
    <tr>
        <td style='text-align:left;'>$userName</td>
        <td style='text-align:left;'>Role name, which can be copied in the <strong>Name</strong> column on the <strong><a href='https://console.cloud.tencent.com/tdmq/role'>Role Management</a></strong> page.
        </td>
    </tr>
    <tr>
        <td style='text-align:left;'>$fullTopicName</td>
        <td style='text-align:left;'>Topic name in the following format: cluster (tenant) ID/namespace/topic name, such as `pulsar-xxx/sdk_http/topic1`. You can directly copy it on the <strong><a href='https://console.cloud.tencent.com/tdmq/topic'>Topic Management</a></strong> page in the console.
        </td>
    </tr>
    </tbody>
</table>
4. Consume messages.
<dx-codeblock>
:::  php
   $req = new ReceiveMessageRequest();
   
   $params = array(
       // Topic name in the following format: cluster (tenant) ID/namespace/topic name
       "Topic" => $fullTopicName,
       // Subscription name
       "SubscriptionName" => $subName,
       // Messages received by the consumer will first be stored in the `receiverQueueSize` queue to tune the message receiving rate
       "ReceiverQueueSize" => 10,
       // It is used to determine the position where the consumer initially receives messages. Valid values: Earliest, Latest.
       "SubInitialPosition" => "Latest"
   );
   $req->fromJsonString(json_encode($params));
   
   // Receive messages
   $resp = $client->ReceiveMessage($req);
:::
</dx-codeblock>
<table>
    <thead>
    <tr>
        <th style='text-align:left;'>Parameter</th>
        <th style='text-align:left;'>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td style='text-align:left;'>$fullTopicName</td>
        <td style='text-align:left;'>Topic name in the following format: cluster (tenant) ID/namespace/topic name, such as `pulsar-xxx/sdk_http/topic1`. You can directly copy it on the <strong><a href='https://console.cloud.tencent.com/tdmq/topic'>Topic Management</a></strong> page in the console.
        </td>
    </tr>
    <tr>
        <td style='text-align:left;'>$subName</td>
        <td style='text-align:left;'>Subscription name, which can be copied on the <strong>Cluster</strong> &gt; <strong>Consumer</strong> tab in the console.</td>
    </tr>
    </tbody>
</table>
5. Acknowledge messages.
<dx-codeblock>
:::  php
   $req = new AcknowledgeMessageRequest();
   
   $params = array(
       // ID of the message to be acknowledged
       "MessageId" => $messageId,
       // Topic name in the following format: cluster (tenant) ID/namespace/topic name
       "AckTopic" => $fullTopicName,
       // Subscription name
       "SubName" => $subName
   );
   $req->fromJsonString(json_encode($params));
   
   // Acknowledge messages
   $resp = $client->AcknowledgeMessage($req);
:::
</dx-codeblock>
<table>
    <thead>
    <tr>
        <th style='text-align:left;'>Parameter</th>
        <th style='text-align:left;'>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td style='text-align:left;'>$messageId</td>
        <td style='text-align:left;'>Message ID obtained after message consumption.</td>
    </tr>
    <tr>
        <td style='text-align:left;'>$fullTopicName</td>
        <td style='text-align:left;'>Topic name in the following format: cluster (tenant) ID/namespace/topic name, such as `pulsar-xxx/sdk_http/topic1`. You can directly copy it on the <strong><a href='https://console.cloud.tencent.com/tdmq/topic'>Topic Management</a></strong> page in the console.
        </td>
    </tr>
    <tr>
        <td style='text-align:left;'>$subName</td>
        <td style='text-align:left;'>Subscription name, which can be copied on the <strong>Cluster</strong> &gt; <strong>Consumer</strong> tab in the console.</td>
    </tr>
    </tbody>
</table>


>? Above is a brief introduction to message sending and receiving operations. For more information, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/pulsar/http/tdmq-pulsar-php-http-demo.zip) or [API Explorer](https://console.cloud.tencent.com/api/explorer?Product=tdmq&Version=2020-02-17&Action=ModifyCluster&SignVersion=).
