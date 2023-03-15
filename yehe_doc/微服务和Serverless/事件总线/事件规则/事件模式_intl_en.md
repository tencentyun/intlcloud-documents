An event pattern defines how EventBridge filters events and routes them to the event target. It must be in the same structure as the matched events. This document describes the common event pattern types:
### Must-Knows

The event pattern match rules are as detailed below:


- Matched events must contain all field names listed in the event pattern in the same nesting structure.
- Match between events and an event pattern is exact match down to the character and case-sensitive. During match, no standardized operations will be performed on the strings.
- Values to be matched must be in JSON format, which include strings and numeric values enclosed in quotation marks as well as keywords not enclosed in quotation marks (`true`, `false`, and `null`).


### Specifying Condition and Operator

You can specify a field value as a match condition. Values to be matched are in a JSON array and enclosed in `[ ]`. Values in `[ ]` are in OR relationship, and keys are in AND relationship.
Assumes that the following COS event is received: 


```
{
    "specversion": "1.0",
    "id": "13a3f42d-7258-4ada-da6d-023a333b4662",
    "type": "cos:created:object",
    "source": "cos.cloud.tencent",
    "subject": "qcs::cos:ap-guangzhou:uid1250000000:bucketname",
    "time": "1615430559146",
    "region": "ap-guangzhou",
    "datacontenttype": "application/json;charset=utf-8",
    "resource": [
        "qcs::eb:ap-guangzhou:uid1250000000:eventbusid/eventruleid"
    ],
    "data": {
        "name": "testname",
        "scope": 100
    }
}
```
To match this event with the specified `name` in the `data` field, the rule should be:


```
{
    "data": {
        "name": [
            "testname"
        ]
    }
}
```
To match the event with any of the specified `name` values in the `data` field, the statement should be:


```
{
    "data": {
        "name": [
            "testname","test"
        ]
    }
}
```


### Prefix Matching

You can match events with the specified prefix by using `{ "prefix": "2021-10-02" }`.
Assumes that the following COS event is received: 


```
{
    "specversion": "1.0",
    "id": "13a3f42d-7258-4ada-da6d-023a333b4662",
    "type": "cos:created:object",
    "source": "cos.cloud.tencent",
    "subject": "qcs::cos:ap-guangzhou:uid1250000000:bucketname",
    "time": "1615430559146",
    "region": "ap-guangzhou",
    "datacontenttype": "application/json;charset=utf-8",
    "resource": [
        "qcs::eb:ap-guangzhou:uid1250000000:eventbusid/eventruleid"
    ],
    "data": {
        "name": "testname",
        "scope": 100
    }
}
```
To match the event with the specified prefix of `name`, the statement should be:


```
{
   "data":{
      "name":[
         {
            "prefix":"te"
         }
      ]
   }
}
```
### Suffix Matching

You can match events with the specified suffix by using `{ "suffix": ".txt" }`.
Assumes that the following TDMQ event is received: 


```
{
    "specversion": "1.0",
    "id": "13a3f42d-7258-4ada-da6d-023a333b4662",
    "type": "connector:tdmq",
    "source": "tdmq.cloud.tencent",
    "subject": "qcs::tdmq:$region:$account:topicName/$topicSets.clusterId/$topicSets.environmentId/$topicSets.topicName/$topicSets.subscriptionName",
    "time": "1615430559146",
    "region": "ap-guangzhou",
    "datacontenttype": "application/json;charset=utf-8",
    "data": {
                    "topic":  "persistent://appid/namespace/topic-1",
                    "tags": "testtopic",
                    "TopicType": "0",
                    "subscriptionName": "xxxxxx",
                    "toTimestamp": "1603352765001",
                    "partitions": "0",
                    "msgId": "123345346",
                    "msgBody": "Hello from TDMQ!"
    }
}
```
To match the event with the specified topic suffix, the statement should be:


```
{
    "data": {
        "topic": [{
            "suffix":"/topic-1"
        }]
    }
}
```
## Exclusion Matching

You can match events that contain anything but the specified value in the specified field with a statement like `{ "anything-but": "initializing" }`.
Assumes that the following COS event is received: 


```
{
   "specversion":"1.0",
   "id":"13a3f42d-7258-4ada-da6d-023a333b4662",
   "type":"cos:created:object",
   "source":"cos.cloud.tencent",
   "subject":"qcs::cos:ap-guangzhou:uid1250000000:bucketname",
   "time":"1615430559146",
   "region":"ap-guangzhou",
   "datacontenttype": "application/json;charset=utf-8",
   "resource":[
    "qcs::eb:ap-guangzhou:uid1250000000:eventbusid/eventruleid"
   ],
   "data":{
      "name":"testname",
      "scope":100
   }
}
```
To match events with anything but `teset1` in the `name` of `data`, the statement should be:


```
{
    "data": {
        "name": [{
            "anything-but":"test1"
        }]
    }
}
```
To match the event with anything by the specified value in the `name` of `data`, the statement should be: 


```
{
    "data": {
        "name": [{
            "anything-but":"testname"
        }]
    }
}
```
### Inclusion Matching

You can match events with the specified values in the specified field of `data` by using a statement like `{ "contain": ".txt" }`.
Assumes that the following TDMQ event is received: 


