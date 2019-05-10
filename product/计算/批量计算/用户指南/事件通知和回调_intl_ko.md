## 개요 정보
Batch Compute는 작업과 컴퓨팅 환경에서 생성된 이벤트를 정보 서비스(CMQ) 형식으로 Throw합니다. 예를 들어 작업 실행 성공/실패, 컴퓨팅 환경 노드 생성 성공/실패/이상 등 이벤트가 발생하면 CMQ의 토픽 구독 메커니즘을 통해 공지와 콜백을 실현할 수 있습니다.

## 사용 가이드
컴퓨팅 환경 관련 이벤트 수신을 예로 들고 있습니다. 다음 3가지 단계에 따라 컴퓨팅 환경 관련 이벤트를 등록할 수 있습니다.

### 1. CMQ 토픽 생성
[CMQ 콘솔](https://console.cloud.tencent.com/mq/topic?rid=1)에 로그인하여 토픽을 생성합니다.
![](https://main.qcloudimg.com/raw/80a323febd0abe3607696b7a41567369.png)
### 2. 컴퓨팅 환경 생성 및 CMQ 관련 토픽 연결
작업 제출(SubmitJob) 또는 컴퓨팅 환경 생성(Create) 시 **notifications** 필드를 추가하고 수신할 이벤트 **event_name**을 지정합니다. 여러 개의 이벤트를 지정할 수 있습니다.
```
"notifications": [
    {
      "event_configs": [
        {
          "event_name": "JobFailed" // 이벤트 이름
        },
        {
          "event_name": "JobSucceed",
          "event_vars": [           // 사용자 지정 이벤트 매개변수
            {
              "name": "jobSucceed",
              "value": "Success"
            }
          ]
        }
      ],
      "topic_name": "job-message"   // CMQ Topic Name
    }
  ],
```
* 현재는 API 또는 CLI를 통해 컴퓨팅 환경 생성 시 CMQ 토픽을 연결만 지원하며 추후에 콘솔 작업도 지원할 예정입니다.
* event_vars: 이벤트가 생성한 고정 메시지 본체는 물론이고 사용자 지정 매개변수를 추가할 수 있습니다.
* topic_name: 관련 CMQ 토픽의 이름(**주의: ID가 아님**)입니다. 모든 이벤트 메시지가 해당 토픽에 전달되며, 토픽은 메시지를 다시 모든 구독자에게 포워딩합니다.

### 3. 구독자 설정 및 테스트
[CMQ 콘솔](https://console.cloud.tencent.com/mq/topic?rid=1)에서 새로 생성한 토픽에 구독자를 추가합니다. 간편하게 조회할 수 있게 이미 생성한 메시지 대기열로 지정할 수 있습니다.
![](https://main.qcloudimg.com/raw/d8f6b9e5b7710438267c82e5eaf4d1ad.png)
메시지 구조는 다음과 같습니다. 구독자가 메시지 대열을 지정하였다면 [CMQ 콘솔 - 메시지 수신](https://console.cloud.tencent.com/mq/receive)을 통해 Batch에서 토픽에 발송한 이벤트 메시지(메시지 수신 내의 메시지 내용은 Base64로 처리해야 함)를 빠르게 조회할 수 있습니다.
```
{
	"Events": [{
		"EventVersion": "1.0",
		"EventTime": "2018-06-15T14:43:17Z",
		"Region": "ap-guangzhou",
		"Batch": {
			"ComputeNodeId": "node-0iy7wxyo",
			"EnvId": "env-ptoxdb1t",
			"ComputeNodeState": "CREATED",
			"Mem": 8,
			"ResourceCreatedTime": "2018-06-15T14:43:18Z",
			"EnvName": "batch-env",
			"ComputeNodeInstanceId": "ins-9rikj9kw",
			"Cpu": 4
		},
		"EventName": "COMPUTE_NODE_CREATED",
		"EventVars": []
	}]
}
```

### 작업 관련 이벤트
유형 | 설명
-----|------
JOB_RUNNING | 작업 실행
JOB_SUCCEED | 작업 완료
JOB_FAILED | 작업 실패
JOB_FAILED_INTERRUPTED | 작업 실패 및 중단 
TASK_RUNNING | 태스크 실행
TASK_SUCCEED | 태스크 완료
TASK_FAILED | 태스크 실패
TASK_FAILED_INTERRUPTED | 태스크 실패 및 중단
TASK_INSTANCE_RUNNING | 태스크 인스턴스 실행
TASK_INSTANCE_SUCCEED | 태스크 인스턴스 완료
TASK_INSTANCE_FAILED | 태스크 인스턴스 실패
TASK_INSTANCE_FAILED_INTERRUPTED | 태스크 인스턴스 실패 및 중단

최신 정의와 제출 작업 API Demo에 대한 세부 정보는, [작업 제출 >>](https://cloud.tencent.com/document/product/599/12683)을 참조하십시오.

### 컴퓨팅 환경 관련 이벤트
유형 | 설명
-----|------
COMPUTE_ENV_CREATED | 컴퓨팅 환경 생성
COMPUTE_ENV_DELETED | 컴퓨팅 환경 삭제
COMPUTE_NODE_CREATED | 컴퓨팅 노드 생성 성공
COMPUTE_NODE_CREATION_FAILED |  컴퓨팅 노드 생성 실패
COMPUTE_NODE_RUNNING | 컴퓨팅 노드 실행 중
COMPUTE_NODE_ABNORMAL | 컴퓨팅 노드 이상
COMPUTE_NODE_DELETING | 컴퓨팅 노드 폐기 중 

최신 정의와 컴퓨팅 환경 생성 API Demo에 대한 세부 정보는, [컴퓨팅 환경 생성 >>](https://cloud.tencent.com/document/product/599/12683)을 참조하십시오.

