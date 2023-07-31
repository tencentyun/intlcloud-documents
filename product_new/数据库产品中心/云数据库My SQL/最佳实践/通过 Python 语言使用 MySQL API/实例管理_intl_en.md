
| API        | Description   | 
| --------   | -----  | 
|ModifyInstanceParam	| Modifies instance parameters |
|CloseWanService	|	 Disables public network access for an instance |
|OpenWanService	 | Enables public network access for an instance |
|RestartDBInstances| Restarts an instance |
|OpenDBInstanceGTID| Enables GTID for an instance |
|ModifyDBInstanceName	| Renames a TencentDB instance |
|ModifyDBInstanceProject	| Modifies the project to which a TencentDB instance belongs |
|ModifyDBInstanceVipVport	| Modifies the IP and port number of a TencentDB instance |
|DescribeDBInstanceCharset	| Queries the character set of a TencentDB instance |
|DescribeDBInstanceConfig	| Queries the configuration information of a TencentDB instance |
|DescribeDBInstanceGTID	| Queries whether GTID is enabled for a TencentDB instance |
|DescribeDBInstanceRebootTime	| Queries the estimated restart time of a TencentDB instance |

### ModifyInstanceParam for Modifying Instance Parameters

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

    # Instantiate a request object
    req = models.ModifyInstanceParamRequest()
    req.InstanceIds = ["cdb-1y6g3zj8","cdb-7ghaiocc"]
    req.ParamList = [{"name":"max_connections","currentValue":"100"},{"name":"character_set_server","currentValue":"utf8"},{"name":"lower_case_table_names","currentValue":"1"}]
    #req.ParamList = [{"name":"max_connections","currentValue":"100"}]
    #param = models.Parameter()
    #param.Name = "max_connections"
    #param.CurrentValue = "1000"
    #req.ParamList = [param]


    print req
    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.ModifyInstanceParam(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    msg = traceback.format_exc() # Method 1  
    print (msg) 

```

### CloseWanService for Disabling Public Network Access for an Instance	

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
    req = models.CloseWanServiceRequest()
    req.InstanceId = "cdb-1y6g3zj8"

    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.CloseWanService(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

### OpenWanService for Enabling Public Network Access for an Instance

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
    req = models.OpenWanServiceRequest()
    req.InstanceId = "cdb-1y6g3zj8"

    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.OpenWanService(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### RestartDBInstances for Restarting an Instance	

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
    req = models.RestartDBInstancesRequest()
    req.InstanceIds = ["cdb-7ghaiocc"]

    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.RestartDBInstances(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### OpenDBInstanceGTID for Enabling GTID for an Instance

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
    req = models.OpenDBInstanceGTIDRequest()
    req.InstanceId = "cdb-7ghaiocc"
    

    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.OpenDBInstanceGTID(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

### ModifyDBInstanceName for Renaming a TencentDB Instance	

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
    client = cdb_client.CdbClient(cred, "ap-beijing")

    # Instantiate a request object: req = models.ModifyInstanceParamRequest()
    req = models.ModifyDBInstanceNameRequest()
    req.InstanceId = "cdb-cukm86n2"
    req.InstanceName = "1s Chinese"

    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.ModifyDBInstanceName(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### ModifyDBInstanceProject for Modifying the Project to Which a TencentDB Instance Belongs	

```python

#!/usr/bin/python
# -*- coding: utf-8 -*-

# Import the TencentCloud API entry module
import logging
import traceback
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models


def DescribeDBInstancesList():
    try:
        # Instantiate an authentication object. The Tencent Cloud account secretId and secretKey need to be passed in as the input parameters
        cred = credential.Credential("secretId", "secretKey")

        # Instantiate the client object to request the product (with TencentDB as an example)
        client = cdb_client.CdbClient(cred, "ap-shanghai")

        # Instantiate a request object: req = models.ModifyInstanceParamRequest()
        req = models.ModifyDBInstanceProjectRequest()
        req.InstanceIds = ["cdb-7ghaiocc"]
        req.NewProjectId =1


        # Call the API you want to access through the client object. You need to pass in the request object
        resp = client.ModifyDBInstanceProject(req)

        # A string return packet in JSON format is outputted
        print(resp.to_json_string())
    except TencentCloudSDKException as err:
        msg = traceback.format_exc() # Method 1  
        print (msg) 



DescribeDBInstancesList()


```

### ModifyDBInstanceVipVport for Modifying the IP and Port Number of a TencentDB Instance	

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
    req = models.ModifyDBInstanceVipVportRequest()
    req.InstanceId = "cdb-7ghaiocc"
    req.DstIp = "10.0.0.13"
    req.DstPort =1025
    req.UniqVpcId = 1111

    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.ModifyDBInstanceVipVport(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
        msg = traceback.format_exc() # Method 1  
        print (msg) 

```


### DescribeDBInstanceCharset for Querying the Character Set of a TencentDB Instance	

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
    req = models.DescribeDBInstanceCharsetRequest()
    req.InstanceId = "cdb-1y6g3zj8"


    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.DescribeDBInstanceCharset(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

### DescribeDBInstanceConfig for Querying the Configuration Information of a TencentDB Instance	

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
    req = models.DescribeDBInstanceConfigRequest()
    req.InstanceId = "cdb-1y6g3zj8"


    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.DescribeDBInstanceConfig(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

### DescribeDBInstanceGTID for Querying Whether GTID Is Activated for a TencentDB Instance	

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
    req = models.DescribeDBInstanceGTIDRequest()
    req.InstanceId = "cdb-1y6g3zj8"


    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.DescribeDBInstanceGTID(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
    
```

### DescribeDBInstanceRebootTime for Querying the Estimated Restart Time of a TencentDB Instance	

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
    req = models.DescribeDBInstanceRebootTimeRequest()
    req.InstanceIds = ["cdb-1y6g3zj8"]


    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.DescribeDBInstanceRebootTime(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```
