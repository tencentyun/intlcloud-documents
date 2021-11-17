An event pattern is the definition of a pattern used by EventBridge to filter and route relevant events to the event target. It must be in the same structure as the matched events. This document describes the common event pattern types:

## Notes

The event pattern match rules are as detailed below:

- Matched events must contain all field names listed in the event pattern in the same nesting structure.
- Match between events and an event pattern is exact match down to the character and case-sensitive. During match, no standardized operations will be performed on the strings.
- Values to be matched must be in JSON format, which include strings and numeric values enclosed in quotation marks as well as keywords not enclosed in quotation marks (`true`, `false`, and `null`).

## Specified Value Match and OR and AND Operators

You can specify a field value as a match condition. Values to be matched are in a JSON array and enclosed in `[ ]`. Values in `[ ]` are in OR relationship, and keys are in AND relationship.
Taking COS data as an example, the received event is as shown below:

<dx-codeblock>
:::  json
{
	"specversion": "0",
	"id": "13a3f42d-7258-4ada-da6d-023a333b4662",
	"type": "cos:created:object",
	"source": "cos.cloud.tencent",
	"subjuect": "qcs::cos:ap-guangzhou:uid1250000000:bucketname",
	"time": "1615430559146",
	"region": "ap-guangzhou",
	"datacontenttype": "application/json;charset=utf-8",
	"resource": [
		"qcs::eb:ap-guangzhou:uid1250000000:eventbusid/eventruleid"
	],
	"data": {
		"name": "taborchen",
		"scope": 100
	}
}
:::
</dx-codeblock>


Specify the `name` value in the `data` field. Below is a rule that can be normally triggered:


<dx-codeblock>
:::  json
{
	"data": {
		"name": [
			"taborchen"
		]
	}
}
:::
</dx-codeblock>


## Prefix Match

You can match the key value by comparing the event prefix with that specified in the pattern, such as `{ "prefix": "2021-10-02" }`.

Taking COS data as an example, the received event is as shown below:


<dx-codeblock>
:::  json
{
	"specversion": "0",
	"id": "13a3f42d-7258-4ada-da6d-023a333b4662",
	"type": "cos:created:object",
	"source": "cos.cloud.tencent",
	"subjuect": "qcs::cos:ap-guangzhou:uid1250000000:bucketname",
	"time": "1615430559146",
	"region": "ap-guangzhou",
	"datacontenttype": "application/json;charset=utf-8",
	"resource": [
		"qcs::eb:ap-guangzhou:uid1250000000:eventbusid/eventruleid"
	],
	"data": {
		"name": "taborchen",
		"scope": 100
	}
}
:::
</dx-codeblock>



Specify the `name` value in the `data` field as a prefix match condition. Below is a rule that can be normally triggered:


<dx-codeblock>
:::  json
{
   "data":{
      "name":[
         {
            "prefix":"ta"
         }
      ]
   }
}
:::
</dx-codeblock>



## Exclusion Match

You can specify a field value that you want to exclude from event match, such as `{ "anything-but": "initializing" }`.

Taking COS data as an example, the received event is as shown below:


<dx-codeblock>
:::  json
{
   "specversion":"0",
   "id":"13a3f42d-7258-4ada-da6d-023a333b4662",
   "type":"cos:created:object",
   "source":"cos.cloud.tencent",
   "subjuect":"qcs::cos:ap-guangzhou:uid1250000000:bucketname",
   "time":"1615430559146",
   "region":"ap-guangzhou",
   "datacontenttype": "application/json;charset=utf-8",
   "resource":[
    "qcs::eb:ap-guangzhou:uid1250000000:eventbusid/eventruleid"
   ],
   "data":{
      "name":"taborchen",
      "scope":100
   }
}
:::
</dx-codeblock>



Specify the `name` value in the `data` field as an exclusion match condition. Below is a rule that can be normally triggered:

<dx-codeblock>
:::  json
{
	"data": {
		"name": [{
			"anything-but": ["tabor1"]
		}]
	}
}
:::
</dx-codeblock>



Specify the `name` value in the `data` field as an exclusion match condition. Below is a rule that cannot be normally triggered:


<dx-codeblock>
:::  json
{
	"data": {
		"name": [{
			"anything-but": ["taborchen"]
		}]
	}
}
:::
</dx-codeblock>


## Numeric Match

You can specify a numeric value or range of a field as a match condition, such as `{ "numeric": [ ">", 0, "<=", 5 ] }`.

Taking COS data as an example, the received event is as shown below:


<dx-codeblock>
:::  json
{
	"specversion": "0",
	"id": "13a3f42d-7258-4ada-da6d-023a333b4662",
	"type": "cos:created:object",
	"source": "cos.cloud.tencent",
	"subjuect": "qcs::cos:ap-guangzhou:uid1250000000:bucketname",
	"time": "1615430559146",
	"region": "ap-guangzhou",
	"datacontenttype": "application/json;charset=utf-8",
	"resource": [
		"qcs::eb:ap-guangzhou:uid1250000000:eventbusid/eventruleid"
	],
	"data": {
		"name": "taborchen",
		"scope": 100,
		"scope2": 100
	}
}
:::
</dx-codeblock>


Specify the `scope` value range in the `data` field to be greater than 0 and less than or equal to 100 as a numeric match condition. Below is a rule where value match can be normally triggered:

```plaintext
{
    "data":{
        "scope":[
            {
                "numeric":[
                    ">",
                    0,
                    "<=",
                    100
                ]
            }
        ]
    }
}
```




Specify the `scope` value range in the `data` field to be greater than 0 and less than 100 as a numeric match condition. Below is a rule where value match cannot be normally triggered:

```plaintext
{
    "data":{
        "scope":[
            {
                "numeric":[
                    ">",
                    0,
                    "<",
                    100
                ]
            }
        ]
    }
}
```




## IP Match

You can specify an IP address in the `data` field as a match condition. For example, in the following sample event pattern, only events whose IP is within the `10.0.0.0/24` IP range will be matched: `{ "cidr": "10.0.0.0/24" }`.

Taking COS data as an example, the received event is as shown below:


<dx-codeblock>
:::  json
{
	"specversion": "0",
	"id": "13a3f42d-7258-4ada-da6d-023a333b4662",
	"type": "cos:created:object",
	"source": "cos.cloud.tencent",
	"subjuect": "qcs::cos:ap-guangzhou:uid1250000000:bucketname",
	"time": "1615430559146",
	"region": "ap-guangzhou",
	"datacontenttype": "application/json;charset=utf-8",
	"resource": [
		"qcs::eb:ap-guangzhou:uid1250000000:eventbusid/eventruleid"
	],
	"data": {
		"name": "taborchen",
		"scope": 100,
		"source-ip": "10.0.0.123"
	}
}
:::
</dx-codeblock>



Specify the `source-ip` value in the `data` field to be within in the IP range of `10.0.0.0/24`. Below is a rule where IP match can be normally triggered:


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


## More Notes

- During pattern match, a null value is different from an empty string, and null values cannot be matched with a pattern that is used to match empty strings.
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
