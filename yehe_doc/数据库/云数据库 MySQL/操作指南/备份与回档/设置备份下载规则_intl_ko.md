
기본적으로 공용 또는 내부 네트워크를 통해 TencentDB for MySQL 인스턴스의 백업 파일을 다운로드할 수 있습니다. 다운로드를 제한하려면 백업 다운로드 설정을 조정할 수 있습니다.
>?
>- 데이터베이스 백업 다운로드 설정은 다음 리전에서 지원됩니다.
>광저우, 상하이, 베이징, 선전, 청두, 충칭, 난징, 중국홍콩, 토론토, 싱가포르, 실리콘밸리, 프랑크푸르트, 서울, 뭄바이, 방콕, 모스크바, 도쿄.
>- 백업 다운로드 설정 활성화 방법:
>  - 2021년 11월 09일 이전에 이 기능을 활성화하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 해야합니다.
>  - 2021년 11월 09일 부터 이 기능은 콘솔에서 사용할 수 있습니다.

## 백업 다운로드 규칙 설정
1. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 후, 왼쪽 사이드바에서 **데이터베이스 백업**을 선택하고 상단에서 리전을 선택합니다.
2. **다운로드 설정** 탭에서 백업 다운로드 설정을 조회하고 **편집**을 클릭하여 수정합니다.
>?공용 네트워크를 통한 다운로드는 기본적으로 활성화되어 있으며 활성화되면 내부 네트워크를 통한 다운로드도 허용됩니다.
>
![](https://qcloudimg.tencent-cloud.cn/raw/530fbf3e6c93eea06ff23e112cad84c0.png)
3. 표시된 페이지에서 다운로드 규칙을 설정하고 **확인**을 클릭합니다.
   - 공용 네트워크를 통해 다운로드:
     - 활성화됨: 다운로드 규칙을 설정할 수 없습니다.
     - 비활성화됨: 특정 IP 및 VPC를 허용하거나 차단하여 다운로드 규칙을 설정할 수 있습니다.
   - 다운로드 조건 설정:
     - 값을 지정하지 않으면 조건이 적용되지 않습니다.
     - IP 주소 조건 값은 ‘,’로 구분합니다.
     - IP 조건의 값으로 IP 또는 IP 대역을 입력할 수 있습니다.
     - IP 및 VPC 요구 사항이 설정되지 않은 경우 내부 네트워크를 통한 다운로드에 제한이 없습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7e0a4a48af62fdd643259f8902fcd95f.png)
4. 구성이 완료되면 **다운로드 설정** 탭으로 돌아가 적용된 규칙을 확인합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/cb4ac45dcde8a57610b0eaec9075c6cb.png)

## 서브 계정에 백업 다운로드 규칙 설정 권한 부여
기본적으로 서브 계정에는 MySQL 인스턴스용 TencentDB에 대한 백업 다운로드 규칙을 설정할 수 있는 권한이 없습니다. 따라서 특정 서브 계정에 권한을 부여하려면 CAM 정책을 생성해야 합니다.

