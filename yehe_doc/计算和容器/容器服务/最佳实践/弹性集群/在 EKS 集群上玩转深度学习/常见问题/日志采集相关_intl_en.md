
This document offers answers to questions that you may have when [building a deep learning container image](https://intl.cloud.tencent.com/document/product/457/42059) and [running deep learning in EKS](https://intl.cloud.tencent.com/document/product/457/42060).




### How do I persistently store logs?

As EKS containers will be terminated after use, you can view logs only when the Pod is in **Running** status. Once the Pod status becomes **Completed**, the following error will be reported:

```shell
Error from server (InternalError): Internal error occurred: can not found connection to pod ***
```

The following describes persistent log storage methods:
- [Redirect](#redirect)
- [Log collection configuration](#configure-log-collection)




#### Redirect[](id:redirect)
The redirect method is simpler. You only need to change the terminal `stdout` to which `kubectl logs` are output to a file for persistent storage. To do so, run the following command:
<dx-codeblock>
:::  shell
kubectl logs -f tf-cnn >> info.log
:::
</dx-codeblock>

However, when using the redirect method, you should note that the output stream will not flow to the terminal; that is, you cannot view the log output progress on the terminal. If you want to output the content to the screen while storing the command output to a file, you can do so in the following two methods:
- Use a pipe and the `tee` command. Run the following command:
<dx-codeblock>
:::  shell
kubectl logs -f tf-cnn |tee info.log
:::
</dx-codeblock>
- You can also run the `logsave` command to output the content to the screen while storing the command output to the file as follows:
<dx-codeblock>
:::  shell
logsave [-asv] info.log kubectl logs -f tf-cnn
:::
</dx-codeblock>
>?The advantage of `logsave` over `tee` is that with `logsave`, the time will be recorded for each input, and there is a certain spacing between logs, which makes it easier for you to find logs.

The above three commands all have a shortcoming: as their redirect is based on the `kubectl logs` output, they must be used when the Pod is in **Running** status, and they are only used to view logs after the Pod is in **Completed** status.
The redirect method is applicable to scenarios with only a small number of logs and with no requirements for outputting and searching for a high number of logs. If your requirements are not high, we recommend you use the redirect method.






#### Log collection configuration[](id:configure-log-collection)

In EKS, you can configure log collection either through environment variables or CRDs.

<dx-tabs>
::: Using environment variables to configure log collection
1. Configure log collection as instructed in [Using Environment Variables to Configure Log Collection](https://intl.cloud.tencent.com/document/product/457/37907) 
 2. If you want to use keys for authorization, you can create a `Secret` in `Opaque` type and create two keys (`SecretId` and `SecretKey`). The values of `SecretId` and `SecretKey` can be obtained in [API Key](https://console.cloud.tencent.com/cam/capi).
 3. You can find the created `Secret` after enabling log collection and associate `SecretId` with `SecretKey` 
4. Get the raw logs in the console, switch to the table view, and format the JSON strings 


This method has a problem: the log collection feature of EKS works by sending the collected logs as JSON strings to the specified consumer, but the timestamps of the collected JSON strings are at the second level 

In this case, logs are displayed in the console at the second level, and the logs displayed on the search and analysis page can be sorted only by second but cannot be output sequentially at a finer time granularity. However, sometimes a large number of logs are output in a short while, for which a millisecond granularity is often required. Therefore, we recommend the CRD-based configuration method.
:::
::: Using CRD to configure log collection (recommended)
1. Configure log collection as instructed in [Configuring Log Collection via the Console](https://intl.cloud.tencent.com/document/product/457/40585).
2. After enabling log collection, create a log rule as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/3ac6a3ba63cb0a8def745131b36c363f.png)
On the search and analysis page, you can see that the time granularity is millisecond, and logs can be output sequentially by millisecond.
>?CRD-Based log collection configuration also supports separating raw logs with regular expressions, which is more flexible but more complicated than configuration through environment variables.


#### Problems that may occur in log collection configuration
- If you select CRD-based log collection configuration, please use a browser with the Chrome kernel, such as the latest version of Edge and Chrome instead of early versions of Edge. As the frontend may not support legacy kernels, problems such as improper display of sample logs and failure to select automatically generated regular expressions may occur.
- After you use CRDs to configure log collection, you do not need to perform other operations when creating a Pod, and the output logs will be collected automatically. If no logs are collected, check whether the server group is full. After there is any available server in the server group, you can restart the Pod of `cls-provisioner`.
:::
</dx-tabs>

