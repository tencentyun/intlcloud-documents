
| API        | 説明   | 
| --------   | -----  | 
|ModifyInstanceParam	|インスタンスパラメータを変更する|
|CloseWanService	|	インスタンスのインターネットアクセスを無効にする|
|OpenWanService	 | インスタンスのインターネットアクセスを有効にする|
|RestartDBInstances	|インスタンスを再起動する|
|OpenDBInstanceGTID	|インスタンスのGTIDを有効にする|
|ModifyDBInstanceName	|MySQLのインスタンス名を変更する|
|ModifyDBInstanceProject	|MySQLインスタンスの所属プロジェクトを変更する|
|ModifyDBInstanceVipVport	|MySQLインスタンスのIPとポート番号を変更する|
|DescribeDBInstanceCharset	|MySQLインスタンスの文字セットを問い合わせする|
|DescribeDBInstanceConfig	|MySQLインスタンスのコンフィグレーション情報を問い合わせする|
|DescribeDBInstanceGTID	|MySQLインスタンスのGTIDが有効になっているかを問い合わせする|
|DescribeDBInstanceRebootTime	|MySQLインスタンスの再起動予定時間を問い合わせする|

### ModifyInstanceParam インスタンスパラメータを変更する|

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

    #要求オブジェクトをインスタンス化します
    req = models.ModifyInstanceParamRequest()
    req.InstanceIds = ["cdb-1y6g3zj8","cdb-7ghaiocc"]
    req.ParamList = [{"name":"max_connections","currentValue":"100"},{"name":"character_set_server","currentValue":"utf8"},{"name":"lower_case_table_names","currentValue":"1"}]
    #req.ParamList = [{"name":"max_connections","currentValue":"100"}]
    #param = models.Parameter()
    #param.Name = "max_connections"
    #param.CurrentValue = "1000"
    #req.ParamList = [param]


    print req
    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.ModifyInstanceParam(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    msg = traceback.format_exc() # 方式1  
    print (msg) 

```

### CloseWanService	インスタンスのインターネットアクセスを無効にします

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
    req = models.CloseWanServiceRequest()
    req.InstanceId = "cdb-1y6g3zj8"

    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.CloseWanService(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

### OpenWanService インスタンスのインターネットアクセスを有効にします

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
    req = models.OpenWanServiceRequest()
    req.InstanceId = "cdb-1y6g3zj8"

    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.OpenWanService(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### RestartDBInstances	インスタンスを再起動します

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
    req = models.RestartDBInstancesRequest()
    req.InstanceIds = ["cdb-7ghaiocc"]

    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.RestartDBInstances(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### OpenDBInstanceGTID インスタンスのGTIDを有効にします

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
    req = models.OpenDBInstanceGTIDRequest()
    req.InstanceId = "cdb-7ghaiocc"
    

    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.OpenDBInstanceGTID(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

### ModifyDBInstanceName	MySQLのインスタンス名を変更します

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
    client = cdb_client.CdbClient(cred, "ap-beijing")

    #要求オブジェクト:req = models.ModifyInstanceParamRequest()をインスタンス化します
    req = models.ModifyDBInstanceNameRequest()
    req.InstanceId = "cdb-cukm86n2"
    req.InstanceName = "1s中国語"

    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.ModifyDBInstanceName(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### ModifyDBInstanceProject	MySQLインスタンスの所属プロジェクトを変更します

```python

#!/usr/bin/python
# -*- coding: utf-8 -*-

# クラウドAPIエントリモジュールの導入
import logging
import traceback
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models


def DescribeDBInstancesList():
    try:
        # 認証オブジェクトをインスタンス化します。引数としてTencent CloudのアカウントsecretId、secretKeyを渡す必要があります
        cred = credential.Credential("secretId", "secretKey")

        #製品（例：cdb）を要求するclientオブジェクトをインスタンス化します
        client = cdb_client.CdbClient(cred, "ap-shanghai")

        #要求オブジェクト:req = models.ModifyInstanceParamRequest()をインスタンス化します
        req = models.ModifyDBInstanceProjectRequest()
        req.InstanceIds = ["cdb-7ghaiocc"]
        req.NewProjectId =1


        # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
        resp = client.ModifyDBInstanceProject(req)

        # json形式の文字列をパッケージに出力します
        print(resp.to_json_string())
    except TencentCloudSDKException as err:
        msg = traceback.format_exc() # 方式1  
        print (msg) 



DescribeDBInstancesList()


```

### ModifyDBInstanceVipVport	MySQLインスタンスのIPとポート番号を変更します

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
    req = models.ModifyDBInstanceVipVportRequest()
    req.InstanceId = "cdb-7ghaiocc"
    req.DstIp = "10.0.0.13"
    req.DstPort =1025
    req.UniqVpcId = 1111

    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.ModifyDBInstanceVipVport(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
        msg = traceback.format_exc() # 方式1  
        print (msg) 

```


### DescribeDBInstanceCharset	MySQLインスタンスの文字セットを問い合わせします

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
    req = models.DescribeDBInstanceCharsetRequest()
    req.InstanceId = "cdb-1y6g3zj8"


    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.DescribeDBInstanceCharset(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

### DescribeDBInstanceConfig	MySQLインスタンスのコンフィグレーション情報を問い合わせします

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
    req = models.DescribeDBInstanceConfigRequest()
    req.InstanceId = "cdb-1y6g3zj8"


    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.DescribeDBInstanceConfig(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

### DescribeDBInstanceGTID	MySQLインスタンスのGTIDが有効になっているかを問い合わせします

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
    req = models.DescribeDBInstanceGTIDRequest()
    req.InstanceId = "cdb-1y6g3zj8"


    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.DescribeDBInstanceGTID(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
    
```

### DescribeDBInstanceRebootTime	MySQLインスタンスの再起動予定時間を問い合わせします

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
    req = models.DescribeDBInstanceRebootTimeRequest()
    req.InstanceIds = ["cdb-1y6g3zj8"]


    # clientオブジェクトを通じてアクセスするインターフェースを呼び出すには、要求オブジェクトを渡す必要があります
    resp = client.DescribeDBInstanceRebootTime(req)

    # json形式の文字列をパッケージに出力します
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```
