## Overview

This document provides an overview of APIs and SDK code samples for async processing queues.

| API | Operation |  Description |
| :--------------- | :------------------ | :--------------------- |
| [DescribeDocProcessQueues](https://intl.cloud.tencent.com/document/product/436/49411)  |  Querying file transcoding queues     |  Queries file transcoding queues.   |
| [UpdateDocProcessQueue](https://intl.cloud.tencent.com/document/product/436/49412)  |  Querying file transcoding queues     |  Queries file transcoding queues.   |

## Querying File Transcoding Queue

#### Feature description

This API (`DescribeDocProcessQueues`) is used to query the file transcoding queue. It can also be used to get the ID of the queue where the specified bucket is in.

#### Sample code
```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; // Replace it with your actual `secretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
$secretKey = "SECRETKEY"; // Replace it with your actual `secretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is `http` by default.
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    $result = $cosClient->describeDocProcessQueues(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
    ));
    // The request succeeded.
    print_r($result);
} catch (\Exception $e) {
    // The request failed.
    echo($e);
}
```

#### Parameter description

| Parameter | Type | Description |
| ---------- | -------------- | ------ |
| Bucket | COS bucket name | String |

#### Response parameter description

`Response` has the following sub-nodes:

| Parameter | Type | Description |
| ------------------ | ------- | -------------------------------------------------------- |
| RequestId               | String | Unique ID of the request	                           |
| TotalCount | Integer| Total number of queues	 |
| PageNumber | Integer|  Current page number. Same as `pageNumber` in the request.	 |
| PageSize | Integer|  Number of entries per page. Same as `pageSize` in the request.	 |
| QueueList | Array|  Queue array |

`QueueList` has the following sub-nodes:

| Parameter | Type | Description |
| ----------------- | ------------------------------------------------------------ | ------- |
| QueueId            | String  | Queue ID	                                               |
| Name           | String  | Queue name	                                       |
| State               | String  | Current status: `Active` or `Paused`	                                       |
| NotifyConfig       | Array  | Callback configuration	                                   |
| MaxSize         | Integer  | Maximum queue length	                   |
| MaxConcurrent              | Integer | Maximum number of concurrent jobs in the current queue                        |
| UpdateTime            | String  | Update time 	 |
| CreateTime | String  | Creation time	  |

`NotifyConfig` has the following sub-nodes:

| Parameter | Type | Description |
| ------------------ | ------- | -------------------------------------------------------- |
| Url         | String  | Callback address		                   |
| State              | String | Status: `On` or `Off`	                        |
| Type            | String  | Callback type: Url		 |
| Event | String  | The event that triggers the callback		  |

## Updating File Transcoding Queue

#### Feature description
This API (`UpdateDocProcessQueue`) is used to update a file transcoding queue.

#### Sample code
```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; // Replace it with your actual `secretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
$secretKey = "SECRETKEY"; // Replace it with your actual `secretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is `http` by default.
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    // Update the file transcoding queue as instructed at https://cloud.tencent.com/document/product/460/46947
    $result = $cosClient->updateDocProcessQueue(array(
        'Bucket' => 'examplebucket-125000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
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
    // The request succeeded.
    print_r($result);
} catch (\Exception $e) {
    // The request failed.
    echo($e);
}
```

#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| :----------------- | :------ | :------- | :-------- | :------- | :----------------------------------------------------------- |
| Name               | Request | Queue name | String    | Yes       | Up to 100 characters                                              |
| QueueID            | Request | Queue ID  | String    | Yes       | None                                                           |
| State              | Request | Queue status | String    | Yes       | 1. Active: Jobs in the queue will be scheduled and executed by the file preview service. </br>2. Paused: The queue is paused, and jobs in it will no longer be scheduled and executed. All jobs in the queue will remain in the `Submitted` status, while jobs being executed will continue without being affected. |
| NotifyConfig       | Request | Notification channel | Container | Yes       | Third-party callback URL                                               |

`NotifyConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| :----------------- | :------------------- | :------------------------- | :----- | :------- | :-------------- |
| Url                | Request.NotifyConfig | Callback configuration                   | String | No       | Up to 100 characters |
| Type               | Request.NotifyConfig | Callback type. General callback: `Url`.    | String | No       | Up to 100 characters |
| Event              | Request.NotifyConfig | Callback event: File preview job completed. | String | No       | Up to 100 characters |
| State              | Request.NotifyConfig | Callback status: `Off` or `On`.          | String | No       | Up to 100 characters |

#### Response parameter description

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------------------------------------------- | :-------- |
| RequestId          | Response | Unique ID of the request                                                | String    |
| Queue              | Response | Queue information. For more information, see `Response.QueueList` in `DescribeDocProcessQueues`. | Container |

