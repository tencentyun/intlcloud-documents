### How to receive callbacks?

For the sake of service reliability and data security, **MPS only supports callback notification based on CMQ.**

### What if I don't receive callbacks?

If you successfully uploaded a file but did not receive the callback message of the file transcoding result after a certain amount of time, possible reasons include:

  - The workflow is configured incorrectly. Please check the workflow settings.
  - If you initiated the transcoding task through an API and a success was returned, you can use the [DescribeTaskDetail](https://cloud.tencent.com/document/product/862/37035) API to query the task progress.
  - Message backlog in the task queue causes prolonged processing or other service exceptions. You can [submit a ticket](https://cloud.tencent.com/workorder/category) to query your queue status.

### How to set up callback?

MPS uses Tencent Cloud CMQ to send transcoding result callback messages. You need to activate CMQ in advance and create a queue before you can receive transcoding callback notifications. In addition, you need to grant MPS permission to write data into the queue. Then, you can set the corresponding queue parameters when creating a workflow in the [MPS Console](https://console.cloud.tencent.com/mps).
![](https://main.qcloudimg.com/raw/287a7f5024e3556abadd8023fbd0822a.png)

### Does CMQ incur fees?

For CMQ-related usage and fee information, please see [CMQ Cost Description](https://intl.cloud.tencent.com/document/product/406/13648).
