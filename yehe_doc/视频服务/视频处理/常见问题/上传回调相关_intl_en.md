[](id:q1)
### How do I receive callbacks?
MPS supports callbacks via message queues and serverless cloud functions, as well as in the form of HTTP.

[](id:q2)
### What do I do if I don't receive callbacks?
If you successfully uploaded a file but did not receive a notification containing the file transcoding result after a certain amount of time, possible reasons include:
- The workflow was not configured correctly. Please check the workflow settings.
- If you initiated the transcoding task through an API and the call was successful, you can use the [DescribeTaskDetail API](https://intl.cloud.tencent.com/document/product/1041/33497) to query the task progress.
- Message backlog in the task queue can cause prolonged processing or other service exceptions. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to query your queue status.

[](id:q3)
### How do I configure callbacks?
- **Message queue:**
MPS uses Tencent Cloud CMQ to send callbacks of transcoding results. You need to activate CMQ and create a queue before you can receive transcoding callbacks. You must also grant MPS the permission to write data into the queue. Then, when creating a workflow in the [MPS console](https://console.cloud.tencent.com/mps), select the queue created.
![](https://qcloudimg.tencent-cloud.cn/raw/5584b4ca5a552a92ce66c974fab16aa8.png)
- **Serverless cloud function:**
MPS has a template in SCF which you can use to enable transcoding callbacks. To receive callbacks via SCF, you need to activate SCF, create a function, and configure a trigger. For details, see [MPS Task Callback Notification](https://intl.cloud.tencent.com/document/product/1041/40337).
- **HTTP callback:**
MPS can send HTTP callbacks to a specified URL. To enable this, set `NotifyType` in [TaskNotifyConfig](https://intl.cloud.tencent.com/document/product/1041/33690) to `URL` and `NotifyUrl` to the HTTP callback URL when you call an API.

[](id:q4)
### Are callbacks charged?
- For CMQ usage and fees, please see [CMQ > Purchase Guide](https://intl.cloud.tencent.com/document/product/406/38676).
- For SCF usage and fees, please see [SCF > Purchase Guide > Billing Overview](https://intl.cloud.tencent.com/document/product/583/17299).
- HTTP callbacks are free currently.

[](id:q5)
### How to upload video files?
MPS supports the following video upload methods:

- **Upload via console**: Log in to the [COS console](https://console.cloud.tencent.com/cos5) and [upload](https://intl.cloud.tencent.com/document/product/436/13321) local video files to a COS bucket. You can use this method if the number of videos to upload is small.
- **Upload via client**: Upload local video files to a COS bucket through the COS SDK. COS supports simple upload for small files and multipart upload for large ones. You can resume from breakpoints during upload and pause, resume, or cancel an upload. This method is suitable for UGC and PGC upload. For detailed directions, see the documents below.
  - [Simple Upload](https://intl.cloud.tencent.com/document/product/436/14113)
  - [Multipart Upload](https://intl.cloud.tencent.com/document/product/436/14112)

[](id:q6)
### How do I configure automatic transcoding upon upload?
Create a workflow, select the template you created for transcoding, and enable the workflow. For details about workflow settings, see [Setting Workflow](https://intl.cloud.tencent.com/document/product/1041/33492).

[](id:q7)
### Can I upload video files in PS format? 
No, you can’t. See the table below for supported formats.

| Format | Video Codec            | Audio Codec        |
| -------- | ----------------------- | ------------------- |
| MP4      | H.264, H.265            | AAC                 |
| FLV      | H.264, H.265            | AAC                 |
| MOV      | H.264, H.265, MPEG4     | AAC                 |
| WMV      | WMV1, WMV2              | WMA1, WMA2          |
| MKV      | H264, VP8, MPEG4        | AAC                 |
| AVI | H264, WMV1, WMV2, MPEG4 |  AAC, WMA1, WMA2 |
| RMVB     | RealVideo                 | RAAC, RACP          |
| TS | H.264, MP1V, MP4V | MP1, MP2, MP3, MP4A  |
| MPG      | MPEG1, MPEG2            | MP2                 |
| 3GP      | H263, MPEG4             | AMR, AAC            |

[](id:q8)
### Why aren’t my videos output at the specified bitrate?
Without compromising visual experience, MPS reduces the quality of unimportant frames to lower the output bitrate.
If you want your videos to be output at the specified bitrate, please provide us the ID of your transcoding template so that we can make adjustment accordingly.

[](id:q9)
### Can videos stored in COS be compressed for preview?
Currently, COS does not support automatic video compression for preview, but CI has a video transcoding feature that essentially generates a new file. The latter allows you to change parameters such as codec, resolution, and bitrate.

