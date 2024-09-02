Common parameters are required in every API for authenticating users and the APIs. Unless otherwise required, they will not be described in individual API documents.

<table class="t">
<tbody><tr>
<th> <b>Parameter</b>
</th><th> <b>Type</b>
</th><th> <b>Description</b>
</th><th width="50"> <b>Required</b>
</th></tr>
<tr>
<td> Action
</td><td> String
</td><td> Command API name of a specific operation, such as  DescribeInstances.
</td><td> Yes
</td></tr>
<tr>
<td> Region
</td><td> String
</td><td>Identifies the region where the instance you want to operate on resides. Valid values: <br>
gz: Guangzhou; sh: Shanghai; bj: Beijing; cd: Chengdu<br>
cq: Chongqing; hk: Hong Kong (China); sg: Singapore; th: Bangkok<br>
kr: Seoul; jp: Tokyo; ru: Moscow; de: Frankfurt<br>
in: Mumbai; usw: Silicon Vally; use: Virginia<br>
</td><td> Yes
</td></tr>
<tr>
<td> Timestamp
</td><td> UInt
</td><td> Current Unix timestamp.
</td><td> Yes
</td></tr>
<tr>
<td> Nonce
</td><td> UInt
</td><td> A random positive integer, which is used in conjunction with `Timestamp` to prevent replay attacks.
</td><td> Yes
</td></tr>
<tr>
<td> SecretId
</td><td> String
</td><td> SecretId applied from Tencent Cloud which is used for identification. Each SecretId corresponds to a unique SecretKey, while SecretKey is used to generate request Signature.<br>For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/1526">Signature Method</a>.
</td><td> Yes
</td></tr>
<tr>
<td> Signature
</td><td> String
</td><td>Request signature, which is used to verify the validity of the current request. For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/1526" title="Signature Method">Signature Method</a>.
</td><td> Yes
</td></tr></tbody></table>

The format of common request parameters in API request links is shown below. Take Tencent Cloud CVM as an example, suppose you need to query the list of CVM instances, the request link of "Action=DescribeInstance" should be:

```
https://domain/v2/index.php?Action=DescribeInstances
&SecretId=xxxxxxx
&Region=gz
&Timestamp=1402992826
&Nonce=345122
&Signature=mysignature
&instanceId=101
```
`instanceId` is a command parameter, and others are common parameters.
