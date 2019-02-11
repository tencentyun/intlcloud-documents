
## SDK Description
 ListCosBuckets is used to fetch the bucket list of COS.
## Request Parameters
For more information, see [Common Request Parameters](https://cloud.tencent.com/document/product/599/12707).

## Response Parameters


| Parameter Name | Type | Description |
|---------|---------|---------|
| cosBucketsList | Array | COS bucket list |

The parameter cosBucketsList is composed as follows:

| Parameter Name | Type | Description |
|---------|---------|---------|
| name | String | COS bucket name |
| region | String | The region of the bucket |
| appId | String | Account APPID or project APPID |
## Example
### Request example

```
$config = array('SecretId'       => 'Your secretId',
                'SecretKey'      => 'Your secretKey',
                'RequestMethod'  => 'GET',
                'DefaultRegion'  => 'gz');
$ca = QcloudApi::load(QcloudApi::MODULE_CLOUDAUDIT, $config);
$package = array();
$a = $ca->ListCosBuckets($package);
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
    "cosBucketsList": [
        {
            "name": "cloudaudit",
            "region": "ap-shanghai",
            "appId": "1254962721"
        },
        {
            "name": "cloudtrail",
            "region": "ap-shanghai",
            "appId": "1254962721"
        },
        {
            "name": "sundehuixxx",
            "region": "ap-shanghai",
            "appId": "1254962721"
        }
    ]
}
```



