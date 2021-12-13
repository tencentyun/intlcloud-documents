TDMQ for Pulsar now supports Tencent Cloud SDK and Apache Pulsar SDK for the following programming languages:

>!
>- In order to be more consistent with the Pulsar open-source community, we have stopped feature updates for the Tencent Cloud SDK since April 30, 2021. We recommend you use the Apache Pulsar SDK for TDMQ for Pulsar.
>- If you are using the Tencent Cloud SDK, and you are sure that you don't use the [additional features](#external) listed below, you can directly replace it with the Apache Pulsar SDK.

<table>
<tr>
<th width="50%">Protocol Type</th><th width="50%">SDK Language</th>
</tr><tr>
<td rowspan="5">Apache Pulsar TCP Protocol</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42947">SDK for Go</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42948">SDK for Java</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42949">SDK for C++</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42950">SDK for Python</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42951">SDK for Node.js</a></td>
</tr>
</table>


### Additional features supported by Tencent Cloud SDK[](id:external)
| Feature | Description |
| ------------------ | ------------------------------------------------------------ |
| Tag filtering | Tags can be added to messages, and one message can be bound to multiple tags. Subscribers can filter messages by tag to decide whether to process them. In this way, tags can be used to optimize the business structure and save topic resources. |
| Backoff delayed message | In scenarios of retry upon failure/timeout, there is generally no need to retry many times in a short period of time, because requests are likely to still fail. It is reasonable to increase the retry time interval gradually. |

