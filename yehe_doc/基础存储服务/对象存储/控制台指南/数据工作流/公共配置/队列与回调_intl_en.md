## Overview

When you activate the data processing workflow service, the system will **automatically create** a user queue for you. When you submit a job, the job will be arranged in the queue first and executed in sequence according to the priority and order of submission. You can also set a **callback rule** to stay up to date with the job or workflow progress, and the system will send the processing result and status information to the specified address. The queues for different services are as follows:

| Feature Name | Queue Name            |
| -------- | ------------------- |
| Media processing | queue-1             |
| Speech recognition | queue-speech-1      |
| File preview | queue-doc-process-1 |

>? Currently, one feature supports only one queue. If you want more concurrent queues, [contact us](https://intl.cloud.tencent.com/contact-sales).
>

## Directions

### Enabling or pausing queue

You can enable or pause a queue in its **Operation** column.

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Select **Bucket List** on the left sidebar.
3. Click the name of the bucket for video storage.
4. On the left sidebar, select **Data Processing Workflow** > **Common Configuration**. Then, click **Queues and Callbacks** to enter the queue configuration page to enable or pause a queue.
>! After a queue is paused, its jobs will stop, and you cannot use the [job](https://intl.cloud.tencent.com/document/product/436/46409) and [workflow](https://intl.cloud.tencent.com/document/product/436/46408) features in the console.
>

### Setting callback rule

COS supports user-defined callback URLs. After an event is completed, the system sends an HTTP POST request whose body contains notification content to a user-defined callback URL. You can use the configured callback URL to learn about the processing progress and status so that you can perform other operations as needed.

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Select **Bucket List** on the left sidebar.
3. Click the name of the bucket for video storage.
4. On the left sidebar, select **Data Processing Workflow** > **Common Configuration**. Then, click **Queues and Callbacks** to enter the queue configuration page.
5. Click **Configure Callback Rule** in the **Operation** column of the target queue.
6. In the pop-up window, set the status to enable or disable callback.
![](https://qcloudimg.tencent-cloud.cn/raw/10e883741266deb93d366ec8fdcc8635.png)
When enabling callback, you need to specify a URL for the system to send HTTP requests. For more information on callback, see [Callback content](#1).


<span id=1></span>
### Callback content

After a job is completed, the system will send the following callback content to the configured callback URL:
```shell
<Response>
      <JobsDetail></JobsDetail>
      <NonExistJobIds></NonExistJobIds>
</Response>
```

The parameters are described as follows:

| Parameter           | Description                                                         | Type      |
| :------------- | :----------------------------------------------------------- | :-------- |
| JobsDetail     | Job details. Same as `Response.JobsDetail` in `CreateMediaJobs`. | Container |
| NonExistJobIds | List of non-existing job IDs queried. If all jobs exist, this parameter is not returned.             | String    |
