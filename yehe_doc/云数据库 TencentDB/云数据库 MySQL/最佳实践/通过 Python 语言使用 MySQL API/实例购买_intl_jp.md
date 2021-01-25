
| API        | 説明   |
| --------   | -----  |
|CreateDBInstance| TencentDBインスタンスを作成します|
|CreateDBInstanceHour| TencentDBインスタンス（従量課金）を作成します|
|DescribeDBInstances|インスタンスリストのクエリーを行います|
|DescribeDBPrice|データベース料金のクエリーを行います|
|DescribeDBZoneConfig| TencentDBの販売可能な仕様を取得します|
|InitDBInstances|新規インスタンスを初期化します|

### CreateDBInstance TencentDBインスタンスを作成します

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

# TencentCloud APIのエントリーコンポーネントをインポートします
import logging
import traceback
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models


'''マスターインスタンスの購入'''
def CreateDBInstancedemomaster():
    try:
        # 認証オブジェクトをインスタンス化します。パラメータ入力には、Tencent CloudアカウントのsecretIdとsecretKeyが必要です
        cred = credential.Credential("secretId", "secretKey")

        #製品（例はcdb）をリクエストするclientオブジェクトをインスタンス化します
        client = cdb_client.CdbClient(cred, "ap-beijing")

        #リクエストオブジェクトをインスタンス化します:req = models.ModifyInstanceParamRequest()
        req = models.CreateDBInstanceRequest()
        req.Memory = 2000
        req.Volume = 120
        req.Period = 1
        req.GoodsNum =1
        req.Zone = "ap-beijing-1"
        req.Port = 3306
        #req.MasterInstanceId = "cdb-7ghaiocc"
        req.InstanceRole = "master"
        req.EngineVersion = "5.6"
        req.Password = "CDB@Qcloud"
        req.ProtectMode = 0
        req.InstanceName = "tencentcdb"
        req.SecurityGroup = ["sg-eq0hvlzp"]


        # clientオブジェクトでアクセスするインターフェースを呼び出すには、リクエストオブジェクトを渡す必要があります。
        resp = client.CreateDBInstance(req)
        # json形式の文字列をパッケージに出力します
        print(resp.to_json_string())


    except TencentCloudSDKException as err:
        msg = traceback.format_exc() # メソッド1  
        print (msg) 




'''読み取り専用インスタンスの購入'''
def CreateDBInstancedemoro():
    try:
        # 認証オブジェクトをインスタンス化します。パラメータ入力には、Tencent CloudアカウントのsecretIdとsecretKeyが必要です
        cred = credential.Credential("secretId", "secretId")

        #製品（例はcdb）をリクエストするclientオブジェクトをインスタンス化します
        client = cdb_client.CdbClient(cred, "ap-beijing")

        #リクエストオブジェクトをインスタンス化します:req = models.ModifyInstanceParamRequest()
        req = models.CreateDBInstanceRequest()
        req.Memory = 2000
        req.Volume = 200
        req.Period = 1
        req.GoodsNum =1
        req.Zone = "ap-beijing-1"
        req.Port = 3306
        req.InstanceRole = "ro"
        req.EngineVersion = "5.6"
        req.Password = "CDB@Qcloud"
        req.ProtectMode = 0
        req.DeployMode =1
        req.GoodsNum =2
        req.SlaveZone = "ap-beijing-1"
        req.ParamList = [{"name":"max_connections","value":"1000"},{"name":"lower_case_table_names","value":"1"}]
        req.BackupZone = "0"
        req.AutoRenewFlag =0
        req.MasterInstanceId ="cdb-bgr97hu0"
        req.RoGroup = {"RoGroupMode":"allinone","RoGroupName":"roweek"}
        req.InstanceName = "tencentcdbRO"


        # clientオブジェクトでアクセスするインターフェースを呼び出すには、リクエストオブジェクトを渡す必要があります。
        resp = client.CreateDBInstance(req)
        # json形式の文字列をパッケージに出力します
        print(resp.to_json_string())


    except TencentCloudSDKException as err:
        msg = traceback.format_exc() # メソッド1  
        print (msg) 


