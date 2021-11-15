
| API        | 설명   | 
| :--------   | :-----  | 
|CreateBackup	|CDB 백업 생성|
|DeleteBackup	|CDB 백업 삭제|
|DescribeBackupConfig	|CDB 백업 설정 정보 조회
|DescribeBackupDatabases	|백업 데이터베이스 리스트 조회|
|DescribeBackupTables	|지정 데이터베이스 백업 데이터 테이블 조회|
|DescribeBackups	|백업 로그 조회|
|DescribeBinlogs	|이진법 로그 조회|
|DescribeSlowLogs	|슬로우 쿼리 로그 조회|
|ModifyBackupConfig	|데이터베이스 백업 설정 수정|

### CreateBackup	CDB 백업 생성

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
    req = models.CreateBackupRequest()
    #req.MasterInstanceId = "cdb-7ghaiocc"
    req.BackupMethod = "logical"

    print req
    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.CreateBackup(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### DeleteBackup	CDB 백업 삭제

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
    req = models.DeleteBackupRequest()
    
    #req.MasterInstanceId = "cdb-7ghaiocc"
    #print  req.BackupId
    req.BackupId = 105119782

    
    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.DeleteBackup(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### DescribeBackupConfig	CDB 백업 설정 정보 조회

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
    #req.MasterInstanceId = "cdb-7ghaiocc"

    print req
    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.DescribeDBZoneConfig(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### DescribeBackupDatabases	백업 데이터베이스 리스트 조회

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
    req = models.DescribeBackupDatabasesRequest()
    #req.MasterInstanceId = "cdb-7ghaiocc"
    req.StartTime = "2018-08-02 15:19:19"

    print req
    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.DescribeBackupDatabases(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    msg = traceback.format_exc() # 방식1  
    print (msg) 
```


### DescribeBackupTables	지정 데이터베이스 백업 데이터 테이블 조회

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
    req = models.DescribeBackupTablesRequest()
    #req.MasterInstanceId = "cdb-7ghaiocc"
    req.StartTime = "2018-08-02 15:19:19"
    req.DatabaseName ="sissi"


    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.DescribeBackupTables(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### DescribeBackups	백업 로그 조회

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
    req = models.DescribeDBPriceRequest()
    #req.MasterInstanceId = "cdb-7ghaiocc"
     


    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.DescribeBackups(req)
    print resp

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### DescribeBinlogs	이진법 로그 조회

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
    req = models.DescribeDBPriceRequest()
    #req.MasterInstanceId = "cdb-7ghaiocc"


    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.DescribeDBInstances(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
    
```


### DescribeSlowLogs	슬로우 쿼리 로그 조회

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
    req = models.DescribeSlowLogsRequest()
    #req.MasterInstanceId = "cdb-7ghaiocc"


    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.DescribeSlowLogs(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
    
```


### ModifyBackupConfig	데이터베이스 백업 설정 수정

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
    req = models.ModifyBackupConfigRequest()
    req.InstanceId = "cdb-1y6g3zj8"
    req.ExpireDays = 10
    req.StartTime = "06:00-10:00"
    req.BackupMethod = "logical"
    print req


    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.ModifyBackupConfig(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```
