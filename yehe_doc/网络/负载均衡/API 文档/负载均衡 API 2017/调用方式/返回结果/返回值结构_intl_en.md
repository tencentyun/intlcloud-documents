
<table class="t">
<tbody><tr>
<th> <b>Name</b>
</th><th> <b>Type</b>
</th><th> <b>Description</b>
</th></tr>
<tr>
<td> code
</td><td> Int
</td><td> Error code of the returned result. 0: success; other values: failure. For more information about the error code, see <a href="https://intl.cloud.tencent.com/document/product/214/11602" title="Error Codes">Error Codes</a>.
</td></tr>
<tr>
<td> message
</td><td> String
</td><td> Request results.
</td></tr></tbody></table>

Example:
Sample requests with common parameters:

```
 https://domain/v2/index.php?Action=DescribeInstances&SecretId=xxxxxxx&Region=gz
 &Timestamp=1402992826&Nonce=345122&Signature=mysignature&instanceId=101
```


Possible response:

```
{
    "code":0,
    "message": "success",
    "instanceSet":
   [{
        "instanceId":"qcvm1234",
        "cpu":1,
        "mem":2,
        "disk":20,
        "bandwidth":65535,
        "os":"centos_62_64",
        "lanIp":"10.207.248.186",
        "wanIp":null,
        "status":0
   }]
}
```

