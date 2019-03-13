## 클러스터를 빠르게 생성하는 방법?
Batch Compute의 컴퓨팅 환경 능력을 사용하면 빠르며 효율적으로 CVM 클러스터를 유지보수할 수 있습니다. Batch의 컴퓨팅 환경은 일반적인 클러스터 개념과 대응하며, 아래 예시는 컴퓨팅 환경 능력을 사용하여 가성비 높은 리소스 클러스터를 손쉽게 생성/폐기하는 방법을 소개하고 있습니다. 현재 컴퓨팅 환경은 명령행 호출만 지원하니 우선 명령행 도구 설치 준비를 참조하십시오.

## 시작 전 준비
시작하기 전에는 문서 [시작 전 준비](/doc/product/599/10807)의 검사 리스트에 따라 잘 준비하십시오. 본 예시는 명령행 도구(CLI)를 사용하기 때문에 사용자는 우선 명령행 도구를 설치 및 구성해야 합니다.

### CLI 설치 및 구성
CLI 구성은 [CLI 구성](/doc/product/440/6184)을 참조하십시오. 설치 후 설치 성공 여부를 검사하십시오.
```
qcloudcli batch help

CreateComputeEnv                        	|DescribeJobSubmitInfo
CreateTaskTemplate                      	|DescribeJobs
DeleteComputeEnv                        	|DescribeTask
DeleteJob                               	|DescribeTaskTemplates
DeleteTaskTemplates                     	|ModifyTaskTemplate
DescribeAvailableCvmInstanceTypes       	|SubmitJob
DescribeComputeEnv                      	|TerminateJob
DescribeComputeEnvs                     	|TerminateTaskInstance
DescribeJob
```

## 컴퓨팅 환경 생성

홈페이지에서 제공하는 예제를 수정하여 계정에 실행할 수 있는 Batch 컴퓨팅 환경을 생성할 수 있습니다. 그 전에 우선 컴퓨팅 환경 구성 항목의 함의를 확인하십시오.
[컴퓨팅 환경 생성](/document/api/599/12691) 등 컴퓨팅 환경 관련 API를 참조하셔도 됩니다.

아래 예시는 광저우 2 지역에서 BS1.LARGE8(BatchCompute 통용형 CPU 4코어 메모리 8GB) 10대를 포함한 유형의 클러스터를 빠르게 생성하는 방법입니다.

```
qcloudcli batch CreateComputeEnv --Version 2017-03-12 --ComputeEnv '{
    "EnvName": "batch-env",          // 컴퓨팅 환경 이름
    "EnvDescription": "batch env demo",   // 컴퓨팅 환경 설명
    "EnvType": "MANAGED",                   // 컴퓨팅 환경 유형, 관리형
    "EnvData": {                            // 구체적인 구성(CVM 인스턴스 생성 설명 참조)
        "InstanceType": "BS1.LARGE8",       // 컴퓨팅 환경 내 CVM 인스턴스 유형
        "ImageId": "img-m4q71qnf",          // 컴퓨팅 환경 내 CVM 이미지 ID(사용자 지정 이미지로 교체 가능)
        "LoginSettings": {
            "Password": "B1[habcd"          // 컴퓨팅 환경 내 CVM 로그인 비밀번호
        },
        "InternetAccessible": {
            "PublicIpAssigned": "TRUE",     // 컴퓨팅 환경 내 CVM 공인 IP 필요 여부
            "InternetMaxBandwidthOut": 10   // 컴퓨팅 환경 내 CVM 대역폭 한도
        },
        "SystemDisk": {
            "DiskType": "CLOUD_BASIC",      // 컴퓨팅 환경 내 CVM 디스크 유형(현재는 HDD 클라우드 디스크)
            "DiskSize": 50                  // 컴퓨팅 환경 내 CVM 디스크 크기
        }
    },
    "DesiredComputeNodeCount": 10           // 컴퓨팅 예상 노드 수
}'
--Placement'{
    "Zone": "ap-guangzhou-2"                // 가용 영역(현재 광저우 2 지역에 교체 가능성이 있음)
}'
```

#### 요청 예제
```
qcloudcli batch CreateComputeEnv --Version 2017-03-12 --ComputeEnv '{"EnvName":"batch-env","EnvDescription":"batch env demo","EnvType":"MANAGED","EnvData":{"InstanceType":"BS1.LARGE8","ImageId":"img-m4q71qnf","LoginSettings":{"Password":"B1[habcd"},"InternetAccessible":{"PublicIpAssigned":"TRUE","InternetMaxBandwidthOut":50},"SystemDisk":{"DiskType":"CLOUD_BASIC","DiskSize":50}},"DesiredComputeNodeCount":1}' --Placement '{"Zone": "ap-guangzhou-2"}'
```

