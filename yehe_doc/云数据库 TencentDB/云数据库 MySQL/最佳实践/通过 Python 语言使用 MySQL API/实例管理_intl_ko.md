
| API        | 설명   | 
| --------   | -----  | 
|ModifyInstanceParam	|인스턴스 매개변수 수정|
|CloseWanService	|	인스턴스 외부 네트워크 액세스 종료|
|OpenWanService	 | 인스턴스 외부 네트워크 액세스 활성화|
|RestartDBInstances	|인스턴스 재시작|
|OpenDBInstanceGTID	|인스턴스 GTID 활성화|
|ModifyDBInstanceName	|CDB 인스턴스 이름 수정|
|ModifyDBInstanceProject	|CDB 인스턴스 서브 프로젝트 수정|
|ModifyDBInstanceVipVport	|CDB 인스턴스 IP와 포트 번호 수정|
|DescribeDBInstanceCharset	|CDB 인스턴스 문자 세트 조회|
|DescribeDBInstanceConfig	|CDB 인스턴스 설정 정보 조회|
|DescribeDBInstanceGTID	|CDB 인스턴스 GTID 활성화 여부 조회|
|DescribeDBInstanceRebootTime	|CDB 인스턴스 예상 재시작 시간 조회|

### ModifyInstanceParam  인스턴스 매개변수 수정

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

    #요청 객체 인스턴스화
    req = models.ModifyInstanceParamRequest()
    req.InstanceIds = ["cdb-1y6g3zj8","cdb-7ghaiocc"]
    req.ParamList = [{"name":"max_connections","currentValue":"100"},{"name":"character_set_server","currentValue":"utf8"},{"name":"lower_case_table_names","currentValue":"1"}]
    #req.ParamList = [{"name":"max_connections","currentValue":"100"}]
    #param = models.Parameter()
    #param.Name = "max_connections"
    #param.CurrentValue = "1000"
    #req.ParamList = [param]


    print req
    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.ModifyInstanceParam(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    msg = traceback.format_exc() # 방식1  
    print (msg) 

```

### CloseWanService	인스턴스 외부 네트워크 액세스 종료

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
    req = models.CloseWanServiceRequest()
    req.InstanceId = "cdb-1y6g3zj8"

    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.CloseWanService(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

### OpenWanService 인스턴스 외부 네트워크 액세스 활성화

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
    req = models.OpenWanServiceRequest()
    req.InstanceId = "cdb-1y6g3zj8"

    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.OpenWanService(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### RestartDBInstances	인스턴스 재시작

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
    req = models.DescribeDBInstancesRequest()
    #req.MasterInstanceId = "cdb-7ghaiocc"

    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.InitDBInstances(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### OpenDBInstanceGTID 인스턴스 GTID 활성화

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
    req = models.OpenDBInstanceGTIDRequest()
    req.InstanceId = "cdb-7ghaiocc"
    

    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.OpenDBInstanceGTID(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

### ModifyDBInstanceName	CDB 인스턴스 이름 수정

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
    client = cdb_client.CdbClient(cred, "ap-beijing")

    #요청 객체 인스턴스화:req = models.ModifyInstanceParamRequest()
    req = models.ModifyDBInstanceNameRequest()
    req.InstanceId = "cdb-cukm86n2"
    req.InstanceName = "1s 중국어”

    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.ModifyDBInstanceName(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```


### ModifyDBInstanceProject	CDB 인스턴스 서브 프로젝트 수정

```python

#!/usr/bin/python
# -*- coding: utf-8 -*-

# 클라우드 API 게이트 모듈 불러오기
import logging
import traceback
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cdb.v20170320 import cdb_client, models


def DescribeDBInstancesList():
    try:
        # 1개의 인증 객체를 인스턴스화, 매개변수 입력 시 Tencent Cloud 계정 secretId, secretKey에 전송 필요
        cred = credential.Credential("secretId", "secretKey")

        #인스턴스화 시 제품(예: cdb)의 client 객체 요청 필요
        client = cdb_client.CdbClient(cred, "ap-shanghai")

        #요청 객체 인스턴스화:req = models.ModifyInstanceParamRequest()
        req = models.ModifyDBInstanceProjectRequest()
        req.InstanceIds = ["cdb-7ghaiocc"]
        req.NewProjectId =1


        # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
        resp = client.ModifyDBInstanceProject(req)

        # json 포맷의 문자열 출력
        print(resp.to_json_string())
    except TencentCloudSDKException as err:
        msg = traceback.format_exc() # 방식1  
        print (msg) 



DescribeDBInstancesList()


```

### ModifyDBInstanceVipVport	CDB 인스턴스 IP와 포트 번호 수정

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
    req = models.ModifyDBInstanceVipVportRequest()
    req.InstanceId = "cdb-7ghaiocc"
    req.DstIp = "10.0.0.13"
    req.DstPort =1025
    req.UniqVpcId = 1111

    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.ModifyDBInstanceVipVport(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
        msg = traceback.format_exc() # 방식1  
        print (msg) 

```


### DescribeDBInstanceCharset	CDB 인스턴스 문자 세트 조회

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
    req = models.DescribeDBInstanceCharsetRequest()
    req.InstanceId = "cdb-1y6g3zj8"


    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.DescribeDBInstanceCharset(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

### DescribeDBInstanceConfig	CDB 인스턴스 설정 정보 조회

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
    req = models.DescribeDBInstanceConfigRequest()
    req.InstanceId = "cdb-1y6g3zj8"


    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.DescribeDBInstanceConfig(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```

### DescribeDBInstanceGTID	CDB 인스턴스 GTID 활성화 여부 조회

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
    req = models.DescribeDBInstanceGTIDRequest()
    req.InstanceId = "cdb-1y6g3zj8"


    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.DescribeDBInstanceGTID(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
    
```

### DescribeDBInstanceRebootTime<42/>CDB 인스턴스 예상 재시작 시간 조회

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
    req = models.DescribeDBInstanceRebootTimeRequest()
    req.InstanceIds = ["cdb-1y6g3zj8"]


    # client 객체를 통해 액세스할 인터페이스 호출, 요청 객체 전송 필요
    resp = client.DescribeDBInstanceRebootTime(req)

    # json 포맷의 문자열 출력
    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)

```