[Cloud Access Management](https://intl.cloud.tencent.com/document/product/598/10583)(CAM)는 Tencent Cloud에서 제공하는 웹 서비스로, 사용자가 Tencent Cloud 계정의 리소스에 대한 액세스 권한을 안전하게 관리하는 데 주로 사용합니다. CAM으로 사용자(그룹)를 생성, 관리 및 폐기할 수 있으며, 신분 관리 및 정책 관리를 통해 누가 어떤 Tencent Cloud 리소스를 사용할지 제어할 수 있습니다.

CAM 사용 시, 정책과 사용자(그룹)를 연결하여 사용자(그룹)가 지정된 리소스로 관련 작업을 완성하도록 인증하거나 거부할 수 있습니다. CAM 정책 관련 더 많은 정보는 [정책 구문](https://intl.cloud.tencent.com/document/product/598/10603)을 참고하십시오.

### 서브 계정 권한부여
1. 루트 계정으로 [CAM 콘솔](https://console.cloud.tencent.com/cam)에 로그인한 뒤 사용자 리스트에서 해당 서브 계정을 선택하고 **인증**을 클릭합니다.
![img](https://qcloudimg.tencent-cloud.cn/raw/89d7cf063bd376a0cc4f4db0c78e7e56.png)
2. 팝업 창에서 **QcloudCDBFullAccess CDB 전체 읽기/쓰기 액세스 권한** 사전 설정 정책을 선택하고 **확인**을 클릭하여 서브 계정 권한 부여를 완료합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/0819ca9a1a81fc00968f0a263dc7727e.png)

### 정책 구문
MySQL 데이터베이스 설정 다운로드 백업 규칙에 대한 CAM 정책은 다음과 같습니다.
```
{
       "version":"2.0",
       "statement":
       [
          {
             "effect":"effect",
             "action":["action"],
             "resource":["resource"]
            }
       ] 
}
```
- **버전 version**: 필수 작성 항목입니다. 현재는 ‘2.0’만 허용합니다.
- **명령 statement**: 하나 또는 다수의 권한과 관련한 자세한 정보를 설명하는 데 사용합니다. 이 요소에는 effect, action, resource 등 기타 여러 요소의 권한 또는 권한 집합이 포함됩니다. 하나의 정책은 하나의 statement 요소만 가집니다.
- **영향 effect**: 필수 작성 항목입니다. 선언으로 발생한 결과가 '허용'인지 '명시적 거절'인지 설명합니다. allow(허용) 및 deny(명시적 거절) 두 가지 상황을 포함합니다.
- **작업 action**: 필수 작성 항목입니다. 허용 또는 거절의 작업을 설명하는데 사용합니다. 작업은 API(접두사 name으로 표시) 또는 기능 집합(특정한 API 조합, 접두사 permid로 표시)이 가능합니다.
- **리소스 resource**: 필수 작성 항목입니다. 인증의 구체적인 데이터를 설명합니다. 

### API 작업
CAM 정책 명령에서 CAM 작업을 지원하는 모든 서비스에서 임의로 API 작업을 지정할 수 있습니다. 데이터베이스 감사 기능 API의 접두사는 name/cdb:을 사용하시기 바랍니다. 단일 명령어에서 다수의 작업을 지정할 경우, 쉼표로 다음과 같이 구분해 주시기 바랍니다.
```
"action":["name/cdb:action1","name/cdb:action2"]
```
와일드카드를 사용해서 여러 항목의 작업을 지정할 수 있습니다. 예를 들어, 다음과 같이 명칭이 단어 ‘Describe’로 시작하는 모든 작업을 지정할 수 있습니다.
```
"action":["name/cdb:Describe*"]
```

### 리소스 경로
리소스 경로의 일반 형식은 다음과 같습니다.
```
qcs::service_type::account:resource
```
- service_type: 제품 약칭. 여기에서는 cdb.
- account: uin/326xxx46과 같은 리소스 소유자의 루트 계정 정보.
- resource: 제품의 리소스 상세 내용, MySQL 인스턴스 (instanceId) 한 개가 리소스 한 개에 해당합니다. 

예시는 다음과 같습니다.
```
 "resource": ["qcs::cdb::uin/326xxx46:instanceId/cdb-kfxxh3"]
```
그 중, cdb-kfxxh3이 MySQL 인스턴스 리소스 ID이며 여기에서는 CAM 정책 명령의 리소스 resource입니다.

### 예시
다음 예는 CAM의 사용법만을 보여줍니다. MySQL 백업 다운로드 규칙 설정에 사용되는 API 전체 목록은 [API 문서](https://intl.cloud.tencent.com/document/product/236/43327)를 참고하십시오.
```
{
       "version":"2.0",
       "statement":
       [
          {
             "effect":"allow",
             "action": ["name/cdb: ModifyBackupDownloadRestriction"],
             "resource": ["*"]
            }
       ]
}
```

### MySQL 백업 다운로드 규칙 설정을 위한 CAM 정책 사용자 정의
1. 루트 계정으로 [CAM 콘솔](https://console.cloud.tencent.com/cam/policy)에 로그인한 후 정책 리스트에서 **사용자 정의 정책 생성**을 클릭합니다.
![img](https://qcloudimg.tencent-cloud.cn/raw/4ddc463dc28ee48b9dd63d862fa41ea1.png)
2. 팝업 창에서 **정책 생성기에서 생성**을 선택합니다. 
3. 서비스와 작업 선택 페이지에서 각 항목의 설정을 선택하고 성명서 추가를 클릭한 후 다음 단계를 클릭합니다.
   - 효과(Effect): 허용 또는 거부를 선택하여 작업 항목 실행 권한을 나타냅니다.
   - 서비스(Service): TencentDB for MySQL를 선택합니다.
   - 작업(Action): MySQL 백업 다운로드 규칙을 설정하는 모든 API를 선택합니다. 자세한 내용은 [API 문서](https://intl.cloud.tencent.com/document/product/236/43327)를 참고하십시오.
   - 리소스(Resource): 자세한 내용은 [리소스 설명 방법](https://intl.cloud.tencent.com/document/product/598/10606)을 참고하십시오. `*`를 입력하면 지정된 리전에서 TencentDB for MySQL 인스턴스의 백업 다운로드 규칙을 설정할 수 있음을 나타낼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5372ae1d2ac16ff63b63fbf175f3fccf.png)
4. 정책 편집 페이지에서 필요에 따라 ‘정책 이름’(예시: BackupDownloadRestriction)과 ‘설명’을 입력하고 **완료**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/3c5454e0da412c0e12beebb4b045979d.png)
5. 정책 리스트로 돌아가면 방금 생성한 사용자 정의 정책을 조회할 수 있습니다. 
![](https://qcloudimg.tencent-cloud.cn/raw/d242b34c0b9cad83d130444d84e205e0.png)

