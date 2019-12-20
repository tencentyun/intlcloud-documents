### 하위 계정에 생성된 메시지 대기열에 대한 모든 권한을 부여합니다

기업 계정 CompanyExample에 하위 계정 Developer가 있습니다. 이 하위 계정은 자신이 생성한 메시지 대기열에 접근할 수 있기를 바랍니다.

솔루션 A:

기업 계정 CompanyExample은 미리 설정 전략 QCloudCmqQueueCreaterFullAccess 및 QCloudCmqTopicCreaterFullAccess를 하위 계정 Developer에 직접적으로 부여합니다. 권한 부여 방법은 [권한 부여 관리](https://intl.cloud.tencent.com/document/product/598/10602)를 참조하십시오.

솔루션 B:

단계1: 전략 구문을 통해 다음 전략을 생성합니다

```
{
    "version": "2.0",
    "statement":
    [
       {
           "effect": "allow",
           "action": "cmqtopic:*",
           "resource": "qcs::cmqtopic:::topicName/uin/${uin}/*"
       },
       {
           "effect": "allow",
           "action": "cmqqueue:*",
           "resource": "qcs::cmqqueue:::queueName/uin/${uin}/*"
       }
    ]
}
```

단계2: 하위 계정에 이 전략을 권한 부여합니다. 권한 부여 방법은 [권한 부여 관리](https://intl.cloud.tencent.com/document/product/598/10602)를 참조하십시오.


