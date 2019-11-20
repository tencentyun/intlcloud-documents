
| API        | Description   | 
| :--------   | :-----  | 
|CreateBackup	| Creates a TencentDB instance backup |
|DeleteBackup	| Deletes a TencentDB instance backup |
|DescribeBackupConfig	| Queries the configuration information of a TencentDB instance backup |
|DescribeBackupDatabases	| Queries the list of backed up databases |
|DescribeBackupTables	| Queries backup data tables of the specified database |
|DescribeBackups	| Queries backup logs |
|DescribeBinlogs	| Queries binary logs |
|DescribeSlowLogs	| Queries slow logs |
|ModifyBackupConfig	| Modifies the database backup configuration |

### CreateBackup for Creating a TencentDB Instance Backup	

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
    req = models.CreateBackupRequest()
    req.InstanceId = "cdb-7ghaiocc"
    req.BackupMethod = "logical"

    print req
    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.CreateBackup(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### DeleteBackup for Deleting a TencentDB Instance Backup	

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
    req = models.DeleteBackupRequest()
    
    req.InstanceId = "cdb-7ghaiocc"
    #print  req.BackupId
    req.BackupId = 105119782

    
    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.DeleteBackup(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### DescribeBackupConfig for Querying the Configuration Information of a TencentDB Instance Backup	

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
    req = models.DescribeBackupConfigRequest()
    req.InstanceId = "cdb-7ghaiocc"

    print req
    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.DescribeBackupConfig(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### DescribeBackupDatabases for Querying the List of Backed up Databases	

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
    req = models.DescribeBackupDatabasesRequest()
    req.InstanceId = "cdb-7ghaiocc"
    req.StartTime = "2018-08-02 15:19:19"

    print req
    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.DescribeBackupDatabases(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    msg = traceback.format_exc() # Method 1  
    print (msg) 
```


### DescribeBackupTables for Querying Backup Data Tables of the Specified Database	

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
    req = models.DescribeBackupTablesRequest()
    req.InstanceId = "cdb-7ghaiocc"
    req.StartTime = "2018-08-02 15:19:19"
    req.DatabaseName ="sissi"


    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.DescribeBackupTables(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### DescribeBackups for Querying Backup Logs	

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
    req = models.DescribeBackupsRequest()
    req.InstanceId = "cdb-7ghaiocc"
     


    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.DescribeBackups(req)
    print resp

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### DescribeBinlogs for Querying Binary Logs	

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
    req = models.DescribeBinlogsRequest()
    req.InstanceId = "cdb-7ghaiocc"


    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.DescribeBinlogs(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
    
```


### DescribeSlowLogs for Querying Slow Logs	

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
    req = models.DescribeSlowLogsRequest()
    req.InstanceId = "cdb-7ghaiocc"


    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.DescribeSlowLogs(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
    
```


### ModifyBackupConfig for Modifying the Database Backup Configuration	

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
    req = models.ModifyBackupConfigRequest()
    req.InstanceId = "cdb-1y6g3zj8"
    req.ExpireDays = 10
    req.StartTime = "06:00-10:00"
    req.BackupMethod = "logical"
    print req


    # Call the API you want to access through the client object. You need to pass in the request object
    resp = client.ModifyBackupConfig(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```
