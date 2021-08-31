TencentCloud API authenticates each access request using the signature algorithm (Signature), so each request is required to include `Signature` for user authentication.

Before using a TencentCloud API for the first time, you need to apply for security credentials in the Tencent Cloud Console. The security credential consists of SecretId and SecretKey. SecretId is used to identify the API requester, while SecretKey is used to encrypt the strings to create a signature so that Tencent Cloud server can validate the identity of the requester. Keep your SecretKey private and avoid disclosure. If you already have the security credential, skip to the “Generating a Signature String” section.

## Applying for Security Credentials 
Before using a TencentCloud API for the first time, you need to apply for security credentials.
1. Log in to the [API Key Management](https://console.cloud.tencent.com/capi) console.
2. Click **Create Key** to create one SecretId/SecretKey pair. Each account can have at most two keys.

## Generating a Signature String
Suppose that the SecretId and SecretKey obtained from the last step are:
 - SecretId: AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA.
 - SecretKey: Gu5t9xGARNpq86cd98joQYCN3Cozk1qA.

To make a request for querying the list of CVM instances, the request parameters are:

| Parameter | Parameter Format | 
|---------|---------|
| Action | Action=DescribeInstances | 
| SecretId | SecretId= AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA | 
| Current timestamp | Timestamp=1408704141 | 
| Random positive integer | Nonce=345122 | 
| Region | Region=gz | 
| First CVM instance ID to query | instanceIds.0=qcvm12345 | 
| Second CVM instance to query | instanceIds.1=qcvm56789 | 

To generate an API signature, do as follows:
### Sorting parameters
Sort the request parameters in an ascending lexicographical order by their names (such as using the `ksort` function in PHP), and the result is as follows:

```
{
  'Action' : 'DescribeInstances',
  'Nonce' : 345122,
  'Region' : 'gz',
  'SecretId' : 'AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA',
  'Timestamp' : 1408704141
  'instanceIds.0' : 'qcvm12345',
  'instanceIds.1' : 'qcvm56789',
}
```

### Concatenating request strings
Format the above sorted request parameters as k=v, and then combine them with "&". Please note that v is the original value, instead of the URL-encoded value.

```
Action=DescribeInstances&Nonce=345122&Region=gz&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA&Timestamp=1408704141& instanceIds.0=qcvm12345&instanceIds.1=qcvm56789
```

### Concatenating original signature strings
The following parameters are required for constructing original signature strings:

- Request method: POST and GET methods are supported. The GET request method is used here.
- Request CVM: cvm.api.qcloud.com. Domain names vary depending on the module to which the API belongs. For more information, see the descriptions of each API.
- Request path: `/v2/index.php`.
- Request string: the string generated in the previous 2 steps.

Construct an original signature string in the format of:
Request method + request CVM + request path + ? + request string.

The resulting string in the example is:

```
GETcvm.api.qcloud.com/v2/index.php?Action=DescribeInstances&Nonce= 345122&Region=gz&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA&Timestamp=1408704141
```

### Generating a signature string
1. Sign the **original signature string** obtained in the previous step using the HMAC-SHA1 algorithm.
2. Encode the generated signature using Base64 to obtain the final signature string.

The sample code in PHP is as follows:

```
$secretKey = 'Gu5t9xGARNpq86cd98joQYCN3Cozk1qA';
$srcStr = 'GETcvm.api.qcloud.com/v2/index.php?Action=DescribeInstances&Nonce=345122&Region=gz&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA&Timestamp=1408704141';
$signStr = base64_encode(hash_hmac('sha1', $srcStr, $secretKey, true));
echo $signStr;
```

The signature string obtained is as follows:

```
HgIYOPcx5lN6gz8JsCFBNAWp2oQ=
```

You can use any other programming languages as long as the resulting signature is the same as the one in this example.

### Adding a signature and sending requests
- Add the `Signature` parameter, which is the **signature string** generated in the previous step, to the request parameter, and convert the signature to a URL-encoded one. The `HgIYOPcx5lN6gz8JsCFBNAWp2oQ=` signature generated above is encoded to `HgIYOPcx5lN6gz8JsCFBNAWp2oQ%3D`.

- If you use the GET request method, all the request parameter values must be URL-encoded. If you use the POST request method, URL encoding is only needed for Signature parameter.
  
- Send HTTPS protocol request to obtain the returned value of API in JSON string format.

The final request URL in the example is as follows:

```
https://cvm.api.qcloud.com/v2/index.php?Action=DescribeInstances
&Nonce=345122
&Region=gz
&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA
&Signature=HgIYOPcx5lN6gz8JsCFBNAWp2oQ%3D
&Timestamp=1408704141
&instanceIds.0=qcvm12345
&instanceIds.1=qcvm56789 
```

