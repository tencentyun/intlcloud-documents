You can write an SCF function to handle object creation and deletion events in a COS bucket. COS can publish events to the function and invoke it by using the event data as parameters. You can add a bucket notification configuration in the COS bucket, which can identify information such as the trigger event type and name of the function to be invoked.

Characteristics of COS triggers:

- **Push model**
COS monitors the specified bucket action (event type) and invokes the associated function to push the event data to the function. In the push model, the bucket notification is used to store the event source mapping with COS.
- **Async invocation**
A COS trigger always invokes a function asynchronously, and the result is not returned to the invoker. For more information on invocation types, please see "Invocation Types" in [How It Works](https://intl.cloud.tencent.com/document/product/583/9694).





## COS Trigger Attributes

- COS bucket (required): the configured COS bucket, which can only be a COS bucket in the same region.
- Event type (required): it supports "file upload" and "file deletion" as well as finer-grained upload and deletion events. For specific event types, please see the table below. The event type determines when the trigger triggers the function. For example, if "File upload" is selected, the function will be triggered when there is a file uploaded to the COS bucket.
<table>
<thead>
<tr>
<th>Event Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>cos:ObjectCreated:*</code></td>
<td>All upload events mentioned below can trigger the function.</td>
</tr>
<tr>
<td><code>cos:ObjectCreated:Put</code></td>
<td>The function will be triggered when a file is created through the `Put Object` API.</td>
</tr>
<tr>
<td><code>cos:ObjectCreated:Post</code></td>
<td>The function will be triggered when a file is created through the `Post Object` API.</td>
</tr>
<tr>
<td><code>cos:ObjectCreated:Copy</code></td>
<td>The function will be triggered when a file is created through the `Put Object - Copy` API.</td>
</tr>
<tr>
<td><code>cos:ObjectCreated:CompleteMultipartUpload</code></td>
<td>The function will be triggered when a file is created through the `CompleteMultipartUpload` API.</td>
</tr>
<tr>
<td><code>cos:ObjectCreated:Origin</code></td>
<td>The function will be triggered when an object is created through <a href="https://intl.cloud.tencent.com/document/product/436/31508">COS origin-pull</a>.</td>
</tr>
<tr>
<td><code>cos:ObjectCreated:Replication</code></td>
<td>The function will be triggered when an object is created through cross-region replication.</td>
</tr>
<tr>
<td><code>cos:ObjectRemove:*</code></td>
<td>All deletion events mentioned below can trigger the function.</td>
</tr>
<tr>
<td><code>cos:ObjectRemove:Delete</code></td>
<td>The function will be triggered when an object in a bucket for which versioning is not enabled is deleted through the `Delete Object` API, or an object on a specified version is deleted with `versionid`.</td>
</tr>
<tr>
<td><code>cos:ObjectRemove:DeleteMarkerCreated</code></td>
<td>The function will be triggered when an object in a bucket for which versioning is enabled or suspended is deleted through the `Delete Object` API.</td>
</tr>
<tr>
<td><code>cos:ObjectRestore:Post</code></td>
<td>The function will be triggered when an archive restoration job is created.</td>
</tr>
<tr>
<td><code>cos:ObjectRestore:Completed</code></td>
<td>The function will be triggered when an archive restoration job is completed.</td>
</tr>
</tbody></table>
- Prefix filtering (optional): prefix filtering is usually used to filter file events in a specified directory. For example, if the prefix to be filtered is `test/`, only file events in the `test/` directory can trigger the function, while those in the `hello/` directory cannot.
- Suffix filtering (optional): suffix filtering is usually used to filter file events in a specified type or with a specified suffix. For example, if the suffix to be filtered is `.jpg`, only file events of the `.jpg` type can trigger the function, while those of the `.png/` type cannot.

## COS Trigger Use Limits

- In order to avoid errors in COS event production and delivery, for the combination of each event (such as file upload/deletion) and prefix/suffix filter in each bucket, COS limits that the same rule can be bound to only one function that can be triggered. Therefore, when you create a COS trigger, do not configure repeated rules for the same COS bucket. For example, if you configure a `Created: *` event trigger in the test bucket for function A (with no filter rule configured), then the upload events (including `Created:Put` and `Created:Post`) in the test bucket cannot be bound to other functions, but you can configure an `ObjectRemove` event trigger in the test bucket for function B.

- When using prefix and suffix filter rule, in order to ensure the uniqueness of the trigger events in the same bucket, it should be noted that the same bucket cannot use overlapping prefixes, overlapping suffixes, or overlapping combinations of prefixes and suffixes to define the filter rule for the same event type. For example, if you configure a `Created: *` trigger event with prefix filter of `Log` in the test bucket for function A, then you cannot configure a `Created: *` trigger event with prefix filter of `Log` in the test bucket.

- In addition, COS triggers can only trigger functions in the same region; for example, for an SCF function created in the Guangzhou region, you can only select a COS bucket in the Guangzhou region (South China) when configuring a COS trigger. If you want to trigger a function through COS bucket events in a specific region, please create a function in that region.

- A COS trigger has limits in two dimensions: SCF and COS, as detailed below:
 - SCF dimension: one function can be bound to 10 COS triggers at most. 
 - COS dimension: the same event and prefix/suffix rule of one function can trigger up to 3 functions, and one COS bucket can be bound to 10 rules at most.


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
					"x-cos-request-id": "NWMxOWY4MGFfMjViMjU4NjRfMTUyMVxxxxxxxxx=",
					"Content-Type": "",
					"x-cos-meta-mykey": "myvalue"
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
					"Authorization": "q-sign-algorithm=sha1&q-ak=xxxxxxxxxxxxxx&q-sign-time=1545205709;1545215769&q-key-time=1545205709;1545215769&q-header-list=host;x-cos-storage-class&q-url-param-list=&q-signature=xxxxxxxxxxxxxxx"
				}
			},
			"eventQueue": "qcs:0:scf:cd:appid/1253970026:default.printevent.$LATEST",
			"reservedInfo": "",
			"reqid": 179398952
		}
	}]
}
```

The data structures are as detailed below:

| Structure | Description |
| ---------- | --- |
| Records | List structure. There may be multiple messages merged in the list. |
| event | This records the event information, including event version, event source, event name, time, queue information, request parameters, and request ID. |
| cos | This records the COS information corresponding to the event. |
| cosBucket | This records the bucket of the specific event, including bucket name, region, and user `APPID`. |
| cosObject | This records the object of the specific event, including object file path, size, custom metadata, and access URL. |

## Sample
The following is a sample COS trigger in Java for your reference:
```
https://github.com/tencentyun/scf-demo-java/blob/master/src/main/java/example/Cos.java
```


