
| API        | 설명   |
| --------   | -----  |
|CreateDBInstance	|CDB 인스턴스 생성|
|CreateDBInstanceHour	|CDB 인스턴스 생성(종량제)|
|DescribeDBInstances	|인스턴스 리스트 조회|
|DescribeDBPrice	|데이터베이스 가격 조회|
|DescribeDBZoneConfig	|CDB 판매 규격 획득|
|InitDBInstances	|신규 인스턴스 초기화|

### CreateDBInstance CDB 인스턴스 생성

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

# 클라우드 API 게이트 모듈 불러오기
import logging
import traceback
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models


'''마스터 인스턴스 구매''’
def CreateDBInstancedemomaster():
    try:
        # 1개의 인증 객체를 인스턴스화, 매개변수 입력 시 Tencent Cloud 계정 secretId, secretKey에 전송 필요
        cred = credential.Credential("secretId", "secretKey")

        #인스턴스화 시 제품(예: cdb)의 client 객체 요청 필요
        client = cdb_client.CdbClient(cred, "ap-beijing")

        #요청 객체 인스턴스화:req = models.ModifyInstanceParamRequest()
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


        # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
        resp = client.CreateDBInstance(req)
        # json 포맷의 문자열 출력
        print(resp.to_json_string())


    except TencentCloudSDKException as err:
        msg = traceback.format_exc() # 방식1  
        print (msg) 




'''읽기 전용 인스턴스 구매''’
def CreateDBInstancedemoro():
    try:
        # 1개의 인증 객체를 인스턴스화, 매개변수 입력 시 Tencent Cloud 계정 secretId, secretKey에 전송 필요
        cred = credential.Credential("secretId", "secretId")

        #인스턴스화 시 제품(예: cdb)의 client 객체 요청 필요
        client = cdb_client.CdbClient(cred, "ap-beijing")

        #요청 객체 인스턴스화:req = models.ModifyInstanceParamRequest()
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


        # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
        resp = client.CreateDBInstance(req)
        # json 포맷의 문자열 출력
        print(resp.to_json_string())


    except TencentCloudSDKException as err:
        msg = traceback.format_exc() # 방식1  
        print (msg) 


'''재해 복구 인스턴스 구매''’
def CreateDBInstancedemodr():
    try:
        # 1개의 인증 객체를 인스턴스화, 매개변수 입력 시 Tencent Cloud 계정 secretId, secretKey에 전송 필요
        cred = credential.Credential("secretId", "secretKey")

        #인스턴스화 시 제품(예: cdb)의 client 객체 요청 필요
        client = cdb_client.CdbClient(cred, "ap-shanghai")

        #요청 객체 인스턴스화:req = models.ModifyInstanceParamRequest()
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


        # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
        resp = client.CreateDBInstance(req)
        # json 포맷의 문자열 출력
        print(resp.to_json_string())


    except TencentCloudSDKException as err:
        msg = traceback.format_exc() # 방식1  
        print (msg) 

#CreateDBInstancedemodr()
#CreateDBInstancedemoro()
#CreateDBInstancedemomaster()

```


### CreateDBInstanceHour CDB 인스턴스 생성(종량제)
```python
'''시간당 과금의 경우 동결 예치금이 필요하며 계정에 금액이 예치되어 있어야 함. 계정 잔액이 0인 경우 구매 불가''’
#!/usr/bin/python
# -*- coding: utf-8 -*-

# 클라우드 API 게이트 모듈 불러오기
import logging
import traceback
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # 1개의 인증 객체를 인스턴스화, 매개변수 입력 시 Tencent Cloud 계정 secretId, secretKey에 전송 필요
    cred = credential.Credential("secretId", "secretKey")

    #인스턴스화 시 제품(예: cdb)의 client 객체 요청 필요
    client = cdb_client.CdbClient(cred, "ap-beijing")

    #요청 객체 인스턴스화:req = models.ModifyInstanceParamRequest()
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


    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.CreateDBInstanceHour(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    msg = traceback.format_exc() # 방식1  
    print (msg) 
```

### DescribeDBInstances	인스턴스 리스트 조회
```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

# 클라우드 API 게이트 모듈 불러오기
import logging
import traceback
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # 1개의 인증 객체를 인스턴스화, 매개변수 입력 시 Tencent Cloud 계정 secretId, secretKey에 전송 필요
    cred = credential.Credential("secretId", "secretKey")

    #인스턴스화 시 제품(예: cdb)의 client 객체 요청 필요
    client = cdb_client.CdbClient(cred, "ap-shanghai")

    #요청 객체 인스턴스화:req = models.ModifyInstanceParamRequest()
    req = models.DescribeDBInstancesRequest()
    req.EngineVersions = ["5.6"]
    req.OrderBy = "instanceId"
    req.InstanceIds = ["cdb-1j8lumf6"]


    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.DescribeDBInstances(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
        msg = traceback.format_exc() # 방식1  
        print (msg) 
```



### DescribeDBPrice	데이터베이스 가격 조회

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

# 클라우드 API 게이트 모듈 불러오기
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # 1개의 인증 객체를 인스턴스화, 매개변수 입력 시 Tencent Cloud 계정 secretId, secretKey에 전송 필요
    cred = credential.Credential("secretId", "secretKey")

    #인스턴스화 시 제품(예: cdb)의 client 객체 요청 필요
    client = cdb_client.CdbClient(cred, "ap-guangzhou")

    #요청 객체 인스턴스화:req = models.ModifyInstanceParamRequest()
    req = models.DescribeDBPriceRequest()  
    req.Zone = "ap-guangzhou-3"
    req.GoodsNum = 1
    req.Memory =2000
    req.Volume =1000
    req.PayType = 'PRE_PAID'
    req.Period=1

    
    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.DescribeDBPrice(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
    
```

### DescribeDBZoneConfig CDB 판매 규격 획득

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

# 클라우드 API 게이트 모듈 불러오기

from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # 1개의 인증 객체를 인스턴스화, 매개변수 입력 시 Tencent Cloud 계정 secretId, secretKey에 전송 필요
    cred = credential.Credential("secretId", "secretKey")

    #인스턴스화 시 제품(예: cdb)의 client 객체 요청 필요
    client = cdb_client.CdbClient(cred, "ap-shanghai")

    #요청 객체 인스턴스화:req = models.ModifyInstanceParamRequest()
    req = models.DescribeDBZoneConfigRequest()
    #req.InstanceId = "cdb-j0edpju5"


    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.DescribeDBZoneConfig(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

### InitDBInstances 신규 인스턴스 초기화
```python

#!/usr/bin/python
# -*- coding: utf-8 -*-

# 클라우드 API 게이트 모듈 불러오기

from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models

try:
    # 1개의 인증 객체를 인스턴스화, 매개변수 입력 시 Tencent Cloud 계정 secretId, secretKey에 전송 필요
    cred = credential.Credential("secretId", "secretKey")

    #인스턴스화 시 제품(예: cdb)의 client 객체 요청 필요
    client = cdb_client.CdbClient(cred, "ap-shanghai")

    #요청 객체 인스턴스화:req = models.ModifyInstanceParamRequest()
    req = models.InitDBInstancesRequest()
    req.InstanceIds = ["cdb-c752yqcn"]
    req.NewPassword = "CDB@Qcloud"
    
    req.Parameters = [{"name":"max_connections","value":"100"},{"name":"character_set_server","value":"utf8"},{"name":"lower_case_table_names","value":"1"}]


    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.InitDBInstances(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

