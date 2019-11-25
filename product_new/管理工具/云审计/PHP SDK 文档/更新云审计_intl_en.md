
## SDK Description
The UpdateAudit API is used to update CloudAudit. It can update certain settings for the specified log file, such as the path and COS bucket. The name of CloudAudit cannot be modified. You do not need to disable the CloudAudit service when modifying the path. If the COS bucket to be modified was a target of the CloudAudit log file, it can be modified successfully; otherwise, you need to manually grant CloudAudit write permission to the COS bucket.



## Request Parameters


| Parameter Name | Required | Type | Description |
|---------|---------|---------|--------|
| IsMultiRegionAudit	| No |	Number	| Indicates whether to enable multi-region collection. 0: disable; 1: enable. |
| KmsKeyId| No |String| The secretId of KMS, which is used to encrypt data. |
| Name	| Yes |	String	| CloudAudit name, which can contain 3-128 ASCII letters (`a-z`; `A-Z`), digits (`0-9`), and underscores (`_`).
| CosBucketName| Yes |String| The name of the receiving COS bucket. For naming convention, see the naming requirements of COS. |
| CosKeyPrefix| No |String| COS bucket Prefix. For naming convention, see the naming requirements of COS. |
| CmqTopicName| No |String| CMQ topic name, which is required if CMQ is enabled. For naming convention, see the naming requirements of CMQ. |


## Response Parameters
The response parameter is null.


## Use Cases
### Sample request

```
$config = array('SecretId'       => 'Your secretId',
                'SecretKey'      => 'Your secretKey',
                'RequestMethod'  => 'GET',
                'DefaultRegion'  => 'gz');
$ca = QcloudApi::load(QcloudApi::MODULE_CLOUDAUDIT, $config);
$package = array('Name'=>'ayisunxxx','CosBucketName'=>'sundehuixxx','CosKeyPrefix'=>'sundehui');
$a = $ca->UpdateAudit($package);
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
### Sample response

```
[]
```

