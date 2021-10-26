## Concurrency Overrun

Concurrency overrun (ResourceLimitReached) refers to a situation where the number of concurrent executions of an SCF function at the same time exceeds the [quota limit](https://intl.cloud.tencent.com/document/product/583/11637), leading to a function error. Concurrency overrun is divided into two types: sync invocation and async invocation.

### Async invocation

Types of async invocation include async invocation by [TencentCloud API trigger](https://intl.cloud.tencent.com/document/product/583/18198), [COS trigger](https://intl.cloud.tencent.com/document/product/583/9707), [scheduled trigger](https://intl.cloud.tencent.com/document/product/583/9708), [CMQ topic trigger](https://intl.cloud.tencent.com/document/product/583/11517), [CLS trigger](https://intl.cloud.tencent.com/document/product/583/38845), [MPS trigger](https://intl.cloud.tencent.com/document/product/583/39163), etc. For specific trigger invocation types, please see the relevant trigger documentation.
When concurrency overrun occurs in an async invocation, the function will automatically retry. For more information, please see [Error Types and Retry Policies](https://intl.cloud.tencent.com/document/product/583/39851).

### Sync invocation

Types of sync invocation include sync invocation by [TencentCloud API trigger](https://intl.cloud.tencent.com/document/product/583/18198), [API Gateway trigger](https://intl.cloud.tencent.com/document/product/583/12513), and [CKafka trigger](https://intl.cloud.tencent.com/document/product/583/17530).
In sync invocation, the error message will be directly returned; therefore, when an error occurs in sync invocation, the platform will not automatically retry, and the retry policy (i.e., whether to retry and the number of retries) will be determined by the invoker. In this case, the function will return a [432 status code](https://intl.cloud.tencent.com/document/product/583/35311) and will not retry the request.


## Concurrency Overrun Troubleshooting

### Viewing concurrency overrun monitoring data

You can view the number of limited times and specific logs of the function in the SCF console.

#### Viewing the number of limited times

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and select **Function Service** on the left sidebar.
2. On the **Function Service** page, select the name of the function you want to view to enter its details page.
3. In **Function Management**, select **Monitoring information** > **Limited times** to view the limited times of the function as shown below:
      ![](https://main.qcloudimg.com/raw/7c0a3f2d7cbb966e995c0041177bf86f.png)

#### Viewing function limit log


1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and select **Function Service** on the left sidebar.
2. On the **Function Service** page, select the name of the function you want to view to enter its details page.
3. In **Log Query**, select **Invocation Logs** > **Too many invocations** to view specific limit logs of the function as shown below:
      ![](https://main.qcloudimg.com/raw/e0645ba74973604fbfecbd4c4eb21248.png)


### Fixing concurrency overrun

- For **async invocation**, there is a system retry policy for concurrency overrun errors, which can automatically process concurrency overrun and retry the requests. Normally, you don't need to perform any operations for concurrency overrun in async invocation; instead, during the maximum waiting time you set, the SCF platform will automatically retry the requests.
- When an error occurs in **sync invocation**, the error message will be directly returned, and the request will not be retried.

>! In async invocation, if your business system is more sensitive to timeliness, you can reduce or minimize the impact of overrun errors on your business system by configuring reserved quota. For example, if you want that important messages will not be lost after the set maximum retention time elapses, you should configure a dead letter queue (DLQ).

#### Configuring DLQ

A DLQ is a CMQ queue under your account used to collect error event information and analyze causes of failures. If you have configured a DLQ for a function, messages in retry failures caused by overrun will be sent to it. For more information, please see [Creating Dead Letter Queue](https://intl.cloud.tencent.com/document/product/583/39704).



#### Configuring reserved quota

The reserved quota is the maximum quota used to guarantee the available concurrency of a function. By configuring the reserved quota, the function can start enough concurrent instances within the quota, and the maximum number of concurrent instances can reach the configured quota. After the reserved quota is set, the function no longer shares the concurrency quota at the account level with other functions, which can reduce the possibility of concurrency overrun and guarantee smooth function execution. For more information, please see [Reserved Concurrency](https://intl.cloud.tencent.com/document/product/583/39464).
