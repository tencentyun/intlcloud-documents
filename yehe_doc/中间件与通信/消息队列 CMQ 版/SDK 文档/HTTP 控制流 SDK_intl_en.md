## Overview
This document describes the control flow APIs and SDK use methods of TDMQ for CMQ. For data flow APIs (related to message sending/receiving), see [HTTP Data Flow API Overview](https://intl.cloud.tencent.com/document/product/1111/46396).

The control flow APIs of TDMQ for CMQ are as listed below:

| API | Description      |
| :----------------------------------------------------------- | :----------------------------- |
| [CreateCmqQueue](https://intl.cloud.tencent.com/document/api/1110/44169) | Creates TDMQ for CMQ queue |
| [CreateCmqSubscribe](https://intl.cloud.tencent.com/document/api/1110/45168) | Creates TDMQ for CMQ subscription |
| [CreateCmqTopic](https://intl.cloud.tencent.com/document/api/1110/44168) | Creates TDMQ for CMQ topic |
| [DeleteCmqQueue](https://intl.cloud.tencent.com/document/api/1110/44167) | Deletes TDMQ for CMQ queue |
| [DeleteCmqSubscribe](https://intl.cloud.tencent.com/document/api/1110/44166) | Deletes TDMQ for CMQ subscription |
| [DeleteCmqTopic](https://intl.cloud.tencent.com/document/api/1110/44165) | Deletes TDMQ for CMQ topic |
| [DescribeCmqDeadLetterSourceQueues](https://intl.cloud.tencent.com/document/api/1110/44164) | Enumerates dead letter source queues in TDMQ for CMQ |
| [DescribeCmqQueueDetail](https://intl.cloud.tencent.com/document/api/1110/44163) | Queries the details of TDMQ for CMQ queue |
| [DescribeCmqQueues](https://intl.cloud.tencent.com/document/api/1110/44162) | Queries all TDMQ for CMQ queues |
| [DescribeCmqSubscriptionDetail](https://intl.cloud.tencent.com/document/api/1110/44161) | Queries the details of TDMQ for CMQ subscription |
| [DescribeCmqTopicDetail](https://intl.cloud.tencent.com/document/api/1110/44160) | Queries the details of TDMQ for CMQ topic |
| [DescribeCmqTopics](https://intl.cloud.tencent.com/document/api/1110/44159) | Enumerates all TDMQ for CMQ topics |
| [ModifyCmqQueueAttribute](https://intl.cloud.tencent.com/document/api/1110/44158) | Modifies TDMQ for CMQ queue |
| [ModifyCmqSubscriptionAttribute](https://intl.cloud.tencent.com/document/api/1110/44157) | Modifies TDMQ for CMQ subscription |
| [ModifyCmqTopicAttribute](https://intl.cloud.tencent.com/document/api/1110/44156) | Modifies TDMQ for CMQ topic |
| [RewindCmqQueue](https://intl.cloud.tencent.com/document/api/1110/44155) | Rewinds TDMQ for CMQ queue |
| [UnbindCmqDeadLetter](https://intl.cloud.tencent.com/document/api/1110/44154) | Unbinds TDMQ for CMQ dead letter queue |


## Directions
TDMQ for CMQ's control flow SDK uses the new version of APIs. Taking **the API for creating a TDMQ for CMQ queue** as an example, the specific usage is as follows:



#### 1. Log in to the [TencentCloud API](https://console.intl.cloud.tencent.com/api/explorer) console.

#### 2. Select **API Explorer** > **Tencent Distributed Message Queue** > **CMQ Management APIs**.

#### 3. Select a specific API and enter the input parameters.
The input parameters are as detailed below:

| Parameter | Description |
| ------------------- | ------------------------------------------------------------ |
| QueueName | Queue name, which must be unique under the same account in the same region. It can contain up to 64 letters, digits, and hyphens and must begin with a letter. |
| MaxMsgHeapNum | Maximum number of heaped messages. The value range is 1,000,000–10,000,000 during the beta test and can be 1,000,000–1,000,000,000 after the product is officially released. The default value is 10,000,000 during the beta test and will be 100,000,000 after the product is officially released. |
| PollingWaitSeconds | Long polling wait time for message reception. Value range: 0–30 seconds. Default value: 0. |
| VisibilityTimeout | Message visibility timeout period. Value range: 1–43200 seconds (i.e., 12 hours). Default value: 30. |
| MaxMsgSize | Maximum message length. Value range: 1024–65536 bytes (i.e., 1–64 KB). Default value: 65536. |
| MsgRetentionSeconds | Message retention period. Value range: 60–1296000 seconds (i.e., 1 minute–15 days). Default value: 345600 (i.e., four days). |
| RewindSeconds | Whether to enable the message rewinding feature for a queue. Value range: 0–msgRetentionSeconds, where 0 means not to enable this feature, while `msgRetentionSeconds` indicates that the maximum rewindable period is the message retention period of the queue. |
| Transaction | 1: transaction queue; 0: general queue. |
| FirstQueryInterval | First lookback interval. |
| MaxQueryCount | Maximum number of lookbacks. |
| DeadLetterQueueName | Dead letter queue name. |
| Policy | Dead letter policy. 0: message has been consumed multiple times but not deleted; 1: `Time-To-Live` has elapsed. |
| MaxReceiveCount | Maximum receipt times. Value range: 1–1000. |
| MaxTimeToLive | Maximum period in seconds before an unconsumed message expires, which is required if `policy` is 1. Value range: 300–43200. This value should be smaller than `msgRetentionSeconds` (maximum message retention period). |
| Trace | Whether to enable message trace. true: yes; false: no. If this field is not configured, the feature will not be enabled. |

#### 4. Call online.

After entering the input parameters, select the **Online Call** tab at the top of the page and click **Send Request**. The returned result is as follows:

![](https://qcloudimg.tencent-cloud.cn/raw/8b9a107ed03c44c39f1fecb86771319b.png)

#### 5. Generate sample code.

After the verification is completed, select the target programming language in the code box on the **Code Generation** tab to generate the corresponding sample code.
Sample code for Java:

```java
import com.tencentcloudapi.common.Credential;
import com.tencentcloudapi.common.profile.ClientProfile;
import com.tencentcloudapi.common.profile.HttpProfile;
import com.tencentcloudapi.common.exception.TencentCloudSDKException;
import com.tencentcloudapi.tdmq.v20200217.TdmqClient;
import com.tencentcloudapi.tdmq.v20200217.models.*;

public class CreateCmqQueue
{
    public static void main(String [] args) {
        try{
            // Instantiate an authentication object. Pass in `secretId` and `secretKey` of your Tencent Cloud account as the input parameters and keep them confidential
            // You can get them at https://console.intl.cloud.tencent.com/cam/capi
            Credential cred = new Credential("SecretId", "SecretKey");
            // (Optional) Instantiate an HTTP option
            HttpProfile httpProfile = new HttpProfile();
            httpProfile.setEndpoint("tdmq.tencentcloudapi.com");
            // Instantiate a client option (optional; skip if no special requirements are present)
            ClientProfile clientProfile = new ClientProfile();
            clientProfile.setHttpProfile(httpProfile);
            // Instantiate the client object of the requested product. `clientProfile` is optional
            TdmqClient client = new TdmqClient(cred, "ap-guangzhou", clientProfile);
            // Instantiate a request object. Each API corresponds to a request object
            CreateCmqQueueRequest req = new CreateCmqQueueRequest();
            req.setQueueName("queen");
            req.setPollingWaitSeconds(10L);
            req.setVisibilityTimeout(10L);
            req.setMaxMsgSize(1048576L);
            req.setMsgRetentionSeconds(345600L);
            // The returned `resp` is an instance of `CreateCmqQueueResponse` which corresponds to the request object
            CreateCmqQueueResponse resp = client.CreateCmqQueue(req);
            // A string response packet in JSON format is output
            System.out.println(CreateCmqQueueResponse.toJsonString(resp));
        } catch (TencentCloudSDKException e) {
            System.out.println(e.toString());
        }
    }
}
```
