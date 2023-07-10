## 소개

CKafka로 데이터 내보내기는 [Serverless Cloud Function](https://www.tencentcloud.com/document/product/583) 기반의 Tencent Cloud COS에서 제공하는 데이터 내보내기 솔루션으로, 사용자는 CSV, JSON 등의 파일 형식의 데이터를 리전 내 Tencent Cloud CKafka 서비스로 내보낼 수 있으며, 대용량 메시지 및 로그 데이터의 취합 분석에 사용됩니다.

## 주의 사항

- CKafka로 데이터 내보내기 기능에는 COS 데이터 인덱스 인터페이스가 포함되며, 제한 사항에 대한 자세한 내용은 [Select 개요](https://intl.cloud.tencent.com/document/product/436/32472)를 참고하십시오.
- COS 콘솔에서 버킷에 CKafka로 데이터 내보내기 규칙을 추가한 적이 있는 경우 [SCF 콘솔](https://console.cloud.tencent.com/scf/list?rid=1&ns=default)에서 기존에 생성한 CKafka로 데이터를 내보내기 함수를 확인할 수 있습니다. CKafka로 데이터 내보내기 함수를 삭제하거나 수정하지 **마십시오.** 그렇지 않으면 규칙이 적용되지 않을 수 있습니다.
- 현재 CKafka로 데이터 내보내기 기능은 광저우, 상하이, 베이징, 청두만 지원합니다.
- COS CKafka로 데이터를 내보내기 기능은 SCF 서비스에 종속됩니다. SCF 서비스는 사용자에게 [Free Tier](https://intl.cloud.tencent.com/document/product/583/12282)를 제공하며 무료 한도를 초과한 부분에 대해서는 [SCF Pricing](https://intl.cloud.tencent.com/document/product/583/12281)에 따라 청구됩니다.

## 작업 단계

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 사이드바에서 **애플리케이션 통합 > 데이터 내보내기**를 클릭하고 **CKafka로 데이터 내보내기**를 찾습니다.
3. **규칙 설정**을 클릭하여 규칙 설정 페이지로 이동합니다.
4. **함수 추가**를 클릭합니다.
>! SCF 서비스가 활성화되지 않은 경우 [SCF 콘솔](https://console.cloud.tencent.com/scf)에서 SCF 서비스를 활성화하고 안내에 따라 서비스 권한 부여를 완료하십시오.
>
5. 팝업 창에서 다음과 같이 정보를 설정합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/46de1cee616ab7e4dcf344c4598725db.png)
   - **함수 이름 접두사**: 함수의 고유 식별자로, 생성 후에는 수정할 수 없습니다. [SCF 콘솔](https://console.cloud.tencent.com/scf/list?rid=1&ns=default)에서 해당 함수를 조회할 수 있습니다.
   - **시나리오 선택**: 내보낼 로그 소스를 선택하십시오. COS 로그 파일 내보내기 사용을 권장합니다.
   - **소스 버킷**: 로그가 저장되는 버킷의 이름으로, COS 로그 파일 내보내기를 선택하는 경우 먼저 COS 로그 스토리지 기능을 활성화해야 합니다.
   - **로그 스토리지 상태**: 로그 스토리지 상태가 활성화되어 있는지 확인해야 합니다.
   - **전달 버킷**: 로그가 저장될 버킷입니다.
   - **로그 접두사 전달**: 로그를 찾기 쉬운 경로 접두사를 입력합니다.
   - **SCF 권한 부여**: CKafka로 데이터를 내보내려면 SCF가 버킷에서 로그 파일을 읽을 수 있는 권한이 필요합니다. 따라서 이 권한 부여를 추가해야 합니다.
6. **사전 설정 매개변수 입력**을 클릭하여 CKafka로 데이터 내보내기를 설정합니다. 설정 항목에 대한 설명은 다음과 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/bf08c9eac65f58fd6beb5f3afd7bb0be.png)
   - **액세스 방법**: CKafka의 액세스 방법입니다. VPC 내부 네트워크 액세스를 선택하는 경우 해당 VPC를 입력해야 합니다.
   - **액세스 주소**: CKafka의 액세스 주소입니다.
   - **주제 이름**: 생성한 CKafka 주제의 이름입니다.
   - **인증 설정**: CKafka 인증 방식으로 **인증 필요**를 선택하면 해당 사용자 이름과 사용자 비밀번호를 입력해야 합니다.
   - **속도 최댓값**: CKafka로 내보내기 위한 속도 최댓값입니다.
7. 일부 맞춤 설정된 로그 데이터 추출은 **이전**을 클릭하여 설정할 수 있습니다. 일반적으로 **확인**을 직접 클릭하여 함수 추가를 완료할 것을 권장합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/9e1ba247fd0515f8d30b056dd728d874.png)
   새로 생성한 함수에 다음과 같은 작업을 진행할 수 있습니다.
 - **로그**를 클릭하여 CKafka로 데이터 내보내기의 이전 실행을 조회합니다. CKafka로 데이터 내보내기 시 오류가 발생하면 **로그**를 클릭하여 SCF 콘솔로 빠르게 리디렉션하여 로그 오류 세부 정보를 조회할 수도 있습니다.
 - **세부 사항**을 클릭하면 현재 함수의 설정 세부 사항을 볼 수 있습니다.
 - **편집**을 클릭하여 CKafka로 데이터 내보내기 규칙을 수정합니다.
 - **트리거**를 클릭하여 버킷의 기존 로그를 선택하고 CKafka로 내보내기를 직접 트리거할 수 있습니다.
 - **삭제**를 클릭하여 사용하지 않는 CKafka로 데이터 내보내기 규칙을 삭제합니다.
