| API        | 描述   | 
| --------   | -----  | 
|CreateDBInstanceHour	|创建云数据库实例（按量计费）|
|DescribeDBInstances	|查询实例列表|
|DescribeDBPrice	|查询数据库价格|
|DescribeDBZoneConfig	|获取云数据库可售卖规格|
|InitDBInstances	|初始化新实例|

### CreateDBInstanceHour 创建云数据库实例（按量计费）
```python
'''小时计费要冻结金额，需要账号有钱，如果账号余额为0，则不能购买'''
#!/usr/bin/python
# -*- coding: utf-8 -*-

# 引入云API入口模块
import logging
import traceback
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # 实例化一个认证对象，入参需要传入腾讯云账户secretId，secretKey
    cred = credential.Credential("secretId", "secretKey")

    #实例化要请求产品(以cdb为例)的client对象
    client = cdb_client.CdbClient(cred, "ap-beijing")

    #实例化一个请求对象:req = models.ModifyInstanceParamRequest()
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


    # 通过client对象调用想要访问的接口，需要传入请求对象
    resp = client.CreateDBInstanceHour(req)

    # 输出json格式的字符串回包
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    msg = traceback.format_exc() # 方式1  
    print (msg) 
```

### DescribeDBInstances	查询实例列表
```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

# 引入云API入口模块
import logging
import traceback
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # 实例化一个认证对象，入参需要传入腾讯云账户secretId，secretKey
    cred = credential.Credential("secretId", "secretKey")

    #实例化要请求产品(以cdb为例)的client对象
    client = cdb_client.CdbClient(cred, "ap-shanghai")

    #实例化一个请求对象:req = models.ModifyInstanceParamRequest()
    req = models.DescribeDBInstancesRequest()
    req.EngineVersions = ["5.6"]
    req.OrderBy = "instanceId"
    req.InstanceIds = ["cdb-1j8lumf6"]


    # 通过client对象调用想要访问的接口，需要传入请求对象
    resp = client.DescribeDBInstances(req)

    # 输出json格式的字符串回包
    print(resp.to_json_string())
except TencentCloudSDKException as err:
        msg = traceback.format_exc() # 方式1  
        print (msg) 
```



### DescribeDBPrice	查询数据库价格

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

# 引入云API入口模块
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # 实例化一个认证对象，入参需要传入腾讯云账户secretId，secretKey
    cred = credential.Credential("secretId", "secretKey")

    #实例化要请求产品(以cdb为例)的client对象
    client = cdb_client.CdbClient(cred, "ap-guangzhou")

    #实例化一个请求对象:req = models.ModifyInstanceParamRequest()
    req = models.DescribeDBPriceRequest()  
    req.Zone = "ap-guangzhou-3"
    req.GoodsNum = 1
    req.Memory =2000
    req.Volume =1000
    req.PayType = 'PRE_PAID'
    req.Period=1

    
    # 通过client对象调用想要访问的接口，需要传入请求对象
    resp = client.DescribeDBPrice(req)

    # 输出json格式的字符串回包
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
    
```

### DescribeDBZoneConfig 获取云数据库可售卖规格

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

# 引入云API入口模块

from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # 实例化一个认证对象，入参需要传入腾讯云账户secretId，secretKey
    cred = credential.Credential("secretId", "secretKey")

    #实例化要请求产品(以cdb为例)的client对象
    client = cdb_client.CdbClient(cred, "ap-shanghai")

    #实例化一个请求对象:req = models.ModifyInstanceParamRequest()
    req = models.DescribeDBZoneConfigRequest()
    #req.InstanceId = "cdb-j0edpju5"


    # 通过client对象调用想要访问的接口，需要传入请求对象
    resp = client.DescribeDBZoneConfig(req)

    # 输出json格式的字符串回包
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

### InitDBInstances 初始化新实例
```python

#!/usr/bin/python
# -*- coding: utf-8 -*-

# 引入云API入口模块

from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # 实例化一个认证对象，入参需要传入腾讯云账户secretId，secretKey
    cred = credential.Credential("secretId", "secretKey")

    #实例化要请求产品(以cdb为例)的client对象
    client = cdb_client.CdbClient(cred, "ap-shanghai")

    #实例化一个请求对象:req = models.ModifyInstanceParamRequest()
    req = models.InitDBInstancesRequest()
    req.InstanceIds = ["cdb-c752yqcn"]
    req.NewPassword = "CDB@Qcloud"
    
    req.Parameters = [{"name":"max_connections","value":"100"},{"name":"character_set_server","value":"utf8"},{"name":"lower_case_table_names","value":"1"}]


    # 通过client对象调用想要访问的接口，需要传入请求对象
    resp = client.InitDBInstances(req)

    # 输出json格式的字符串回包
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

