## 컴퓨팅 환경 사용 예
본 예시는 명령행을 사용하여 컴퓨팅 환경을 생성한 다음, 지정 컴퓨팅 환경에 하나의 작업을 제출하고 마지막으로 컴퓨팅 환경을 폐기하는 방법을 소개합니다.

## 시작 전 준비
시작하기 전에 문서 [시작 전 준비](/doc/product/599/10807)의 검사 리스트에 따라 준비하십시오. 본 예시는 CLI와 COS를 사용하기 때문에 사용자는 먼저 CLI를 설치 및 구성하고 COS Bucket을 생성해야 합니다.

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

### 결과 저장용 COS Bucket 생성

이 간단한 예시에서 결과는 시스템 표준 출력에 바로 출력됩니다. Batch는 시스템 표준 출력 stdout와 stderr를 수집할 수 있고 태스크 종료 후 정보를 지정한 COS Bucket에 업로드할 수 있습니다. 정보 저장용 Bucket과 서브 폴더를 미리 준비해야 합니다.

[CLI - 사전 준비](/doc/product/599/10548)에서 3장 **"COS 디렉터리 준비"**를 참조하여 대응하는 COS Bucket과 서브 폴더를 생성하십시오.


## 컴퓨팅 환경 생성

홈페이지에서 제공하는 예제를 수정하여 계정에 실행할 수 있는 Batch 컴퓨팅 환경을 생성할 수 있습니다. 그 전에 우선 컴퓨팅 환경 구성 항목의 함의를 확인하십시오.
[컴퓨팅 환경 생성](/document/api/599/12691) 등 컴퓨팅 환경 관련 API를 참조하셔도 됩니다.

```
qcloudcli batch CreateComputeEnv --Version 2017-03-12 --ComputeEnv '{
    "EnvName": "test compute env",          // 컴퓨팅 환경 이름
    "EnvDescription": "test compute env",   // 컴퓨팅 환경 설명
    "EnvType": "MANAGED",                   // 컴퓨팅 환경 유형, 관리형
    "EnvData": {                            // 구체적인 구성(CVM 인스턴스 생성 설명 참조)
        "InternetAccessible": {
            "PublicIpAssigned": "TRUE",
            "InternetMaxBandwidthOut": 50
        },
        "LoginSettings": {
            "Password": "B1[habcd"
        },
        "InstanceType": "S1.SMALL1",        // CVM 인스턴스 유형
        "ImageId": "img-xxxxyyyy"           // CVM 이미지 ID(교체가 필요함)
    },
    "DesiredComputeNodeCount": 2            // 컴퓨팅 예상 노드 수
}'
--Placement'{
    "Zone": "ap-guangzhou-2"                // 가용 영역(교체 필요할 수 있음)
}'
```


#### 요청 예제
```
qcloudcli batch CreateComputeEnv --Version 2017-03-12  --ComputeEnv '{"EnvName": "test compute env", "EnvDescription": "test compute env", "EnvType": "MANAGED", "EnvData": {"InstanceType": "S1.SMALL2", "ImageId": "교체 예정", "LoginSettings": {"Password": "교체 예정"}, "InternetAccessible": {"PublicIpAssigned": "TRUE", "InternetMaxBandwidthOut": 50}, "SystemDisk": {"DiskType": "CLOUD_BASIC", "DiskSize": 50 } }, "DesiredComputeNodeCount": 2 }' --Placement '{"Zone": "ap-guangzhou-2"}'
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

## 컴퓨팅 환경 목록 보기
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


## 지정 컴퓨팅 환경 보기
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

## 지정 컴퓨팅 환경에 태스크 제출
#### 요청 예제
```
qcloudcli batch SubmitJob --Version 2017-03-12  --Job '{"JobName": "test job", "JobDescription": "xxx", "Priority": "1", "Tasks": [{"TaskName": "hello2", "TaskInstanceNum": 1,  "Application": {"DeliveryForm": "LOCAL", "Command": "python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "}, "EnvId": "교체 예정", "RedirectInfo": {"StdoutRedirectPath": "cos://dondonbatch-1251783334.cosgz.myqcloud.com/hello2/logs/", "StderrRedirectPath":  "cos://dondonbatch-1251783334.cosgz.myqcloud.com/hello2/logs/"} } ] }' --Placement '{"Zone": "ap-guangzhou-2"}'

```

#### 반환 결과 예제
```
{
    "Response": {
        "RequestId": "cf821ae0-71d6-42b1-b878-6ecdeec15796",
        "JobId": "job-lhi5agkh"
    }
}
```

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

