This document summarizes the message structures of all trigger events that are connected to SCF. For more information on trigger configuration and restrictions, please see [Trigger Overview](https://intl.cloud.tencent.com/document/product/583/9705).
>The event structure of the input parameter passed in by a trigger has been partially defined and can be used directly. You can get and use the Java library through the [Java Cloud Event Definition](https://github.com/tencentyun/scf-java-libs) or the Go library through the [Go Cloud Event Definition](https://github.com/tencentyun/scf-go-lib/tree/master/events).
>

## Event Message Structure of Integration Request for API Gateway Trigger

When an API Gateway trigger receives a request, event data will be sent to the bound function in JSON format as shown below.
```
{
  "requestContext": {
    "serviceId": "service-f94sy04v",
    "path": "/test/{path}",
    "httpMethod": "POST",
    "requestId": "c6af9ac6-7b61-11e6-9a41-93e8deadbeef",
    "identity": {
      "secretId": "abdcdxxxxxxxsdfs"
    },
    "sourceIp": "10.0.2.14",
    "stage": "release"
  },
  "headers": {
    "Accept-Language": "en-US,en,cn",
    "Accept": "text/html,application/xml,application/json",
    "Host": "service-3ei3tii4-251000691.ap-guangzhou.apigateway.myqloud.com",
    "User-Agent": "User Agent String"
  },
  "body": "{\"test\":\"body\"}",
  "pathParameters": {
    "path": "value"
  },
  "queryStringParameters": {
    "foo": "bar"
  },
  "headerParameters":{
    "Refer": "10.0.2.14"
  },
  "stageVariables": {
    "stage": "release"
  },
  "path": "/test/value",
  "queryString": {
    "foo" : "bar",
    "bob" : "alice"
  },
  "httpMethod": "POST"
}
```

## Event Message Structure for Timer Trigger

When a function is invoked at a scheduled time, event data will be sent to the bound function in JSON format as shown below.

```
{
    "Type":"Timer",
    "TriggerName":"EveryDay",
    "Time":"2019-02-21T11:49:00Z",
    "Message":"user define msg body"
}
```



## Event Message Structure for COS Trigger

When an object creation or deletion event occurs in the specified COS bucket, event data will be sent to the bound function in JSON format as shown below.
```
{
    "Records": [{
        "cos": {
            "cosSchemaVersion": "1.0",
            "cosObject": {
                "url": "http://testpic-1253970026.cos.ap-chengdu.myqcloud.com/testfile",
                "meta": {
                    "x-cos-request-id": "NWMxOWY4MGFfMjViMjU4NjRfMTUyMV8yNzhhZjM=",
                    "Content-Type": ""
                },
                "vid": "",
                "key": "/1253970026/testpic/testfile",
                "size": 1029
            },
            "cosBucket": {
                "region": "cd",
                "name": "testpic",
                "appid": "1253970026"
            },
            "cosNotificationId": "unkown"
        },
        "event": {
            "eventName": "cos:ObjectCreated:*",
            "eventVersion": "1.0",
            "eventTime": 1545205770,
            "eventSource": "qcs::cos",
            "requestParameters": {
                "requestSourceIP": "192.168.15.101",
                "requestHeaders": {
                    "Authorization": "q-sign-algorithm=sha1&q-ak=AKIDQm6iUh2NJ6jL41tVUis9KpY5Rgv49zyC&q-sign-time=1545205709;1545215769&q-key-time=1545205709;1545215769&q-header-list=host;x-cos-storage-class&q-url-param-list=&q-signature=098ac7dfe9cf21116f946c4b4c29001c2b449b14"
                }
            },
            "eventQueue": "qcs:0:lambda:cd:appid/1253970026:default.printevent.$LATEST",
            "reservedInfo": "",
            "reqid": 179398952
        }
    }]
}
```

## Event Message Structure for CKafka Trigger

When a specified CKafka topic receives a message, the backend consumption module of SCF will consume the message and encapsulate it into an event in JSON format like the one below, which will trigger the bound function and pass the data content as input parameters to the function.
```
{
  "Records": [
    {
      "Ckafka": {
        "topic": "test-topic",
        "partition":1,
        "offset":36,
        "msgKey": "None",
        "msgBody": "Hello from Ckafka!"
      }
    },
    {
      "Ckafka": {
        "topic": "test-topic",
        "partition":1,
        "offset":37,
        "msgKey": "None",
        "msgBody": "Hello from Ckafka again!"
      }
    }
  ]
}
```

## Event Structure for CMQ Topic Trigger

When a specified CMQ topic receives a message, event data will be sent to the bound function in JSON format as shown below.
```
{
  "Records": [
    {
      "CMQ": {
        "type": "topic",
        "topicOwner":"120xxxxx",
        "topicName": "testtopic",
        "subscriptionName":"xxxxxx",
        "publishTime": "1970-01-01T00:00:00.000Z",
        "msgId": "123345346",
        "requestId":"123345346",
        "msgBody": "Hello from CMQ!",
        "msgTag": "tag1,tag2"
      }
    }
  ]
}
```

