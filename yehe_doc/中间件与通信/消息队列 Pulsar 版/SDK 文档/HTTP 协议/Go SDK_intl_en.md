## Overview

This document uses Go as an example to describe how to connect to TDMQ for Pulsar to send and receive messages over the HTTP protocol.

## Prerequisites

- [You have created the required resources](https://intl.cloud.tencent.com/document/product/1110/42915).
- [You have installed Go](https://golang.org/dl/)
- [You have downloaded the demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/pulsar/http/tdmq-pulsar-go-http-demo.zip)

## Directions

1. Prepare the environment.
   1. Use a Tencent Cloud mirror for faster download.
      1. Linux or macOS.
      <dx-codeblock>
      :::  shell
      export GOPROXY=https://mirrors.tencent.com/go/
      :::
      </dx-codeblock>
      2. Windows。
      <dx-codeblock>
      :::  shell
      set GOPROXY=https://mirrors.tencent.com/go/
      :::
      </dx-codeblock>
   2. Install the basic and product packages.
      1. Install the common basic package.
      <dx-codeblock>
      :::  shell
      go get -v -u github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common
      :::
      </dx-codeblock>
      2. Install the corresponding TDMQ product package.
      <dx-codeblock>
      :::  shell
      go get -v -u github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/tdmq
      :::
      </dx-codeblock>
      <dx-alert infotype="explain" title="">
      For more information, see SDK for Go Installation.
      </dx-alert>
2. Create the TDMQ client.
<dx-codeblock>
:::  go
 // Authentication information
 credential := common.NewCredential(SECRET_ID, SECRET_KEY)
 cpf := profile.NewClientProfile()
 cpf.HttpProfile.Endpoint = ENDPOINT
 // Create the TDMQ client
 client, _ := tdmq.NewClient(credential, REGION, cpf)
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
        <td style='text-align:left;'>SECRET_ID、SECRET_KEY</td>
        <td style='text-align:left;'>TencentCloud API key, which can be copied on the <strong>Access Key</strong> &gt; <strong>API Key Management</strong> page in the <a href='https://console.cloud.tencent.com/cam'>CAM console</a>.
            <img
                    src="https://main.qcloudimg.com/raw/8ec140474be0ced1352695b372b2934d.png"
                    referrerpolicy="no-referrer" alt="img"></td>
    </tr>
    <tr>
        <td style='text-align:left;'>ENDPOINT</td>
        <td style='text-align:left;'>API request domain: tdmq.tencentcloudapi.com.</td>
    </tr>
    <tr>
        <td style='text-align:left;'>REGION</td>
        <td style='text-align:left;'>Cluster region. For more regions, see <a href='https://cloud.tencent.com/document/api/1179/46067#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8'>Region List</a>.
                href='https://cloud.tencent.com/document/api/1179/46067#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8'>地域列表</a>。
        </td>
    </tr>
    </tbody>
</table>
3. Send messages.
<dx-codeblock>
:::  go
   request := tdmq.NewSendMessagesRequest()
   // Authorized role key
   request.StringToken = common.StringPtr(token)
   // Authorized role name
   request.ProducerName = common.StringPtr(userName)
   // Set the topic name in the following format: cluster (tenant) ID/namespace/topic name
   request.Topic = common.StringPtr(topicName)
   // Message content
   request.Payload = common.StringPtr("this is a new message.")
   // Message sending timeout period
   request.SendTimeout = common.Int64Ptr(3000)
   // Send the message
   response, err := client.SendMessages(request)
   if _, ok := err.(*errors.TencentCloudSDKError); ok {
       fmt.Printf("An API error has returned: %s", err)
       return
   }
   if err != nil {
       panic(err)
   }
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
        <td style='text-align:left;'>token</td>
        <td style='text-align:left;'>Role key, which can be copied in the <strong>Key</strong> column on the <strong><a href='https://console.cloud.tencent.com/tdmq/role'>Role Management</a></strong> page.
                <img
                src="https://main.qcloudimg.com/raw/52907691231cc11e6e4801298ba90a6c.png" referrerpolicy="no-referrer"
                alt="img"></td>
    </tr>
    <tr>
        <td style='text-align:left;'>userName</td>
        <td style='text-align:left;'>Role name, which can be copied in the <strong>Name</strong> column on the <strong><a href='https://console.cloud.tencent.com/tdmq/role'>Role Management</a></strong> page.
                href='https://console.cloud.tencent.com/tdmq/role'>角色管理</a></strong> 页面复制<strong>名称</strong>列复制。
        </td>
    </tr>
    <tr>
        <td style='text-align:left;'>topicName</td>
        <td style='text-align:left;'>Topic name in the following format: cluster (tenant) ID/namespace/topic name, such as `pulsar-xxx/sdk_http/topic1`. You can directly copy it on the <strong><a href='https://console.cloud.tencent.com/tdmq/topic'>Topic Management</a></strong> page in the console.
            <strong><a href='https://console.cloud.tencent.com/tdmq/topic'>Topic 管理</a></strong> 页面直接复制。
        </td>
    </tr>
    </tbody>
</table>
4. Consume messages.
<dx-codeblock>
:::  go
   request := tdmq.NewReceiveMessageRequest()
   // Set the topic name in the following format: cluster (tenant) ID/namespace/topic name
   request.Topic = common.StringPtr(topicName)
   // Set the subscription name
   request.SubscriptionName = common.StringPtr(subName)
   // Messages received by the consumer will first be stored in the `receiverQueueSize` queue to tune the message receiving rate
   request.ReceiverQueueSize = common.Int64Ptr(10)
   // It is used to determine the position where the consumer initially receives messages. Valid values: Earliest, Latest.
   request.SubInitialPosition = common.StringPtr("Latest")
   // Consume messages
   response, err := client.ReceiveMessage(request)
   if _, ok := err.(*errors.TencentCloudSDKError); ok {
       fmt.Printf("An API error has returned: %s", err)
       return
   }
   if err != nil {
       panic(err)
   }
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
        <td style='text-align:left;'>topicName</td>
        <td style='text-align:left;'>Topic name in the following format: cluster (tenant) ID/namespace/topic name, such as `pulsar-xxx/sdk_http/topic1`. You can directly copy it on the <strong><a href='https://console.cloud.tencent.com/tdmq/topic'>Topic Management</a></strong> page in the console.
                href='https://console.cloud.tencent.com/tdmq/topic'>Topic 管理</a></strong> 页面直接复制。
        </td>
    </tr>
    <tr>
        <td style='text-align:left;'>subName</td>
        <td style='text-align:left;'>Subscription name, which can be copied on the <strong>Cluster</strong> &gt; <strong>Consumer</strong> tab in the console.</td>
    </tr>
    </tbody>
</table>
5. Acknowledge messages.
<dx-codeblock>
:::  go
   request := tdmq.NewAcknowledgeMessageRequest()
   // Set the message ID
   request.MessageId = common.StringPtr(messageId)
   // Set the topic name in the following format: cluster (tenant) ID/namespace/topic name
   request.AckTopic = common.StringPtr(topicName)
   // Set the message subscription
   request.SubName = common.StringPtr(subName)
   // Acknowledge messages
   response, err := client.AcknowledgeMessage(request)
   if _, ok := err.(*errors.TencentCloudSDKError); ok {
       fmt.Printf("An API error has returned: %s", err)
       return
   }
   if err != nil {
       panic(err)
   }
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
        <td style='text-align:left;'>messageId</td>
        <td style='text-align:left;'>Message ID obtained after message consumption.</td>
    </tr>
    <tr>
        <td style='text-align:left;'>topicName</td>
        <td style='text-align:left;'>Topic name in the following format: cluster (tenant) ID/namespace/topic name, such as `pulsar-xxx/sdk_http/topic1`. You can directly copy it on the <strong><a href='https://console.cloud.tencent.com/tdmq/topic'>Topic Management</a></strong> page in the console.
                href='https://console.cloud.tencent.com/tdmq/topic'>Topic 管理</a></strong> 页面直接复制。
        </td>
    </tr>
    <tr>
        <td style='text-align:left;'>subName</td>
        <td style='text-align:left;'>Subscription name, which can be copied on the <strong>Cluster</strong> &gt; <strong>Consumer</strong> tab in the console.</td>
    </tr>
    </tbody>
</table>


>? Above is a brief introduction to message sending and receiving operations. For more information, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/pulsar/http/tdmq-pulsar-go-http-demo.zip) or [API Explorer](https://console.cloud.tencent.com/api/explorer?Product=tdmq&Version=2020-02-17&Action=ModifyCluster&SignVersion=).