```
{
    "specversion": "1.0",
    "id": "13a3f42d-7258-4ada-da6d-023a333b4662",
    "type": "connector:tdmq",
    "source": "tdmq.cloud.tencent",
    "subject": "qcs::tdmq:$region:$account:topicName/$topicSets.clusterId/$topicSets.environmentId/$topicSets.topicName/$topicSets.subscriptionName",
    "time": "1615430559146",
    "region": "ap-guangzhou",
    "datacontenttype": "application/json;charset=utf-8",
    "data": {
                    "topic":  "persistent://appid/namespace/topic-1",
                    "tags": "testtopic",
                    "TopicType": "0",
                    "subscriptionName": "xxxxxx",
                    "toTimestamp": "1603352765001",
                    "partitions": "0",
                    "msgId": "123345346",
                    "msgBody": "Hello from TDMQ!"
    }
}
```
To match the event with the specified `topic` value in `data`, the statement should be:


```
{
    "data": {
        "topic": [{
            "contain":"topic-1"
        }]
    }
}
```

To match the event that includes all the specified `topic` values in `data`, the statement should be: 


```
{
    "data": {
        "topic": [{
            "contain":["topic-1","appid"]
        }]
    }
}
```
### Array Matching

You can filter array fields with a syntax statement, such as `{"array": "{\"key1:\"value1\"}"}`.
Assumes that the following DTS event is received:


```
{
  "id": "13a3f42d-7258-4ada-da6d-023a33******",
  "type": "dts:mysql:update",
  "specversion": "1.0",
  "source": "dts.cloud.tencent",
  "subject": "cdb-xxx",
  "time": 1660013278609,
  "region": "ap-guangzhou",
  "dataContentType": "application/json;charset=utf-8",
  "tags": {
    "key1": "value1",
    "key2": "value2"
  },
  "data": {
    "topic": "topic-subs-xxx-cdb-xxx",
    "partition": 0,
    "offset": 72235,
    "partition_seq": 72236,
    "event": {
      "dmlEvent": {
        "dmlEventType": 1,
        "columns": [
          {
            "name": "time",
            "originalType": "time"
          },
          {
            "name": "id",
            "originalType": "int(11)",
            "isKey": true
          }
        ],
        "rows": [
          {
            "oldColumns": [
              {
                "dataType": 13,
                "charset": "utf8",
                "bv": "c3NzYWFhcWFxMTEx"
              }
            ],
            "newColumns": [
              {
                "dataType": 13,
                "charset": "utf8",
                "bv": "MjA6MTI6MjI="
              }
            ]
          }
        ]
      }
    },
    "header": {
      "sourceType": 1,
      "messageType": 2,
      "timestamp": 1648555949,
      "serverId": 109741,
      "fileName": "mysql-bin.000005",
      "position": 11172920,
      "gtid": "38cecd93-a9c2-11ec-b952-043f72d8da53:55",
      "schemaName": "dts",
      "tableName": "dts_mysql",
      "seqId": 72286,
      "isLast": true
    },
    "eb_consumer_time": "2022-03-29T20:12:29+08:00",
    "eb_connector": "cdb-xxx"
  }
}
```
To match the event via the `columns` fields, the statement should be: 


```
{
    "source": "dts.cloud.tencent",
    "type": "dts:mysql:update",
    "data": {
        "event": {
            "dmlEvent": {
                "columns": [{
                    "array": "{\"name\":\"time\"}"
                }]
            }
        }
    }
}
```
Multiple filters are combined with AND.


```
{
    "source": "dts.cloud.tencent",
    "type": "dts:mysql:update",
    "data": {
        "event": {
            "dmlEvent": {
                "columns": [{
                    "array": "{\"name\":\"id\",\"originalType\":\"int(11)\"}"
                            }]
            }
        }
    }
}
```
### IP Matching

You can specify an IP address in the `data` field as a match condition. For example, if the statement is `{ "cidr": "10.0.0.0/24" }`, events whose IP is within the `10.0.0.0/24` IP range are returned. 
Assumes that the following COS event is received: 


```
{
    "specversion": "1.0",
    "id": "13a3f42d-7258-4ada-da6d-023a333b4662",
    "type": "cos:created:object",
    "source": "cos.cloud.tencent",
    "subject": "qcs::cos:ap-guangzhou:uid1250000000:bucketname",
    "time": "1615430559146",
    "region": "ap-guangzhou",
    "datacontenttype": "application/json;charset=utf-8",
    "resource": [
        "qcs::eb:ap-guangzhou:uid1250000000:eventbusid/eventruleid"
    ],
    "data": {
        "name": "testname",
        "scope": 100,
        "source-ip": "10.0.0.123"
    }
}
```
To match the event with the specified `source-ip`, the statement should be:


```
{
    "data": {
        "source-ip": [{
            "cidr": "10.0.0.0/24"
        }]
    }
}
```
### More


- A null value is different from an empty string, and null values do not match with a pattern that is used to match empty strings.
- All match patterns can be nested. In the following sample, exclusion match and prefix match are nested:
```
{
    "data": {
        "name": [{
            "anything-but": {
                "prefix": "init"
            }
        }]
    }
}
```

- OR is supported in all matching modes. You can specify the prefix and suffix as below:
```
{
    "data": {
        "topic": [
          {
            "prefix":"pre"
          },
          {
            "suffix":"suf"
          }
        ]
    }
}
```	
