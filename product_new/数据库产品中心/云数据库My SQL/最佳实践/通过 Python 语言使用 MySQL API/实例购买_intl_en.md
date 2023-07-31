| API        | Description   | 
| --------   | -----  | 
|CreateDBInstanceHour	| Creates a pay-as-you-go TencentDB instance |
|DescribeDBInstances	| Queries the list of instances |
|DescribeDBPrice	| Inquires the price of a TencentDB instance |
|DescribeDBZoneConfig	| Queries the specifications of purchasable TencentDB instances |
|InitDBInstances	| Initializes a new instance |


### CreateDBInstanceHour for Creating a Pay-as-you-go TencentDB Instance
```python
'''Hourly billing requires freezing an amount in your account, so If your account balance is 0, no purchase can be made'''
#!/usr/bin/python
# -*- coding: utf-8 -*-

# Import the TencentCloud API entry module
import logging
import traceback
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # Instantiate an authentication object. The Tencent Cloud account secretId and secretKey need to be passed in as the input parameters
    cred = credential.Credential("secretId", "secretKey")

    # Instantiate the client object to request the product (with TencentDB as an example)
    client = cdb_client.CdbClient(cred, "ap-beijing")

    # Instantiate a request object: req = models.ModifyInstanceParamRequest()
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


    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.CreateDBInstanceHour(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    msg = traceback.format_exc() # Method 1  
    print (msg) 
```

### DescribeDBInstances for Querying the List of Instances	
```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

# Import the TencentCloud API entry module
import logging
import traceback
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # Instantiate an authentication object. The Tencent Cloud account secretId and secretKey need to be passed in as the input parameters
    cred = credential.Credential("secretId", "secretKey")

    # Instantiate the client object to request the product (with TencentDB as an example)
    client = cdb_client.CdbClient(cred, "ap-shanghai")

    # Instantiate a request object: req = models.ModifyInstanceParamRequest()
    req = models.DescribeDBInstancesRequest()
    req.EngineVersions = ["5.6"]
    req.OrderBy = "instanceId"
    req.InstanceIds = ["cdb-1j8lumf6"]


    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.DescribeDBInstances(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
        msg = traceback.format_exc() # Method 1  
        print (msg) 
```



### DescribeDBPrice for Inquiring the Price of a TencentDB Instance	

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

# Import the TencentCloud API entry module
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # Instantiate an authentication object. The Tencent Cloud account secretId and secretKey need to be passed in as the input parameters
    cred = credential.Credential("secretId", "secretKey")

    # Instantiate the client object to request the product (with TencentDB as an example)
    client = cdb_client.CdbClient(cred, "ap-guangzhou")

    # Instantiate a request object: req = models.ModifyInstanceParamRequest()
    req = models.DescribeDBPriceRequest()  
    req.Zone = "ap-guangzhou-3"
    req.GoodsNum = 1
    req.Memory =2000
    req.Volume =1000
    req.PayType = 'PRE_PAID'
    req.Period=1

    
    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.DescribeDBPrice(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
    
```

### DescribeDBZoneConfig for Querying the Specifications of Purchasable TencentDB Instances

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

# Import the TencentCloud API entry module

from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # Instantiate an authentication object. The Tencent Cloud account secretId and secretKey need to be passed in as the input parameters
    cred = credential.Credential("secretId", "secretKey")

    # Instantiate the client object to request the product (with TencentDB as an example)
    client = cdb_client.CdbClient(cred, "ap-shanghai")

    # Instantiate a request object: req = models.ModifyInstanceParamRequest()
    req = models.DescribeDBZoneConfigRequest()
    #req.InstanceId = "cdb-j0edpju5"


    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.DescribeDBZoneConfig(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

### InitDBInstances for Initializing a New Instance
```python

#!/usr/bin/python
# -*- coding: utf-8 -*-

# Import the TencentCloud API entry module

from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # Instantiate an authentication object. The Tencent Cloud account secretId and secretKey need to be passed in as the input parameters
    cred = credential.Credential("secretId", "secretKey")

    # Instantiate the client object to request the product (with TencentDB as an example)
    client = cdb_client.CdbClient(cred, "ap-shanghai")

    # Instantiate a request object: req = models.ModifyInstanceParamRequest()
    req = models.InitDBInstancesRequest()
    req.InstanceIds = ["cdb-c752yqcn"]
    req.NewPassword = "CDB@Qcloud"
    
    req.Parameters = [{"name":"max_connections","value":"100"},{"name":"character_set_server","value":"utf8"},{"name":"lower_case_table_names","value":"1"}]


    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.InitDBInstances(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

