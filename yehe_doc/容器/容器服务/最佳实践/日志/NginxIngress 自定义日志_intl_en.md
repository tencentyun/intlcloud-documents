

By integrating CLS, TKE provides a complete set of productized capabilities to collect and consume Nginx-ingress logs. For more information, see [Nginx-ingress Log Configuration](https://intl.cloud.tencent.com/document/product/457/38983). If the default log index doesn't meet your needs, you can customize the index. This document describes how to update the log index of Nginx Ingress.

## Prerequisites

1. Nginx Ingress is on v1.1.0 or later. Log in to the [TKE console](https://console.cloud.tencent.com/tke2), select **Cluster Details** > **Add-On Management**, and you can view the version of the Nginx Ingress add-on.
![](https://qcloudimg.tencent-cloud.cn/raw/e0a14da8c010ab6bc909b0d02ed69c07.png)
2. The Nginx Ingress instance is on v0.49.3 or later. Log in to the [TKE console](https://console.cloud.tencent.com/tke2), select **Cluster Details** > **Services and Routes** > **NginxIngress**, and click **View YAML** on the right of the target instance. In the YAML file, the `ccr.ccs.tencentyun.com/paas/nginx-ingress-controller` image must be on v0.49.3 or later.
![](https://qcloudimg.tencent-cloud.cn/raw/99a2f973e95d1fa62b48ae9c91093ed3.png)
- You have enabled the log service of Nginx Ingress as instructed in [Nginx-ingress Log Configuration](https://intl.cloud.tencent.com/document/product/457/38983#tke-nginx-ingress-.E9.87.87.E9.9B.86.E6.97.A5.E5.BF.97).

## Directions

>! To modify the log structure, you need to understand the log stream of Nginx Ingress, which consists of log output, collection, indexing, and configuration. Here, if log output or collection is missing or incorrectly configured, log modification will fail. 


[](id:step1)
### Step 1. Modify the log output format of the Nginx Ingress instance

The log configuration of the Nginx Ingress instance is in the master configuration ConfigMap `instance name-ingress-nginx-controller`, where you need to modify the `log-format-upstream` key.
![](https://qcloudimg.tencent-cloud.cn/raw/bf5cac23f297ca1e08b1bc6f61370271.png)

#### Sample
Add two consecutive strings `$namespace` and `$service_name` to the end of a log.
![](https://qcloudimg.tencent-cloud.cn/raw/8e2ac7866c60bf896cd2895056b5124a.png)

For more information on log fields of Nginx Ingress, see [Log format](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/log-format/).

### Step 2. Modify the format for collecting and reporting cluster logs to Agent

The cluster log collection rules are in a resource object of the `logconfigs.cls.cloud.tencent.com` type. Log in to the [TKE console](https://console.cloud.tencent.com/tke2), select **Cluster Details** > **Kubernetes resource manager**, find the `instance name-ingress-nginx-controller` resource object, and you can click **Edit YAML** to modify it.
![](https://qcloudimg.tencent-cloud.cn/raw/6f3cc462ceddc67dfd7030737516b41f.png) 

You need to modify the following fields:

- beginningRegex: The regular expression of the log start.
- keys: Log fields.
- logRegex: The regular expression of the log end.

The regular expressions match the Nginx log row format. We recommend you add the fields to the existing Nginx log format, declare them at the end of `keys`, and add their regular expression parsing results to the end of `beginningRegex` and `logRegex` respectively.

#### Sample
Add the two keys in [step 1](#step1) to the end of `keys` and add the regular expression strings to the end of `beginningRegex` and `logRegex` respectively:

![](https://qcloudimg.tencent-cloud.cn/raw/6298797d480e73af7a9c3aeaab531036.png)

### (Optional) Step 3. Modify the log index format of CLS 

To search for a field, you need to add the index of the new field in the corresponding log topic in the CLS console as instructed in [Configuring Index](https://intl.cloud.tencent.com/document/product/614/39594). Then, all collected logs can be searched for by the index.

![](https://qcloudimg.tencent-cloud.cn/raw/41e3e814cbc4494ad487a788632576a2.png)
![](https://qcloudimg.tencent-cloud.cn/raw/7a5577ed28bb662bd7d604e8aaadeeb2.png)

## Restoring the Initial Settings

As log rule modification is complicated and involves regular expressions, any incorrect step can cause log collection failure. If a log collection error occurs, we recommend you restore to the initial log collection capabilities by disabling the log collection feature and [enabling it](https://intl.cloud.tencent.com/document/product/457/32419) again.
