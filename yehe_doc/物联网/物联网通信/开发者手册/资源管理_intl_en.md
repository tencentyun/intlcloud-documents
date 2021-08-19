## Feature Overview

The resource management feature is mainly used to transfer resources between devices and the platform. The following two topics are required for this feature:

- Data upstream topic (for publishing): `$resource/up/service/${productid}/${devicename}`
- Data downstream topic (for subscribing): `$resource/down/service/${productid}/${devicename}`

## Device Resource Upload

### Step 1. Create a resource upload task on the device
   
1. The device sends a message in JSON format with the following content to `$resource/up/service/${productid}/${devicename}` to create a device resource upload task:
```json
{
		 "type":"create_upload_task",
		 "size":100,
		 "name":"zxc",
		 "md5sum":"************",
}
```
2. After successful creation, the backend returns the resource upload URL through `$resource/down/service/${productid}/${devicename}` with a message in JSON format with the following content:
```
{
		 "type":"create_upload_task_rsp",
		 "size":100,
		 "name":"zxc",
		 "md5sum":"************",
		 "url":"https://iothub.cos.ap-guangzhou.myqcloud.com/********"
}
```

### Step 2. Report the resource upload progress
  
1. Resource upload uses HTTP PUT requests, so the Base64-encoded MD5 value needs to be added to the header. During the resource upload process, the device reports the resource upload progress through `$resource/up/service/${productid}/${devicename}` with a message in JSON format with the following content:
```json
{
		 "type":"report_upload_progress",
		 "name":"zxc",
		 "progress":{
				"state":"uploading",
				"percent":89,
				"result_code":0,
				"result_msg":""
			}
}
```
2. The response to progress reporting is sent to the device through `$resource/down/service/${productid}/${devicename}` with a message in JSON format with the following content:
```
{
		 "type":"report_upload_progress_rsp",
		 "result_code":0,
		 "result_msg":"ok"
}
```

## Platform Resource Delivery

### Step 1. Query the resource download URL
1. The device sends a message in JSON format with the following content through `$resource/up/service/${productid}/${devicename}` to query the download task:
```json
{
      "type":"get_download_task"
}
```
2. If there is a download task, the result will be delivered through `$resource/down/service/${productid}/${devicename}` with a message in JSON format with the following content:
```json
{
	 	"type":"get_download_task_rsp",
	 	"size":372338,
	 	"name":"AAAA",
	 	"md5sum":"a567907174*****3bb9a2bb20716fd97",
	 	"url":"https://iothub.cos.ap-guangzhou.myqcloud.com/********"
}
```

### Step 2. Report the resource download progress

1. The resource download progress is reported through `$resource/up/service/${productid}/${devicename}` with a message in JSON format with the following content:
```json
{
		 "type":"report_download_progress",
		 "name":"zxc",
		 "progress":{
				"state":"downloading",
				"percent":89,
				"result_code":0,
				"result_msg":""
			}
}
```
2. The response to progress reporting is sent to the device through `$resource/down/service/${productid}/${devicename}` with a message in JSON format with the following content:
```json
{
		 "type":"report_download_progress_rsp",
		 "result_code":0,
		 "result_msg":"ok"
}
```
