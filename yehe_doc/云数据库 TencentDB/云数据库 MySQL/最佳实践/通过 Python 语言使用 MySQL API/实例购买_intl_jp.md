| API        | 説明   | 
| --------   | -----  | 
|CreateDBInstanceHour	|MySQLインスタンス（従量課金）を作成する|
|DescribeDBInstances	|インスタンスリストを問い合わせする|
|DescribeDBPrice	|データベース価格を問い合わせする|
|DescribeDBZoneConfig	|MySQLの販売可能な規格を取得する|
|InitDBInstances	|新しいインスタンスを初期化する|

### CreateDBInstanceHour MySQLインスタンス（従量課金）を作成します
```python
'''時間課金の場合に金額を凍結するには、アカウントに残高がある必要があります。アカウント残高が0の場合は購入できません'''
#!/usr/bin/python
# -*- coding: utf-8 -*-

# クラウドAPIエントリモジュールの導入
import logging
import traceback
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # 認証オブジェクトをインスタンス化します。引数としてTencent CloudのアカウントsecretId、secretKeyを渡す必要があります
    cred = credential.Credential("secretId", "secretKey")

    #製品（例：cdb）を要求するclientオブジェクトをインスタンス化します
    client = cdb_client.CdbClient(cred, "ap-beijing")

    #要求オブジェクト:req = models.ModifyInstanceParamRequest()をインスタンス化します
    req = models.CreateDBInstanceHourRequest()
    req.EngineVersion = "5.6"
    req.Zone = "ap-beijing-3"
    req.ProjectId = 0
    req.GoodsNum = 1
    req.Memory = 1000
    req.Volume = 50
    req.InstanceRole = "master"
    req.Port =3311
    req.Password = "CDB@Qcloud"
    req.ParamList = [{"name":"max_connections","value":"1000"},{"name":"lower_case_table_names","value":"1"}]
    req.ProtectMode = 1
    req.SlaveZone = "ap-beijing-3"
    req.InstanceName = "oneday1"
    req.AutoRenewFlag = 0


    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.CreateDBInstanceHour(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    msg = traceback.format_exc() # 方式1  
    print (msg) 
```

### DescribeDBInstances	インスタンスリストを問い合わせします
```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

# クラウドAPIエントリモジュールの導入
import logging
import traceback
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # 認証オブジェクトをインスタンス化します。引数としてTencent CloudのアカウントsecretId、secretKeyを渡す必要があります
    cred = credential.Credential("secretId", "secretKey")

    #製品（例：cdb）を要求するclientオブジェクトをインスタンス化します
    client = cdb_client.CdbClient(cred, "ap-shanghai")

    #要求オブジェクト:req = models.ModifyInstanceParamRequest()をインスタンス化します
    req = models.DescribeDBInstancesRequest()
    req.EngineVersions = ["5.6"]
    req.OrderBy = "instanceId"
    req.InstanceIds = ["cdb-1j8lumf6"]


    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.DescribeDBInstances(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
        msg = traceback.format_exc() # 方式1  
        print (msg) 
```



### DescribeDBPrice	データベース価格を問い合わせします

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

# クラウドAPIエントリモジュールの導入
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # 認証オブジェクトをインスタンス化します。引数としてTencent CloudのアカウントsecretId、secretKeyを渡す必要があります
    cred = credential.Credential("secretId", "secretKey")

    #製品（例：cdb）を要求するclientオブジェクトをインスタンス化します
    client = cdb_client.CdbClient(cred, "ap-guangzhou")

    #要求オブジェクト:req = models.ModifyInstanceParamRequest()をインスタンス化します
    req = models.DescribeDBPriceRequest()  
    req.Zone = "ap-guangzhou-3"
    req.GoodsNum = 1
    req.Memory =2000
    req.Volume =1000
    req.PayType = 'PRE_PAID'
    req.Period=1

    
    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.DescribeDBPrice(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
    
```

### DescribeDBZoneConfig MySQLの販売可能な規格を取得します

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

# クラウドAPIエントリモジュールの導入

from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # 認証オブジェクトをインスタンス化します。引数としてTencent CloudのアカウントsecretId、secretKeyを渡す必要があります
    cred = credential.Credential("secretId", "secretKey")

    #製品（例：cdb）を要求するclientオブジェクトをインスタンス化します
    client = cdb_client.CdbClient(cred, "ap-shanghai")

    #要求オブジェクト:req = models.ModifyInstanceParamRequest()をインスタンス化します
    req = models.DescribeDBZoneConfigRequest()
    #req.InstanceId = "cdb-j0edpju5"


    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.DescribeDBZoneConfig(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

### InitDBInstances 新しいインスタンスを初期化します
```python

#!/usr/bin/python
# -*- coding: utf-8 -*-

# クラウドAPIエントリモジュールの導入

from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # 認証オブジェクトをインスタンス化します。引数としてTencent CloudのアカウントsecretId、secretKeyを渡す必要があります
    cred = credential.Credential("secretId", "secretKey")

    #製品（例：cdb）を要求するclientオブジェクトをインスタンス化します
    client = cdb_client.CdbClient(cred, "ap-shanghai")

    #要求オブジェクト:req = models.ModifyInstanceParamRequest()をインスタンス化します
    req = models.InitDBInstancesRequest()
    req.InstanceIds = ["cdb-c752yqcn"]
    req.NewPassword = "CDB@Qcloud"
    
    req.Parameters = [{"name":"max_connections","value":"100"},{"name":"character_set_server","value":"utf8"},{"name":"lower_case_table_names","value":"1"}]


    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.InitDBInstances(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

