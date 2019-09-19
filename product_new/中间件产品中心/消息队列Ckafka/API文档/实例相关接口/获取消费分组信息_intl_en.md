## 1. API Description

This API (GetGroupInfo) is used to get CKafka consumer group details under the user account.
API domain name: `ckafka.api.qcloud.com`

## 2. Input Parameters

The list below contains only the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/doc/api/431/5883).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
|instanceId | Yes | String| (Filter) Filter by instance ID |
|group.N| Yes |String| CKafka consumer group (Consumer-group) is an array in the format of group.0=xxx&group.1=yyy |



## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
|data|JSON Array| Consumer group information returned by this API call |
|data::group|String| CKafka consumer group |
|data::err_code|Int| Error code. It will be 0 if there are no errors |
|data::state|String| Group status (e.g., Empty, Stable, or Dead): <br>Dead: The consumer group does not exist <br>Empty: There is currently no consumer subscription in the consumer group <br>PreparingRebalance: Status of the consumer group is Preparing to Rebalance <br>CompletingRebalance: Status of the consumer group is Rebalancing<br>Stable: Consumers have joined the consumer group. The status is stable |
|data::protocol_type|String| Consumer groups will normally select `consumer` as the protocol type, but some systems use their own protocols. For example, the protocol used by kafka-connect is `connect`. **The API currently only knows the standard `consumer` protocol format  and can resolve to the assignment status of the specific partition only if this format is used** |
|data::protocol|String| Algorithms used to assign consumer partitions usually include range (which is the default option for CKafka consumer’s SDK), roundrobin and sticky |
|data::members|JSON Array| This array contains information only when state is `Stable` and protocol_type is `consumer` |
|data::members::member_id|String| Unique ID generated for a consumer in the consumer group by the coordinator |
|data::members::client_id|String| client.id information is set by clients in their own consumer SDK |
|data::members::client_host|String| Generally stores the IP address of the client |
|data::members::assignment|JSON Array | Stores the partition information assigned to the consumer |
|data::members::assignment::version|JSON Array | Assignment version information |
|data::members::assignment::topic|String| Name of the assigned topic |
|data::members::assignment::partitions|Array| Information about the assigned partition |

## 4. Samples

**Input:**

```http
 https://domain/v2/index.php?Action=GetGroupInfo&<Common Request Parameters>
```

**Output:**

```
{
	"code": 0,
	"message": "",
	"codeDesc": "Success",
	"data": [{
		"err_code": 0,
		"state": "Stable",
		"protocol_type": "consumer",
		"protocol": "range",
		"members": [{
			"member_id": "consumer-1-/10.53.88.65-2018-08-10 10:17:19:639-88206ef1-9248-43a0-9ff4-e22c3ab21e92",
			"client_id": "consumer-1",
			"client_host": "/10.53.88.65",
			"assignment": {
				"version": 0,
				"topics": [{
					"topic": "test",
					"partitions": [
						0
					]
				}]
			}
		}],
		"group": "perf-consumer-97910"
	}]
}
```

