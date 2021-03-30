## Feature Overview

**Tencent Cloud Tag:** tag is a resource management tool provided by Tencent Cloud. You can use tags to categorize, search for, and aggregate Tencent Cloud resources. A tag has two parts: tag key and tag value. You can create a tag by defining its tag key and tag value based on conditions such as the resource usage and resource owner. For more information, please see [Product Overview](https://intl.cloud.tencent.com/document/product/651/13334).

**Configure alarm by tag**: Tencent Cloud Tag enables you to quickly filter Tencent Cloud resources under bound tags. This can help promptly update alarm policies for tagged instance quantity changes, reduce the costs of secondary modification of alarm policies, and implement tag-based automatic monitoring.

## Use Cases

<table>
<tr>
<th>Use Case</th>
<th>Example</th>
</tr>
<tr>
<td>Configure alarm policies by instance importance</td>
<td>Primary instances, secondary instances, etc.</td>
</tr>
<tr>
<td>Configure alarm policies by business module</td>
<td>Business A, business B, etc.</td>
</tr>
<tr>
<td>Configure alarm policies by alarm recipient</td>
<td>OPS, R&D, etc.</td>
</tr>
</table>

## Limits

- The tag feature currently is only supported for CVM - basic monitoring and will be supported for more Tencent Cloud services in the future.
- **If the alarm object is bound to the "tag" type, it temporarily cannot be switched to the alarm object type of instance ID, instance group, or all projects. If you want to switch the type, you need to create an alarm policy again.**
- Each resource can be associated with up to 50 different tag keys.
- Each user can create up to 1,000 tag keys.
- Each tag key can be associated with up to 1,000 tag values.

## Directions

- [Creating tag](#step1)
- [Configuring alarm by tag](#step2)
- [Associating instance with tag](#step3)
  

<span id= "step1"></span>

### Creating tag

You can create tags according to different use cases and needs.

1. Go to the tag list page in the [Tag console](https://console.cloud.tencent.com/tag/taglist).
2. On the tag list page, click **Create** and enter the tag key and tag value (which can be left empty). You can create multiple tags for different use cases.
   ![](https://main.qcloudimg.com/raw/7f71df3dfee7168fc958fdcf5c107a5f.png)
3. After entering the information, click **OK**.

<span id= "step2"></span>


### Configuring alarm by tag

1. Go to the alarm policy page in the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/alarm2/policy).
2. Click **Create** to enter the alarm policy creation page, select the **Tag** type in the **Alarm Object** column, and select the corresponding tag key and tag value. For other configuration items, please see [Creating Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38916).
   ![](https://main.qcloudimg.com/raw/6f84d0ab70625f8bf8360fb9c0ffa90b.png)
3. After completing the configuration, click **Complete**.

<span id= "step3"></span>

### Associating tag

>?The following describes how to associate Tencent Cloud services with tags with a CVM instance as an example. You can follow the steps below to associate instances of the same service with the same tag to facilitate the filtering and management of such instances.

You can associate tags in two ways:

- When you purchase new CVM instances, you can associate them with tags according to their use cases to automatically bind them to alarm policies under the tags.
- You can associate existing CVM instances with tags according to their use cases to automatically bind them to alarm policies under the tags.

#### Associating new CVM instance with tag

1. Go to the instance list page in the [CVM console](https://console.cloud.tencent.com/cvm/instance).
2. Click **Create** to create a CVM instance as instructed in [Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855). When configuring the instance in step 2, select the corresponding tag key and tag value in the **Tag** column.
![](https://main.qcloudimg.com/raw/86a07bb2777e31eb9eb283e7ffd7c747.png)

#### Associating existing CVM instance with tag

1. Go to the instance list page in the [CVM console](https://console.cloud.tencent.com/cvm/instance).
2. On the instance list page, find the target instance and select **More** > **Instance Settings** > **Edit Tag** in the **Operation** column.
3. In the tag editing window, associate the instance with the corresponding tag key and value and click **OK**.
![](https://main.qcloudimg.com/raw/4a18fcd3d6d61af1b6462954a47ba2b0.png)



