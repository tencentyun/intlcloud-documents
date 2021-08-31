
| API        | Description   |
| --------   | -----  |
|CreateDBInstance| Creates a TencentDB instance |
|CreateDBInstanceHour	| Creates a pay-as-you-go TencentDB instance |
|DescribeDBInstances	| Queries the list of instances |
|DescribeDBPrice| Queries the price of a TencentDB instance |
|DescribeDBZoneConfig| Queries the purchasable specifications of TencentDB instances |
|InitDBInstances	| Initializes new instances |

### CreateDBInstance for Creating a TencentDB Instance

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

# Introduce the TencentCloud API entry module
import logging
import traceback
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models


'''Purchase a source instance'''
def CreateDBInstancedemomaster():
    try:
        # Instantiate an authentication object. The Tencent Cloud account secretId and secretKey need to be passed in as the input parameters.
        cred = credential.Credential("secretId", "secretKey")

        # Instantiate the client object to request the product (with TencentDB as an example)
        client = cdb_client.CdbClient(cred, "ap-beijing")

        # Instantiate a request object: req = models.ModifyInstanceParamRequest()
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


        # To use the client object to call the API you want to access, you need to pass in the request object.
        resp = client.CreateDBInstance(req)
        # A string return packet in JSON format is outputted.
        print(resp.to_json_string())


    except TencentCloudSDKException as err:
        msg = traceback.format_exc() # Method 1  
        print (msg) 




'''Purchase a read-only instance'''
def CreateDBInstancedemoro():
    try:
        # Instantiate an authentication object. The Tencent Cloud account secretId and secretKey need to be passed in as the input parameters.
        cred = credential.Credential("secretId", "secretId")

        # Instantiate the client object to request the product (with TencentDB as an example)
        client = cdb_client.CdbClient(cred, "ap-beijing")

        # Instantiate a request object: req = models.ModifyInstanceParamRequest()
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


        # To use the client object to call the API you want to access, you need to pass in the request object.
        resp = client.CreateDBInstance(req)
        # A string return packet in JSON format is outputted.
        print(resp.to_json_string())


    except TencentCloudSDKException as err:
        msg = traceback.format_exc() # Method 1  
        print (msg) 


'''Purchase a disaster recovery instance'''
def CreateDBInstancedemodr():
    try:
        # Instantiate an authentication object. The Tencent Cloud account secretId and secretKey need to be passed in as the input parameters.
        cred = credential.Credential("secretId", "secretKey")

        # Instantiate the client object to request the product (with TencentDB as an example)
        client = cdb_client.CdbClient(cred, "ap-shanghai")

        # Instantiate a request object: req = models.ModifyInstanceParamRequest()
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


        # To use the client object to call the API you want to access, you need to pass in the request object.
        resp = client.CreateDBInstance(req)
        # A string return packet in JSON format is outputted.
        print(resp.to_json_string())


    except TencentCloudSDKException as err:
        msg = traceback.format_exc() # Method 1  
        print (msg) 

#CreateDBInstancedemodr()
#CreateDBInstancedemoro()
#CreateDBInstancedemomaster()

```


### CreateDBInstanceHour for Creating a Pay-as-You-Go TencentDB Instance
```python
'''Hourly billing requires freezing an amount in your account, so if your account balance is negative, no purchase can be made.'''
#!/usr/bin/python
# -*- coding: utf-8 -*-

# Introduce the TencentCloud API entry module
import logging
import traceback
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # Instantiate an authentication object. The Tencent Cloud account secretId and secretKey need to be passed in as the input parameters.
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


    # To use the client object to call the API you want to access, you need to pass in the request object.
    resp = client.CreateDBInstanceHour(req)

    # A string return packet in JSON format is outputted.
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    msg = traceback.format_exc() # Method 1  
    print (msg) 
```

### DescribeDBInstances for Querying the List of Instances	
```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

# Introduce the TencentCloud API entry module
import logging
import traceback
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # Instantiate an authentication object. The Tencent Cloud account secretId and secretKey need to be passed in as the input parameters.
    cred = credential.Credential("secretId", "secretKey")

    # Instantiate the client object to request the product (with TencentDB as an example)
    client = cdb_client.CdbClient(cred, "ap-shanghai")

    # Instantiate a request object: req = models.ModifyInstanceParamRequest()
    req = models.DescribeDBInstancesRequest()
    req.EngineVersions = ["5.6"]
    req.OrderBy = "instanceId"
    req.InstanceIds = ["cdb-1j8lumf6"]


    # To use the client object to call the API you want to access, you need to pass in the request object.
    resp = client.DescribeDBInstances(req)

    # A string return packet in JSON format is outputted.
    print(resp.to_json_string())
except TencentCloudSDKException as err:
        msg = traceback.format_exc() # Method 1  
        print (msg) 
```



### DescribeDBPrice for Querying the Price of a TencentDB Instance

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

# Introduce the TencentCloud API entry module
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # Instantiate an authentication object. The Tencent Cloud account secretId and secretKey need to be passed in as the input parameters.
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

    
    # To use the client object to call the API you want to access, you need to pass in the request object.
    resp = client.DescribeDBPrice(req)

    # A string return packet in JSON format is outputted.
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
    
```

### DescribeDBZoneConfig for Querying the Purchasable Specifications of TencentDB Instances

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

# Introduce the TencentCloud API entry module

from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # Instantiate an authentication object. The Tencent Cloud account secretId and secretKey need to be passed in as the input parameters.
    cred = credential.Credential("secretId", "secretKey")

    # Instantiate the client object to request the product (with TencentDB as an example)
    client = cdb_client.CdbClient(cred, "ap-shanghai")

    # Instantiate a request object: req = models.ModifyInstanceParamRequest()
    req = models.DescribeDBZoneConfigRequest()
    #req.InstanceId = "cdb-j0edpju5"


    # To use the client object to call the API you want to access, you need to pass in the request object.
    resp = client.DescribeDBZoneConfig(req)

    # A string return packet in JSON format is outputted.
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

### InitDBInstances for Initializing New Instances
```python

#!/usr/bin/python
# -*- coding: utf-8 -*-

# Introduce the TencentCloud API entry module

from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # Instantiate an authentication object. The Tencent Cloud account secretId and secretKey need to be passed in as the input parameters.
    cred = credential.Credential("secretId", "secretKey")

    # Instantiate the client object to request the product (with TencentDB as an example)
    client = cdb_client.CdbClient(cred, "ap-shanghai")

    # Instantiate a request object: req = models.ModifyInstanceParamRequest()
    req = models.InitDBInstancesRequest()
    req.InstanceIds = ["cdb-c752yqcn"]
    req.NewPassword = "CDB@Qcloud"
    
    req.Parameters = [{"name":"max_connections","value":"100"},{"name":"character_set_server","value":"utf8"},{"name":"lower_case_table_names","value":"1"}]


    # To use the client object to call the API you want to access, you need to pass in the request object.
    resp = client.InitDBInstances(req)

    # A string return packet in JSON format is outputted.
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

