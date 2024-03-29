## 简介

本文档提供关于异步处理队列接口相关的 API 概览以及 SDK 示例代码。

| API           |    操作名  |   操作描述               |
| :--------------- | :------------------ | :--------------------- |
| [DescribeDocProcessQueues](https://intl.cloud.tencent.com/document/product/436/49411) |  查询文档转码队列     |  用于查询文档转码队列   |
| [UpdateDocProcessQueue](https://intl.cloud.tencent.com/document/product/436/49412) | 更新文档转码队列 | 用于更新文档转码队列 |

## 查询文档转码队列

#### 功能说明

DescribeDocProcessQueues 接口用于查询文档转码队列。（可通过该接口获取桶对应的队列 ID）

#### 示例代码
```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //替换为用户的 secretId，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //替换为用户的 secretKey，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //替换为用户的 region，已创建桶归属的region可以在控制台查看，https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //协议头部，默认为http
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    $result = $cosClient->describeDocProcessQueues(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
    ));
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

| 参数名称   | 类型           | 描述   |
| ---------- | -------------- | ------ |
| Bucket | COS 存储桶名称 | String |

#### 返回参数说明

Response 中的具体数据描述如下：

| 参数名称             | 类型   | 描述                                                         | 
| ------------------ | ------- | -------------------------------------------------------- | 
| RequestId               | String | 请求的唯一 ID	                           | 
| TotalCount | Integer| 队列总数	 | 
| PageNumber | Integer|  当前页数，同请求中的 pageNumber	 | 
| PageSize | Integer|  每页个数，同请求中的 pageSize	 | 
| QueueList | Array|  队列数组 | 

QueueList 中的具体数据描述如下：

| 参数名称          | 类型                                                         | 描述    |
| ----------------- | ------------------------------------------------------------ | ------- |
| QueueId            | String  |队列 ID	                                               | 
| Name           | String  |队列名字	                                       | 
| State               | String  |当前状态，Active 或者 Paused	                                       | 
| NotifyConfig       | Array  |回调配置	                                   | 
| MaxSize         | Integer  |队列最大长度	                   | 
| MaxConcurrent              | Integer |当前队列最大并行执行的任务数                        | 
| UpdateTime            | String  |更新时间	 | 
| CreateTime | String  |创建时间	  | 

NotifyConfig 中的具体数据描述如下：

| 参数名称             | 类型   | 描述                                                         | 
| ------------------ | ------- | -------------------------------------------------------- | 
| Url         | String  |回调地址		                   | 
| State              | String |开关状态，On 或者 Off	                        | 
| Type            | String  |回调类型，Url		 | 
| Event | String  |触发回调的事件		  | 

## 更新文档转码队列

#### 功能说明
UpdateDocProcessQueue 接口用于更新文档转码队列。

#### 示例代码
```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //替换为用户的 secretId，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //替换为用户的 secretKey，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //替换为用户的 region，已创建桶归属的region可以在控制台查看，https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //协议头部，默认为http
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    // 更新文档转码队列 https://cloud.tencent.com/document/product/460/46947
    $result = $cosClient->updateDocProcessQueue(array(
        'Bucket' => 'examplebucket-125000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Key' => '', // QueueID
        'Name' => '',
        'QueueID' => '',
        'State' => '',
        'NotifyConfig' => array(
            'Url' => '',
            'Type' => '',
            'Event' => '',
            'State' => '',
        ),
    ));
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

Request 中的具体数据描述如下：

| 节点名称（关键字） | 父节点  | 描述     | 类型      | 是否必选 | 限制                                                         |
| :----------------- | :------ | :------- | :-------- | :------- | :----------------------------------------------------------- |
| Name               | Request | 队列名称 | String    | 是       | 长度限制100字符                                              |
| QueueID            | Request | 队列 ID  | String    | 是       | 无                                                           |
| State              | Request | 队列状态 | String    | 是       | 1. Active 表示队列内的作业会被文档预览服务调度转码执行 </br>2. Paused 表示队列暂停，作业不再会被文档预览服务调度执行，队列内的所有作业状态维持在已提交状态，已经处于执行中的任务将继续执行，不受影响 |
| NotifyConfig       | Request | 通知渠道 | Container | 是       | 第三方回调 Url                                               |

Container 类型 NotifyConfig 的具体数据描述如下：

| 节点名称（关键字） | 父节点               | 描述                       | 类型   | 是否必选 | 限制            |
| :----------------- | :------------------- | :------------------------- | :----- | :------- | :-------------- |
| Url                | Request.NotifyConfig | 回调配置                   | String | 否       | 长度限制100字符 |
| Type               | Request.NotifyConfig | 回调类型，普通回调：Url    | String | 否       | 长度限制100字符 |
| Event              | Request.NotifyConfig | 回调事件，文档预览任务完成 | String | 否       | 长度限制100字符 |
| State              | Request.NotifyConfig | 回调开关，Off，On          | String | 否       | 长度限制100字符 |

#### 返回参数说明

Response 中的具体数据描述如下：

| 节点名称（关键字） | 父节点   | 描述                                                         | 类型      |
| :----------------- | :------- | :----------------------------------------------------------- | :-------- |
| RequestId          | Response | 请求的唯一 ID                                                | String    |
| Queue              | Response | 队列信息，详情请参见 [DescribeDocProcessQueues](https://intl.cloud.tencent.com/document/product/1045/47935) 中的 Response.QueueList | Container |

