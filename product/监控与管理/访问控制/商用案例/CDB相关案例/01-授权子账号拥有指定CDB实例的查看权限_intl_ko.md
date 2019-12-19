### 하위 계정에 지정된 CDB 인스턴스에 대한 확인 권한을 부여합니다

기업 계정 CompanyExample(ownerUin은 12345678)에 서브 계정 Developer가 있습니다. 이 서브 계정은 기업 계정 CompanyExample의 두 개 CDB 인스턴스(인스턴스 ID는 각각 cdb-1 및 cdb-2)에 대한 확인 권한이 있어야 합니다.

단계1: 전략 구문을 통해 다음 전략을 생성합니다
```
 {
    "version": "2.0",
    "statement":
     {
         "effect": "allow",
         "action": "cdb:*",
         "resource": ["qcs::cdb::uin/12345678:instanceId/cdb-1", "qcs::cdb::uin/12345678:instanceId/cdb-2"]
     }
}
```
단계2: 하위 계정에 이 전략을 권한 부여합니다. 권한 부여 방법은 [권한 부여 관리](https://intl.cloud.tencent.com/document/product/598/10602)를 참조하십시오.

참고: 하위 계정 Developer는 CDB 조회 리스트 페이지에서 인스턴스 ID가 cdb-1 및 cdb-2인 리소스만 확인할 수 있습니다.
