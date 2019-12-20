### 하위 계정에 VOD에 대한 모든 권한을 부여합니다

기업 계정 CompanyExample(ownerUin은 12345678)에 하위 계정 Developer가 있습니다. 이 하위 계정은 기업 계정 CompanyExample의 VOD 서비스에 대한 완전한 관리 권한이 있어야 합니다.

솔루션 A:

기업 계정 CompanyExample은 미리 설정 전략 QcloudVODFullAccess를 하위 계정 Developer에 직접적으로 부여합니다. 권한 부여 방법은 [권한 부여 관리](https://intl.cloud.tencent.com/document/product/598/10602)를 참조하십시오.

솔루션 B:

단계1: 전략 구문을 통해 다음 전략을 생성합니다
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "vod:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": "cos:*",
            "resource": "qcs::cos::uid/10022853:*",
            "effect": "allow"
        }
    ]
}
```
단계2: 하위 계정에 이 전략을 권한 부여합니다. 권한 부여 방법은 [권한 부여 관리](https://intl.cloud.tencent.com/document/product/598/10602)를 참조하십시오.
