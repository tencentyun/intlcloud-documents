
## SDK 描述
DeleteAudit 用于删除云审计（CloudAudit）。
## 请求参数


|参数名称|必选|类型|描述|
|---------|---------|---------|--------|
|Name|是|String|CloudAudit 名称|
## 响应参数
响应参数为空。

## 实际案例
### 请求示例

```
$config = array('SecretId'       => '您的secretId',
                'SecretKey'      => '您的secretKey',
                'RequestMethod'  => 'GET',
                'DefaultRegion'  => 'gz');
$ca = QcloudApi::load(QcloudApi::MODULE_CLOUDAUDIT, $config);
$package = array('Name'=>'ayisunxxx');
$a = $ca->DeleteAudit($package);
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
### 响应示例

```
[]
```
