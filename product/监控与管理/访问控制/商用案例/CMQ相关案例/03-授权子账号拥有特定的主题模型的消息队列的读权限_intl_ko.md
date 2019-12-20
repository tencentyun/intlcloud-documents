### 하위 계정에 특정 주제 모델의 메시지 대기열에 대한 읽기 권한을 부여합니다

기업 계정 CompanyExample(ownerUin: 12345678)에는 주제 모델을 기반으로 하는 메시지 대기열이 있습니다. 동시에 이 메시지 대기열에 접근하려는 하위 계정 Developer를 가지고 있습니다.

단계1: 전략 구문을 통해 다음 전략을 생성합니다
```
{
    "version": "2.0",
    "statement":   
     {
        "action": "cmqqueue:SendMessage",
        "resource":"qcs::cmqqueue:::queueName/uin/12345678/test-caten",
        "effect": "allow"
     } 
}
```

단계2: 하위 계정에 이 전략을 권한 부여합니다. 권한 부여 방법은 [권한 부여 관리](https://intl.cloud.tencent.com/document/product/598/10602)를 참조하십시오.

