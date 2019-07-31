You can write an SCF function to handle object creation and deletion events in a COS bucket. COS can publish the event to the function and call the function by using the event data as parameters. You can add a bucket notification configuration in the COS bucket, which can identify information such as the trigger event type and name of the function to be called. For more information, see the [PutBucketNotification](https://cloud.tencent.com/document/product/436/8588) API.

Characteristics of COS triggers:

- **Push model**: COS monitors the specified bucket action (event type) and calls the associated SCF function to push the event data to the function. In the push model, the bucket notification is used to store the event source mapping with COS.
- **Async call**: A COS trigger always calls a function asynchronously, and the result is not returned to the caller. For more information about calling types, see [Calling Types](https://cloud.tencent.com/document/product/583/9694#.E8.B0.83.E7.94.A8.E7.B1.BB.E5.9E.8B).

## COS Trigger Configurations

- COS bucket (required): The configured COS bucket, which can only be a COS bucket in the same region.
- Event type (required): It supports "file upload" and "file deletion", as well as finer-grained upload and deletion events. For specific event types, see the table below. The event type determines when the trigger triggers the function. For example, if "File upload" is selected, the function will be triggered when there is a file uploaded to the COS bucket.

| Event type | Description |
| ---------- | --- |
| cos: ObjectCreated:* | All upload events mentioned below can trigger the function |
| cos: ObjectCreated:Put | The function will be triggered when a file is created using the Put Object API |
| cos: ObjectCreated:Post | The function will be triggered when a file is created using the Post Object API |
| cos: ObjectCreated:Copy | The function will be triggered when a file is created using the Put Object - Copy API |
| cos: ObjectCreated:CompleteMultipartUpload | The function will be triggered when a file is created using the CompleteMultipartUploadt API |
| cos: ObjectRemove:* | All deletion events mentioned below can trigger the function |
| cos: ObjectRemove:Delete | The function will be triggered when an object in a bucket for which version management is disabled is deleted using the Delete Object API, or an object on a specified version is deleted using `versionid` |
| cos: ObjectRemove:DeleteMarkerCreated | The function will be triggered when an object in a bucket for which version management is enabled or suspended is deleted using the Delete Object API |

- Prefix and suffix filtering (optional): You can configure filtering by the prefix and suffix of the object name for the notifications. For example, you can add a suffix rule of ".jpg" when configuring "Upload event", so that the function will be only triggered when a file with the extension ".jpg" is added to the bucket.

## COS Trigger Usage Limits

- In order to avoid errors in COS event production and delivery, for the combination of each event (such as file upload/deletion) and prefix/suffix filter in each bucket, COS limits that the same rule can be bound to only one function that can be triggered. Therefore, when you create a COS trigger, do not configure repeated rules for the same COS bucket. For example, if you configure a "Created: *" event trigger in the test bucket for function A (with no filter rule configured), then the upload events (including Created:Put and Created:Post) in the test bucket cannot be bound to other functions, but you can configure an "ObjectRemove" event trigger in the test bucket for function B.

- When using prefix and suffix filter rule, in order to ensure the uniqueness of the trigger events in the same bucket, it should be noted that the same bucket cannot use overlapping prefixes, overlapping suffixes, or overlapping combinations of prefixes and suffixes to define the filter rule for the same event type. For example, if you configure a "Created: *" trigger event with prefix filter of "Log" in the test bucket for function A, then you cannot configure a "Created: *" trigger event with prefix filter of "Log" in the test bucket.

- In addition, COS triggers can only trigger functions in the same region; for example, for an SCF function created in the Guangzhou region, you can only select a COS bucket in the Guangzhou region (South China) when configuring a COS trigger. If you want to trigger an SCF function via COS bucket events in a specific region, please create a function in the same region.

## Event Message Structure for COS Trigger

When an object creation or deletion event occurs in the specified COS bucket, event data will be sent to the bound SCF function in JSON format as shown below.

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


The data structures are detailed as below:

| Parameter name| Description |
| ---------- | --- |
| Records | List structure. There may be multiple messages merged in the list |
| event | This records the event information, including event version, event source, event name, time, queue information, request parameters, and request ID |
| cos | This records the COS information corresponding to the event |
| cosBucket | This records the bucket of the specific event, including bucket name, region, and user APPID |
| cosObject | This records the object of the specific event, including object file path, size, custom metadata, and access URL |