'''ディザスタリカバリインスタンスの購入'''
def CreateDBInstancedemodr():
    try:
        # 認証オブジェクトをインスタンス化します。パラメータ入力には、Tencent CloudアカウントのsecretIdとsecretKeyが必要です
        cred = credential.Credential("secretId", "secretKey")

        #製品（例はcdb）をリクエストするclientオブジェクトをインスタンス化します
        client = cdb_client.CdbClient(cred, "ap-shanghai")

        #リクエストオブジェクトをインスタンス化します:req = models.ModifyInstanceParamRequest()
        req = models.CreateDBInstanceRequest()
        
        req.Memory = 4000
        req.Volume = 200
        req.Period = 1
        req.GoodsNum =1
        #req.Zone = "ap-shanghai-2"
        req.Port = 3306
        req.InstanceRole = "dr"
        #req.MasterInstanceId
        req.EngineVersion = "5.6"
        req.Password = "CDB@Qcloud"
        req.ProtectMode = 0
        req.DeployMode =0
        #req.SlaveZone = "ap-guangzhou-3"
        req.ParamList = [{"name":"max_connections","value":"1000"},{"name":"lower_case_table_names","value":"1"}]
        req.BackupZone = "0"
        req.AutoRenewFlag =0
        #req.RoGroup = {"RoGroupMode":"alone","RoGroupName":"roweek"}
        #req.RoGroup = {"RoGroupName":"roweek"}
        #param = models.RoGroup()
        #param.RoGroupMode = "alone"
        #param.RoGroupName = "roweek"
        #param.MinRoInGroup = 1
        #req.RoGroup = [param]
        

        #ro = [{"roGroupMode":"allinone"},{"RoGroupName":"ro_www"}]
        #req.RoGroup = [ro]
        req.MasterInstanceId ="cdb-bgr97hu0"
        req.MasterRegion = "ap-beijing"
        #roGroup = [RoGroupMode="allinone", RoGroupName="weekro",RoOfflineDelay=1,MinRoInGroup=5,MinRoInGroup=1]
        #req.RoGroup = [roGroup]
        req.InstanceName = "tencentcdbDR"


        # clientオブジェクトでアクセスするインターフェースを呼び出すには、リクエストオブジェクトを渡す必要があります。
        resp = client.CreateDBInstance(req)
        # json形式の文字列をパッケージに出力します
        print(resp.to_json_string())


    except TencentCloudSDKException as err:
        msg = traceback.format_exc() # メソッド1  
        print (msg) 

#CreateDBInstancedemodr()
#CreateDBInstancedemoro()
#CreateDBInstancedemomaster()

```


### CreateDBInstanceHour TencentDBインスタンス（従量課金）を作成します
```python
'''1時間単位の課金の場合、凍結された金額が必要で、アカウントに残額が必要です。アカウント残額が0の場合は購入できません'''
#!/usr/bin/python
# -*- coding: utf-8 -*-

