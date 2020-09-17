
CAM 정책으로 사용자가 CDB 콘솔에서 특정 리소스에 대한 조회 및 사용 권한을 부여할 수 있습니다. 이 예시는 사용자가 콘솔에서 특정 정책을 사용하도록 설정하는 방법에 관해 설명합니다.


## CDB의 Full read/write 정책
사용자에게 CDB 인스턴스를 생성하고 관리할 수 있는 권한을 주고자 한다면, 해당 사용자의 이름에 대한 정책을 QcloudCDBFullAccess로 설정할 수 있습니다.

[정책 관리](https://console.cloud.tencent.com/cam/policy) 화면으로 이동해, 오른쪽 상단 검색창에서 QcloudCDBFullAccess를 검색하면 해당 정책을 찾을 수 있습니다.
![](https://main.qcloudimg.com/raw/5ec89e71595a5edd3e7f723a19c01a6a.png)
정책 구문은 아래와 같습니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cdb:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "vpc:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "cvm:*"
            ],
            "resource": "qcs::cvm:::sg/*",
            "effect": "allow"
        },
        {
            "action": [
                "cos:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "effect": "allow",
            "action": "monitor:*",
            "resource": "*"
        },
        {
            "action": [
                "kms:CreateKey",
                "kms:GenerateDataKey",
                "kms:Decrypt",
                "kms:ListKey"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
위 정책은 CDB, 사설 네트워크(VPC), 보안 그룹, 객체 스토리지(COS), KMS와 모니터(Monitor)의 모든 리소스에 대한 권한을 CAM 정책으로 사용자에게 각각 부여함으로써 목적을 달성할 수 있습니다.

## CDB의 읽기 전용 정책
사용자에게 생성, 삭제, 시작 및 수정 권한 없이, CDB 인스턴스를 조회하는 권한만 주고자 한다면 해당 사용자의 이름에 대한 정책을 QcloudCDBInnerReadOnlyAccess로 설정할 수 있습니다.

>?CDB의 읽기 전용 정책을 설정하시길 권장합니다

[정책 관리](https://console.cloud.tencent.com/cam/policy) 화면으로 이동해, [서비스 유형] 항목을 누르고 드롭다운 메뉴에서 [TencentDB for MySQL]을 선택하면 해당 정책을 찾을 수 있습니다.

정책 구문은 아래와 같습니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cdb:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

## CDB 관련 리소스의 읽기 전용 정책
사용자에게 생성, 삭제, 수정 등의 작업 권한 없이, CDB 인스턴스 및 관련 리소스(VPC, 보안 그룹, COS, Monitor)를 조회하는 권한만 주고자 한다면, 해당 사용자의 이름에 대한 정책을 QcloudCDBReadOnlyAccess로 설정할 수 있습니다.

[정책 관리](https://console.cloud.tencent.com/cam/policy) 화면으로 이동해, [서비스 유형] 항목을 누르고 드롭다운 메뉴에서 [TencentDB for MySQL]을 선택하면 해당 정책을 찾을 수 있습니다.

정책 구문은 아래와 같습니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cdb:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "vpc:Describe*",
                "vpc:Inquiry*",
                "vpc:Get*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "cvm:DescribeSecurityGroup*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "cos:List*",
                "cos:Get*",
                "cos:Head*",
                "cos:OptionsObject"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "effect": "allow",
            "action": "monitor:*",
            "resource": "*"
        }
    ]
}
```
위 정책은 아래에 대한 작업 권한을 CAM 정책으로 사용자에게 각각 부여함으로써 목적을 달성할 수 있습니다.
- CDB에서 “Describe”로 시작되는 모든 작업.
- VPC에서 “Describe”로 시작되는 모든 작업, “Inquiry”로 시작되는 모든 작업 및 “Get”으로 시작되는 모든 작업.
- 보안 그룹에서 “DescribeSecurityGroup”으로 시작되는 모든 작업.
- COS에서 “List”로 시작되는 모든 작업, “Get”으로 시작되는 모든 작업, “Head”로 시작되는 모든 작업 및 “OptionsObject”로 시작되는 모든 작업.
- Monitor에 있는 모든 작업.

## 사용자에게 리소스 이외의 API 작업 권한을 부여하는 정책
사용자에게 리소스 이외의 API에 대한 작업 권한을 주고자 한다면, 해당 사용자의 이름에 대한 정책을 QcloudCDBProjectToUser로 설정할 수 있습니다.
[정책 관리](https://console.cloud.tencent.com/cam/policy) 화면으로 이동해, [서비스 유형] 항목을 누르고 드롭다운 메뉴에서 [TencentDB for MySQL]을 선택하면 해당 정책을 찾을 수 있습니다.
정책 구문은 아래와 같습니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cdb:BalanceRoGroupLoad",
                "cdb:CancelBatchOperation",
                "cdb:CreateBatchJobFiles",
                "cdb:CreateDBInstance",
                "cdb:CreateDBInstanceHour",
                "cdb:CreateMonitorTemplate",
                "cdb:CreateParamTemplate",
                "cdb:DeleteBatchJobFiles",
                "cdb:DeleteMonitorTemplate",
                "cdb:DeleteParamTemplate",
                "cdb:DescribeBatchJobFileContent",
                "cdb:DescribeBatchJobFiles",
                "cdb:DescribeBatchJobInfo",
                "cdb:DescribeProjectSecurityGroups",
                "cdb:DescribeDefaultParams",
                "cdb:DescribeMonitorTemplate",
                "cdb:DescribeParamTemplateInfo",
                "cdb:DescribeParamTemplates",
                "cdb:DescribeRequestResult",
                "cdb:DescribeRoGroupInfo",
                "cdb:DescribeRoMinScale",
                "cdb:DescribeTasks",
                "cdb:DescribeUploadedFiles",
                "cdb:ModifyMonitorTemplate",
                "cdb:ModifyParamTemplate",
                "cdb:ModifyRoGroupInfo",
                "cdb:ModifyRoGroupVipVport",
                "cdb:StopDBImportJob",
                "cdb:UploadSqlFiles"
            ],
            "effect": "allow",
            "resource": "*"
        }
    ]
}
```

## 사용자에게 특정 CDB 작업 권한을 부여하는 정책
사용자에게 특정 CDB에 대한 작업 권한을 주고자 한다면, 아래의 정책을 해당 사용자에게 연결할 수 있습니다. 아래의 정책은 사용자에게 ID가 cdb-xxx인 광저우 리전의 CDB 인스턴스에 대한 작업 권한을 허용합니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cdb:*",
            "resource": "qcs::cdb:ap-guangzhou::instanceId/cdb-xxx",
            "effect": "allow"
        }
    ]
}
```

## 사용자에게 일괄 CDB 작업 권한을 부여하는 정책
사용자에게 CDB에 대한 일괄 작업 권한을 주고자 한다면, 아래의 정책을 해당 사용자에게 연결할 수 있습니다. 아래의 정책은 사용자에게 ID가 cdb-xxx, cdb-yyy인 광저우 리전의 CDB 인스턴스 및 ID가 cdb-zzz인 베이징 리전의 CDB 인스턴스에 대한 작업 권한을 허용합니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cdb:*",
            "resource": ["qcs::cdb:ap-guangzhou::instanceId/cdb-xxx", "qcs::cdb:ap-guangzhou::instanceId/cdb-yyy", "qcs::cdb:ap-beijing::instanceId/cdb-zzz"],
            "effect": "allow"
        }
    ]
}
```

