
| API        | 説明   | 
| :--------   | :-----  | 
|CreateBackup	|MySQLのバックアップを作成する|
|DeleteBackup	|MySQLのバックアップを削除する|
|DescribeBackupConfig	|MySQLのバックアップのコンフィグレーション情報を問い合わせする|
|DescribeBackupDatabases	|バックアップデータベースリストを問い合わせする|
|DescribeBackupTables	|指定したデータベースのバックアップデータテーブルを問い合わせする|
|DescribeBackups	|バックアップログを問い合わせする|
|DescribeBinlogs	|バイナリーログを問い合わせする|
|DescribeSlowLogs	|スロークエリログを問い合わせする|
|ModifyBackupConfig	|データベースのバックアップ構成を変更する|

### CreateBackup	MySQLのバックアップを作成します

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
    req = models.CreateBackupRequest()
    req.InstanceId = "cdb-7ghaiocc"
    req.BackupMethod = "logical"

    print req
    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.CreateBackup(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### DeleteBackup	MySQLのバックアップを削除します

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
    req = models.DeleteBackupRequest()
    
    req.InstanceId = "cdb-7ghaiocc"
    #print  req.BackupId
    req.BackupId = 105119782

    
    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.DeleteBackup(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### DescribeBackupConfig	MySQLのバックアップのコンフィグレーション情報を問い合わせします

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
    req = models.DescribeBackupConfigRequest()
    req.InstanceId = "cdb-7ghaiocc"

    print req
    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.DescribeBackupConfig(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### DescribeBackupDatabases	バックアップデータベースリストを問い合わせします

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
    req = models.DescribeBackupDatabasesRequest()
    req.InstanceId = "cdb-7ghaiocc"
    req.StartTime = "2018-08-02 15:19:19"

    print req
    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.DescribeBackupDatabases(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    msg = traceback.format_exc() # 方式1  
    print (msg) 
```


### DescribeBackupTables	指定したデータベースのバックアップデータテーブルを問い合わせします

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
    req = models.DescribeBackupTablesRequest()
    req.InstanceId = "cdb-7ghaiocc"
    req.StartTime = "2018-08-02 15:19:19"
    req.DatabaseName ="sissi"


    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.DescribeBackupTables(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### DescribeBackups	バックアップログを問い合わせします

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
    req = models.DescribeBackupsRequest()
    req.InstanceId = "cdb-7ghaiocc"
     


    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.DescribeBackups(req)
    print resp

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### DescribeBinlogs	バイナリーログを問い合わせします

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
    req = models.DescribeBinlogsRequest()
    req.InstanceId = "cdb-7ghaiocc"


    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.DescribeBinlogs(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
    
```


### DescribeSlowLogs	スロークエリログを問い合わせします

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
    req = models.DescribeSlowLogsRequest()
    req.InstanceId = "cdb-7ghaiocc"


    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.DescribeSlowLogs(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
    
```


### ModifyBackupConfig	データベースのバックアップ構成を変更します

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
    req = models.ModifyBackupConfigRequest()
    req.InstanceId = "cdb-1y6g3zj8"
    req.ExpireDays = 10
    req.StartTime = "06:00-10:00"
    req.BackupMethod = "logical"
    print req


    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.ModifyBackupConfig(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```
