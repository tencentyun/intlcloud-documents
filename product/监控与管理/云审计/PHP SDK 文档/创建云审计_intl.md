
## SDK Description
CreateAudit is used to create CloudAudits. A user can only create a maximum of 50 CloudAudits.
## Request Parameters


| Parameter Name | Required | Type | Description |
|---------|---------|---------|--------|
| IsMultiRegionAudit	| No |	Number	| Indicates whether to enable multi-region collection. 0: Disable; 1: Enable. |
| KmsKeyId	| No |	String	| The scretId of Kms, which is used to encrypt data. |
| Name | Yes | String | CloudAudit name, which has a length of 3-128 bytes. Only ASCII coded letters (`a-z, A-Z`), numbers (`0-9`) and underscore (`_`) are allowed. |
| CosBucketName	| Yes |	String	| The name of the COS Bucket to be delivered. Refer to the naming requirements for COS. |
| CosKeyPrefix | No | String | Prefix of COS bucket. For the naming convention, see COS documentation. |
| CmqTopicName	| No |	String	| CMQ topic name, which is required if CMQ is enabled. Refer to the naming requirements for CMQ. |



## Response Parameters


| Parameter Name | Type | Description |
|---------|---------|---------|
| IsMultiRegionAudit | Number | Indicates whether to enable multi-region collection. 1: Yes; 0: No. |
| KmsKeyId | String | ID of Kms key |
| Name | String | CloudAudit name |
| CosBucketName | String | COS bucket name |
| CosKeyPrefix | String | Prefix of COS bucket |
| CmqTopicName | String | CMQ topic name |

## Example
### Request example

```
$config = array('SecretId'       => 'Your secretId',
                'SecretKey'      => 'Your secretKey',
                'RequestMethod'  => 'GET',
                'DefaultRegion'  => 'gz');
$ca = QcloudApi::load(QcloudApi::MODULE_CLOUDAUDIT, $config);
$package = array('IsMultiRegionAudit ' => 1, 'Name' => 'ayisunxxx','CosBucketName'=>'sundehuixxx');
$a = $ca->CreateAudit($package);
if ($a === false) {
    $error = $ca->getError();
    echo "Error code:" . $error->getCode() . ".\n";
    echo "message:" . $error->getMessage() . ".\n";
    echo "ext:" . var_export($error->getExt(), true) . ".\n";
} else {
    var_dump($a);
}
echo "\nRequest :" . $ca->getLastRequest();
echo "\nResponse :" . $ca->getLastResponse();
echo "\n";
```
### Response example

```
{
    "IsMultiRegionAudit": "1",
    "KmsKeyId": "",
    "Name": "ayisunxxx",
    "CosBucketName": "sundehuixxx",
    "CosKeyPrefix": "91000000009",
    "CmqTopicName": ""
}
```