## 사용자에게 특정 리전 CDB 작업 권한을 부여하는 정책
사용자에게 특정 리전의 CDB에 대한 작업 권한을 주고자 한다면, 아래의 정책을 해당 사용자에게 연결할 수 있습니다. 아래의 정책은 사용자에게 광저우 리전의 CDB에 대한 작업 권한을 허용합니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cdb:*",
            "resource": "qcs::cdb:ap-guangzhou::*",
            "effect": "allow"
        }
    ]
}
```

## 사용자 정의 정책
정책 사전 설정이 사용자의 수요를 충족하지 못했다면 사용자 정의 정책을 생성할 수 있습니다. 리소스를 기준으로 권한을 주고자 한다면 리소스급 권한을 지원하지 않은 CDB API에 대한 작업 권한을 사용자에게 부여할 수 있습니다. 단, 정책 명령의 리소스 엘리먼트(Resource Element)를 반드시 *으로 지정해야 합니다.
     
사용자 정의 정책 구문은 아래와 같습니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "Action"
            ],
            "resource": "Resource",
            "effect": "Effect"
        }
    ]
}
```
- Action에서 허용 또는 거부할 작업으로 변경합니다.
- Resource에서 권한을 부여할 구체적인 리소스로 변경합니다.
- Effect에서 허용 또는 거부로 변경합니다.
