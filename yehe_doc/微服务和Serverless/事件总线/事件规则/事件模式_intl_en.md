An event pattern defines how EventBridge filters events and routes them to the event target. It must be in the same structure as the matched events. This document describes the common event pattern types:

### Principle of Matching

The event pattern match rules are as detailed below: 

- Matched events must contain all field names listed in the event pattern in the same nesting structure.
- Match between events and an event pattern is exact match down to the character and case-sensitive. During match, no standardized operations will be performed on the strings.
- Values to be matched must be in JSON format, which include strings and numeric values enclosed in quotation marks as well as keywords not enclosed in quotation marks (`true`, `false`, and `null`).


### Specifying Condition and Operator

You can specify a field value as a match condition. Values to be matched are in a JSON array and enclosed in `[ ]`. Values in `[ ]` are in OR relationship, and keys are in AND relationship.
Taking COS data as an example, the received event is as shown below: 

<dx-codeblock>
:::  json
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
:::
</dx-codeblock>


For the above event, if you specify the `name` value in the `data` field as a match condition, a rule that can be normally triggered is as follows: 


<dx-codeblock>
:::  json
{
	"data": {
		"name": [
			"testname"
		]
	}
}
:::
</dx-codeblock>

<span id=2></span>
### Prefix Matching

You can perform key value matching by comparing the event prefix with that specified in the pattern, such as `{ "prefix": "2021-10-02" }`.

Taking COS data as an example, the received event is as shown below: 


<dx-codeblock>
:::  json
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
:::
</dx-codeblock>



If you specify the `name` value in the `data` field as a prefix match condition, a rule that can be normally triggered is as follows: 


<dx-codeblock>
:::  json
{
   "data":{
      "name":[
         {
            "prefix":"te"
         }
      ]
   }
}
:::
</dx-codeblock>

### Suffix Matching
You can perform key value matching by comparing the event suffix with that specified in the pattern, such as `{ "suffix": ".txt" }`.

Taking TDMQ data as an example, the received event is as shown below: 

<dx-codeblock>
:::  json
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
:::
</dx-codeblock>

If you specify the `topic` value in the `data` field as a suffix match condition, a rule that can be normally triggered is as follows: 

<dx-codeblock>
:::  json
{
	"data": {
		"topic": [{
			"suffix":"/topic-1"
		}]
	}
}
:::
</dx-codeblock>


## Exclusion Matching

You can specify a field value that you want to exclude from event match, such as `{ "anything-but": "initializing" }`.

Taking COS data as an example, the received event is as shown below: 


<dx-codeblock>
:::  json
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
:::
</dx-codeblock>



If you specify the `name` value in the `data` field as an exclusion match condition, a rule that can be normally triggered is as follows: 

<dx-codeblock>
:::  json
{
	"data": {
		"name": [{
			"anything-but":"test1"
		}]
	}
}
:::
</dx-codeblock>



If you specify the `name` value in the `data` field as an exclusion match condition, a rule that cannot be normally triggered is as follows: 


<dx-codeblock>
:::  json
{
	"data": {
		"name": [{
			"anything-but":"testname"
		}]
	}
}
:::
</dx-codeblock>

### Inclusion Matching
You can specify a field to be included in data as a match condition, such as `{ "contain": ".txt" }`.

Taking TDMQ data as an example, the received event is as shown below: 

<dx-codeblock>
:::  json
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
:::
</dx-codeblock>

If you specify the `topic` value in the `data` field as an inclusion match condition, a rule that can be normally triggered is as follows: 

<dx-codeblock>
:::  json
{
	"data": {
		"topic": [{
			"contain":"topic-1"
		}]
	}
}
:::
</dx-codeblock>


### Array Matching

You can filter array fields with syntaxes, such as `{"array": "{\"key1:\"value1\"}"}`.
To generate event rules based on a field in the `data` attribute, such as DTS data, the received event is as follows:  

<dx-codeblock>
:::  json
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
:::
</dx-codeblock>



For the above event, to match the rule with the `columns` fields, the triggered rule is as follows:  


<dx-codeblock>
:::  json
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
:::
</dx-codeblock>



Multiple filters are combined with AND. 


<dx-codeblock>
:::  json
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
:::
</dx-codeblock>




### IP Matching

You can specify an IP address in the `data` field as a match condition. For example, in the following sample event pattern, only events whose IP is within the `10.0.0.0/24` IP range will be matched: `{ "cidr": "10.0.0.0/24" }`.

Taking COS data as an example, the received event is as shown below: 


<dx-codeblock>
:::  json
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
:::
</dx-codeblock>



If you specify `source-ip` in the `data` field as a match condition, a rule that can be normally triggered is as follows: 


<dx-codeblock>
:::  json
{
	"data": {
		"source-ip": [{
			"cidr": "10.0.0.0/24"
		}]
	}
}
:::
</dx-codeblock>


### Notes

- A null value is different from an empty string, and null values do not match with a pattern that is used to match empty strings.
- All match patterns can be nested. In the following sample, exclusion match and prefix match are nested:
  <dx-codeblock>
  :::  json
  {
  "data": {
  	"name": [{
  		"anything-but": {
  			"prefix": "init"
  		}
  	}]
  }
  }
  :::
  </dx-codeblock>
