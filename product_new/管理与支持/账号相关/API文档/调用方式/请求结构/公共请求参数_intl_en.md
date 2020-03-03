Common request parameters are required in every API and will not be detailed in each API document unless necessary. **They are required in each request for the request to be initiated properly**. They always begin with an uppercase letter for distinction between API request parameters.

The following lists the specific common request parameters:

<table class="t">
<tbody><tr>
<th> <b>Name</b>
</th><th> <b>Type</b>
</th><th> <b>Description</b>
</th><th width="50"> <b>Required</b>
</th></tr>
<tr>
<td> Action
</td><td> String
</td><td> Name of the action-specific API. For example, if you want to call the <a href="https://intl.cloud.tencent.com/document/product/378/4400" title="DescribeProject">DescribeProject</a> API, then the `Action` parameter should be `DescribeProject`.
</td><td> Yes
</td></tr>
<tr>
<td> Region
</td><td> String
</td><td> Region parameter. Parameter value for each region: <br>Beijing: bj, Guangzhou: gz, Shanghai: sh, Hong Kong (China): hk, North America: ca.
</td><td> No
</td></tr>
<tr>
<td> Timestamp
</td><td> UInt
</td><td> Current UNIX timestamp which records the time when an API request is initiated.
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
</td><td> An ID that the user applies for on the <a href="https://console.cloud.tencent.com/capi">TencentCloud API Key</a> page. A `SecretId` is paired with a unique `SecretKey`, which is used to generate the request signature (`Signature`). 
</td><td> Yes
</td></tr>
<tr>
<td> Signature
</td><td> String
</td><td> Request signature, which is used to verify the validity of the request. It is generated automatically by the system based on the input parameters. 
</td><td> Yes
</td></tr></tbody></table>

Suppose you want to query the project list under the current account, a sample of the request would be as follows:

```
https://account.api.qcloud.com/v2/index.php?
Action=DescribeProject
&SecretId=xxxxxxx
&Timestamp=1465055529
&Nonce=59485
&Signature=mysignature
&<API request parameters>
```

A complete TencentCloud API request requires two types of parameters: common request parameters and API request parameters. 5 common request parameters are described above. For more information on API request parameters, please see <a href="/doc/api/372/接口请求参数" title="API Request Parameters">API Request Parameters</a>.
