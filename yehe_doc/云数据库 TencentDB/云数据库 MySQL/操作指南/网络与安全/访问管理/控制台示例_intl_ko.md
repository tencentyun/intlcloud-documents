
CAM 정책을 통해 사용자에게 CDB 콘솔에서 특정 리소스에 대한 조회 및 사용 권한을 부여할 수 있습니다. 이 예시는 사용자가 콘솔에서 특정 정책을 사용할 수 있도록 설정하는 방법에 관해 설명합니다.

## CDB의 전체 읽기/쓰기 정책
사용자에게 CDB 인스턴스에 대한 생성 및 관리 권한을 부여할 경우, 해당 사용자에게 QcloudCDBFullAccess 정책을 사용할 수 있습니다.

[정책 관리](https://console.cloud.tencent.com/cam/policy) 인터페이스로 이동해 오른쪽 상단 검색창에서 QcloudCDBFullAccess를 검색하면 해당 정책을 찾을 수 있습니다.
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
위 정책은 CAM 정책으로 CDB, VPC, 보안 그룹, COS, KMS, Monitor의 모든 리소스에 대한 권한을 사용자에게 부여합니다.

## CDB의 읽기 전용 정책
사용자에게 CDB 인스턴스에 대한 생성, 삭제, 수정 권한 없이 조회 권한만 부여할 경우, 해당 사용자에게 QcloudCDBInnerReadOnlyAccess 정책을 사용할 수 있습니다.

>?CDB의 읽기 전용 정책 설정을 권장합니다.

[정책 관리](https://console.cloud.tencent.com/cam/policy) 인터페이스로 이동해 [서비스 유형] 항목을 클릭하고, 드롭다운 메뉴에서 [TencentDB for MySQL]을 선택하면 해당 정책을 찾을 수 있습니다.

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
사용자에게 CDB 인스턴스에 대한 생성, 삭제, 수정 권한 없이 인스턴스 및 관련 리소스(VPC, 보안 그룹, COS, Monitor) 조회 권한만 부여할 경우, 해당 사용자에게 QcloudCDBReadOnlyAccess 정책을 사용할 수 있습니다.

[정책 관리](https://console.cloud.tencent.com/cam/policy) 인터페이스로 이동해 [서비스 유형] 항목을 클릭하고, 드롭다운 메뉴에서 [TencentDB for MySQL]을 선택하면 해당 정책을 찾을 수 있습니다.

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
위 정책은 CAM 정책으로 다음 작업에 대한 권한을 사용자에게 부여합니다.
- CDB에서 'Describe'로 시작되는 모든 작업
- VPC에서 'Describe', 'Inquiry', 'Get'으로 시작되는 모든 작업
- 보안 그룹에서 'DescribeSecurityGroup'으로 시작되는 모든 작업
- COS에서 'List', 'Get', 'Head', 'OptionsObject'로 시작되는 모든 작업
- Monitor에 있는 모든 작업

## 사용자에게 리소스 레벨 이외의 API 인터페이스 작업 권한을 부여하는 정책
사용자에게 리소스 레벨 이외의 API 인터페이스에 대한 작업 권한을 부여할 경우, 해당 사용자에게 QcloudCDBProjectToUser 정책을 사용할 수 있습니다.
[정책 관리](https://console.cloud.tencent.com/cam/policy) 인터페이스로 이동해 [서비스 유형] 항목을 클릭하고 드롭다운 메뉴에서 [TencentDB for MySQL]을 선택하면 해당 정책을 찾을 수 있습니다.
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
사용자에게 특정 CDB에 대한 작업 권한을 부여할 경우, 아래 정책을 해당 사용자에게 연결할 수 있습니다. 아래 정책은 사용자에게 ID가 cdb-xxx인 광저우 리전의 CDB 인스턴스에 대한 작업 권한을 허용합니다.
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
사용자에게 CDB에 대한 일괄 작업 권한을 부여할 경우, 아래 정책을 해당 사용자에게 연결할 수 있습니다. 아래 정책은 사용자에게 ID가 cdb-xxx, cdb-yyy인 광저우 리전의 CDB 인스턴스 및 ID가 cdb-zzz인 베이징 리전의 CDB 인스턴스에 대한 작업 권한을 허용합니다.
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
사용자에게 특정 리전의 CDB에 대한 작업 권한을 부여할 경우, 아래 정책을 해당 사용자에게 연결할 수 있습니다. 아래 정책은 사용자에게 광저우 리전의 CDB 디바이스에 대한 작업 권한을 허용합니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cdb:*",
            "resource": "qcs::cvm:ap-guangzhou::*",
            "effect": "allow"
        }
    ]
}
```

## 사용자 정의 정책
사전 설정 정책이 원하는 정책을 충족하지 못할 경우 사용자 정의 정책을 생성할 수 있습니다. 리소스에 따른 권한 부여 시, 리소스 레벨의 권한을 지원하지 않는 CDB API 작업에 대해서도 해당 작업에 대한 사용 권한을 부여할 수 있습니다. 단, 정책 명령의 리소스 엘리먼트는 반드시 *로 지정해야 합니다.
     
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