#### 반환 결과 예제
반환값, 그 중 EnvId는 Batch 컴퓨팅 환경의 유일한 ID입니다.
```
{
    "Response": {
        "EnvId": "env-c96rwhnf",
        "RequestId": "bead16d4-b33b-47b5-9b86-6a02b4bed1b2"
    }
}
```
생성한 CVM을 CVM 콘솔을 통해 조회하거나 Batch 컴퓨팅 환경 API를 통해 조회 및 관리할 수 있습니다. 다음은 Batch의 명령행 API를 통해 컴퓨팅 환경 및 컴퓨팅 환경 내 인스턴스 정보를 조회하는 방법을 소개하고 있습니다. EnvId를 사용하면 반환 EnvId를 기록할 수 있습니다.

## 컴퓨팅 환경 목록 보기

Batch의 명령행 API를 통해 생성한 모든 컴퓨팅 환경 리스트를 조회할 수 있습니다.

#### 요청 예제
```
qcloudcli batch DescribeComputeEnvs --Version 2017-03-12
```

#### 반환 결과 예제
```
{
    "Response": {
        "TotalCount": 1,
        "ComputeEnvSet": [
            {
                "EnvId": "env-c96rwhnf",
                "Placement": {
                    "Zone": "ap-guangzhou-2"
                },
                "EnvType": "MANAGED",
                "EnvName": "test compute env",
                "ComputeNodeMetrics": {
                    "CreatedCount": 0,
                    "DeletingCount": 0,
                    "CreationFailedCount": 0,
                    "SubmittedCount": 0,
                    "CreatingCount": 0,
                    "AbnormalCount": 0,
                    "RunningCount": 2
                },
                "CreateTime": "2017-11-27T07:10:02Z"
            }
        ],
        "RequestId": "bac76f1c-06cd-4ef4-82a9-f230fa5a1992"
    }
}
```
반환 결과에 조회할 컴퓨팅 환경 정보를 포함합니다.

## 지정한 컴퓨팅 환경 및 포함한 노드 리스트 조회
#### 요청 예제
```
qcloudcli batch DescribeComputeEnv --Version 2017-03-12 --EnvId env-c96rwhnf
```

#### 반환 결과 예제
```
{
    "Response": {
        "EnvId": "env-c96rwhnf",
        "Placement": {
            "Zone": "ap-guangzhou-2"
        },
        "EnvType": "MANAGED",
        "EnvName": "test compute env",
        "RequestId": "12dc7dba-f33b-4d5a-8cd6-ebd1df17ebf7",
        "ComputeNodeMetrics": {
            "CreatedCount": 0,
            "DeletingCount": 0,
            "CreationFailedCount": 0,
            "SubmittedCount": 0,
            "CreatingCount": 0,
            "AbnormalCount": 0,
            "RunningCount": 2
        },
        "ComputeNodeSet": [
            {
                "ComputeNodeId": "node-838udz1w",
                "ComputeNodeState": "RUNNING",
                "Mem": 2,
                "ResourceCreatedTime": "2017-11-27T07:10:46Z",
                "ComputeNodeInstanceId": "ins-q09nyg5g",
                "AgentVersion": "1.0.7",
                "TaskInstanceNumAvailable": 1,
                "Cpu": 1
            },
            {
                "ComputeNodeId": "node-c4z8f8xc",
                "ComputeNodeState": "RUNNING",
                "Mem": 2,
                "ResourceCreatedTime": "2017-11-27T07:10:41Z",
                "ComputeNodeInstanceId": "ins-fgqcau4q",
                "AgentVersion": "1.0.7",
                "TaskInstanceNumAvailable": 1,
                "Cpu": 1
            }
        ],
        "CreateTime": "2017-11-27T07:10:02Z"
    }
}
```

컴퓨팅 환경 전체 및 모든 노드의 세부 정보를 포함합니다.

## 컴퓨팅 환경 폐기
#### 요청 예제
```
qcloudcli batch DeleteComputeEnv --Version 2017-03-12 --EnvId env-c96rwhnf
```

#### 반환 결과 예제
```
{
    "Response": {
        "RequestId": "389f011a-7dbd-4993-82fe-334ac923ff88"
    }
}
```

호출 후 컴퓨팅 환경은 클러스터 내의 모든 CVM을 자동으로 폐기합니다.