# TencentCloud APIのエントリーコンポーネントをインポートします
import logging
import traceback
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # 認証オブジェクトをインスタンス化します。パラメータ入力には、Tencent CloudアカウントのsecretIdとsecretKeyが必要です
    cred = credential.Credential("secretId", "secretKey")

    #製品（例はcdb）をリクエストするclientオブジェクトをインスタンス化します
    client = cdb_client.CdbClient(cred, "ap-beijing")

    #リクエストオブジェクトをインスタンス化します:req = models.ModifyInstanceParamRequest()
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


    # clientオブジェクトでアクセスするインターフェースを呼び出すには、リクエストオブジェクトを渡す必要があります。
    resp = client.CreateDBInstanceHour(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    msg = traceback.format_exc() # メソッド1  
    print (msg) 
```

### DescribeDBInstancesインスタンスリストのクエリーを行います
```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

# TencentCloud APIのエントリーコンポーネントをインポートします
import logging
import traceback
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # 認証オブジェクトをインスタンス化します。パラメータ入力には、Tencent CloudアカウントのsecretIdとsecretKeyが必要です
    cred = credential.Credential("secretId", "secretKey")

    #製品（例はcdb）をリクエストするclientオブジェクトをインスタンス化します
    client = cdb_client.CdbClient(cred, "ap-shanghai")

    #リクエストオブジェクトをインスタンス化します:req = models.ModifyInstanceParamRequest()
    req = models.DescribeDBInstancesRequest()
    req.EngineVersions = ["5.6"]
    req.OrderBy = "instanceId"
    req.InstanceIds = ["cdb-1j8lumf6"]


    # clientオブジェクトでアクセスするインターフェースを呼び出すには、リクエストオブジェクトを渡す必要があります。
    resp = client.DescribeDBInstances(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
        msg = traceback.format_exc() # メソッド1  
        print (msg) 
```



### DescribeDBPrice データベースの価格のクエリーを行います

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

# TencentCloud APIのエントリーコンポーネントをインポートします
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # 認証オブジェクトをインスタンス化します。パラメータ入力には、Tencent CloudアカウントのsecretIdとsecretKeyが必要です
    cred = credential.Credential("secretId", "secretKey")

    #製品（例はcdb）をリクエストするclientオブジェクトをインスタンス化します
    client = cdb_client.CdbClient(cred, "ap-guangzhou")

    #リクエストオブジェクトをインスタンス化します:req = models.ModifyInstanceParamRequest()
    req = models.DescribeDBPriceRequest()  
    req.Zone = "ap-guangzhou-3"
    req.GoodsNum = 1
    req.Memory =2000
    req.Volume =1000
    req.PayType = 'PRE_PAID'
    req.Period=1

    
    # clientオブジェクトでアクセスするインターフェースを呼び出すには、リクエストオブジェクトを渡す必要があります。
    resp = client.DescribeDBPrice(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
    
```

### DescribeDBZoneConfig TencentDBの販売可能な仕様を取得します

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

# TencentCloud APIのエントリーコンポーネントをインポートします

from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # 認証オブジェクトをインスタンス化します。パラメータ入力には、Tencent CloudアカウントのsecretIdとsecretKeyが必要です
    cred = credential.Credential("secretId", "secretKey")

    #製品（例はcdb）をリクエストするclientオブジェクトをインスタンス化します
    client = cdb_client.CdbClient(cred, "ap-shanghai")

    #リクエストオブジェクトをインスタンス化します:req = models.ModifyInstanceParamRequest()
    req = models.DescribeDBZoneConfigRequest()
    #req.InstanceId = "cdb-j0edpju5"


    # clientオブジェクトでアクセスするインターフェースを呼び出すには、リクエストオブジェクトを渡す必要があります。
    resp = client.DescribeDBZoneConfig(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

### InitDBInstances 新規インスタンスを初期化します
```python

#!/usr/bin/python
# -*- coding: utf-8 -*-

# TencentCloud APIのエントリーコンポーネントをインポートします

from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # 認証オブジェクトをインスタンス化します。パラメータ入力には、Tencent CloudアカウントのsecretIdとsecretKeyが必要です
    cred = credential.Credential("secretId", "secretKey")

    #製品（例はcdb）をリクエストするclientオブジェクトをインスタンス化します
    client = cdb_client.CdbClient(cred, "ap-shanghai")

    #リクエストオブジェクトをインスタンス化します:req = models.ModifyInstanceParamRequest()
    req = models.InitDBInstancesRequest()
    req.InstanceIds = ["cdb-c752yqcn"]
    req.NewPassword = "CDB@Qcloud"
    
    req.Parameters = [{"name":"max_connections","value":"100"},{"name":"character_set_server","value":"utf8"},{"name":"lower_case_table_names","value":"1"}]


    # clientオブジェクトでアクセスするインターフェースを呼び出すには、リクエストオブジェクトを渡す必要があります。
    resp = client.InitDBInstances(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

