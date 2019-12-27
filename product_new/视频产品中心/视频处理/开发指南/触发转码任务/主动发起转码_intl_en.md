In MPS, you can initiate a transcoding task in the following methods:
- You can set up a workflow to automatically trigger a transcoding task upon file upload.
- You can call an API to manually initiate a transcoding task for an uploaded file.
 
For more information on the first method, please see [Setting Workflow](https://intl.cloud.tencent.com/document/product/1041/33475). This document describes how to call an API to initiate a task.

## Initiating a Transcoding Task
You can call the PocessMedia API to initiate a transcoding task for a single file. If the API is successfully called, the task ID, i.e., the `TaskID` field in the result, will be returned.

### Sample request
```
https://mps.tencentcloudapi.com/?Action=ProcessMedia
&InputInfo.Type=COS
&InputInfo.CosInputInfo.Bucket=TopRankVideo-125*****65
&InputInfo.CosInputInfo.Region=ap-chongqing
&InputInfo.CosInputInfo.Object=/movie/201907/WildAnimal.mov
&MediaProcessTask.TranscodeTaskSet.0.Definition=20
&MediaProcessTask.TranscodeTaskSet.1.Definition=30
&MediaProcessTask.TranscodeTaskSet.2.Definition=40
&<Common request parameter>
```

### Sample response
```
{
  "Response": {
    "RequestId": "6ca31e3a-6b8e-4b4e-9256-fdc700064ef3",
    "TaskId": "125****65-procedurev2-bffb15f07530b57bc1aabb01fac74bca"
  }
}
```

If you have configured CMQ for event notification, you will receive a notification upon completion of this task. In addition to receiving event notifications through CMQ, you can also use the [DescribeTaskDetail](https://intl.cloud.tencent.com/document/product/1041/33497) API to query the task result. The input parameter is `TaskId` returned by the ProcessMedia API.
