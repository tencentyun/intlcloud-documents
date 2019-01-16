
## SDK Description
  ListAudits is used to fetch the CloudAudit list.
## Request Parameters
For more information, see [Common Request Parameters](https://cloud.tencent.com/document/product/599/12707).

## Response Parameters


| Parameter Name | Type | Description |
|---------|---------|---------|
| auditLists | Array | The list of tracking sets |

The parameter auditLists is composed of as follows:

| Parameter Name | Type | Description |
|---------|---------|---------|
| Name | String | CloudAudit name |
| bucketName | String | COS bucket name |
| prefix | String | Log prefix |
| status | Number | Audit status. 0: Disabled; 1: Enabled. |
| IsMultiRegionAudit | Number | Indicates whether to enable multi-region collection. 0: No; 1: Yes. |

## Example
### Request example

```
$config = array('SecretId'       => 'Your secretId',
                'SecretKey'      => 'Your secretKey',
                'RequestMethod'  => 'GET',
                'DefaultRegion'  => 'gz');
$ca = QcloudApi::load(QcloudApi::MODULE_CLOUDAUDIT, $config);
$package = array();
$a = $ca->ListAudits($package);
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
    "auditLists": [
        {
            "name": "ayisunxxx",
            "bucketName": "sundehuixxx",
            "prefix": "91000000009",
            "status": 1,
            "isMultiRegionAudit": 1
        }
    ]
}
```



