CSS는 CAM 액세스 제어를 통해 권한을 관리하여 계정의 CSS 도메인, 설정, 데이터 정보를 편리하게 관리할 수 있습니다. 사용자(그룹)를 생성, 관리, 삭제할 수 있으며, 서브 계정(그룹)에 각기 다른 인터페이스 권한을 부여하여 신분 관리 및 정책을 제어할 수 있습니다.

CAM을 사용할 경우 정책을 하나의 사용자 또는 하나의 사용자 그룹과 연결할 수 있으며, 정책을 통해 사용자가 지정된 리소스로 지정된 작업을 완료할 수 있도록 권한을 부여하거나 거부할 수 있습니다.

## 기본 개념

- 루트 계정: 등록된 Tencent Cloud 계정입니다.
- 서브 계정: 루트 계정을 통해 생성되며, 루트 계정에 완전히 종속되는 계정입니다.
- 협업 파트너: 루트 계정의 신분을 보유하고 있으며 현 루트 계정의 협업 파트너로 추가된 계정으로, 현 루트 계정의 서브 계정 중 하나입니다.
- 사용자 그룹: 동일한 권한을 가진 일련의 사용자 그룹입니다. 정책과 연결할 수 있어 일괄적인 권한 관리가 용이합니다.

자세한 정의 및 권한 관련 내용은 [CAM 사용자](https://intl.cloud.tencent.com/document/product/598/32633)를 참고하십시오.

## 작업 순서
### 1단계: 서브 계정/사용자 그룹 생성

루트 계정은 하나 또는 다수의 서브 계정을 생성하여 특정 역할 및 정책을 할당할 수 있습니다. 서브 계정은 확인된 ID와 자격 증명을 가지고 있으며 콘솔에 로그인하여 설정을 완료할 수 있습니다. 동시에 API 액세스 권한도 가지고 있습니다. 다음 이미지와 같이 Tencent Cloud 콘솔에 로그인한 후 [액세스 관리](https://console.cloud.tencent.com/cam/) 페이지로 이동하여 사용자를 생성할 수 있습니다.

![](https://main.qcloudimg.com/raw/c1c92bdd08c8cf19ac17ba80cd4a11be.png)
자세한 방법은 액세스 관리의 [서브 계정](https://intl.cloud.tencent.com/document/product/598/13674) 및 [사용자 그룹](https://intl.cloud.tencent.com/document/product/598/33380)을 참고하십시오.

### 2단계: 사용자/사용자 그룹에 정책 추가

사용자/사용자 그룹 관리 및 정책 관리 페이지에서 정책을 추가하고 권한을 부여할 수 있습니다. 자세한 내용은 [권한 관리](https://intl.cloud.tencent.com/document/product/598/10602)를 참고하시기 바라며, 간략한 설명은 다음과 같습니다.

- 방법1: 사용자/사용자 그룹 페이지로 이동하여 정책을 추가할 사용자/사용자 그룹을 선택한 후, 작업 리스트에 있는 [권한 부여]/[정책 연결]를 클릭합니다. 해당 라이브 방송 정책을 선택하고 [확인]을 클릭하면 추가가 완료됩니다.
![](https://main.qcloudimg.com/raw/9da12095cfa57813a373ab9ffeabc9a4.png)

![](https://main.qcloudimg.com/raw/ec1e09ab6cde2a703ac90d7ccdad6424.png)

![](https://main.qcloudimg.com/raw/f09b5d456ba1fd554ad321ddcc67cbdc.png)

- 방법2: 정책 페이지로 이동하여 추가할 정책을 선택한 후, 작업 리스트에 있는 [사용자/그룹 연결]을 클릭합니다. 권한을 부여할 사용자를 선택하고 [확인]을 클릭하면 추가가 완료됩니다.
![](https://main.qcloudimg.com/raw/5b5e0dc032934846e39e7aee740ae34b.png)

**추가 가능한 정책**:
1. 시스템 사전 설정 정책 추가: 왼쪽 사이드 바를 통해 정책 페이지로 이동하면 현재 모든 정책 정보를 확인할 수 있습니다.
	- CSS 시스템의 사전 설정 정책은 [QcloudLIVEFullAccess](https://console.cloud.tencent.com/cam/policy/detail/9545933&QcloudLIVEFullAccess&2)(전체 읽기/쓰기 정책)와 [QcloudLIVEReadOnlyAccess](https://console.cloud.tencent.com/cam/policy/detail/13346800&QcloudLIVEReadOnlyAccess&2)(읽기 전용 정책)가 있습니다.
	- 태그를 사용해야 하는 경우, [QcloudTAGFullAccess](https://console.cloud.tencent.com/cam/policy/detail/1592575&QcloudTAGFullAccess&2) (태그(TAG) 전체 읽기/쓰기 액세스 정책) 권한을 부여해야 합니다.
	- 실시간 로그를 사용해야 하는 경우, [QcloudCamFullAccess](https://console.cloud.tencent.com/cam/policy/detail/596169&QcloudCamFullAccess&2) (사용자 및 권한(CAM) 전체 읽기/쓰기 액세스 권한 정책) 권한을 부여해야 합니다.
2. 사용자 정의 정책 추가: 정책 페이지로 이동하여 [사용자 정의 정책 생성]을 클릭한 후 [정책 생성기에서 생성]을 선택합니다. 자세한 내용은 [사용자 정의 정책](https://intl.cloud.tencent.com/document/product/598/10601)을 참고하십시오.

>? 현재 CSS의 일부 인터페이스는 리소스 레벨의 권한 부여를 지원합니다. 구체적인 인터페이스는 API 인증 규칙을 참고하십시오.

**예시**:
[인증서 추가] 인터페이스 권한을 서브 계정에 부여하고 지정 도메인에만 사용하는 경우, 다음 순서에 따라 설정합니다.
1. 해당 인터페이스에 액세스를 허용할 도메인 레벨의 정책을 생성하고 정책 생성기의 정책 생성 페이지로 이동합니다.
2. 각 항목을 입력합니다. [효과] 항목에 [허용]을 선택하고, [서비스] 항목에 [CSS]를 선택하고, [작업] 항목에 [도메인 리스트 조회]를 선택하고, [리소스] 항목에 권한을 부여할 도메인을 입력합니다. 구문은 다음과 같습니다.
```
qcs::${ApiModule}:${Region}:uin/:domain/${DomainName}
```
 그중에서,
 - `${ApiModule}`에 live를 입력합니다.
 - `${Region}`에 ap-guangzhou를 입력합니다.
 - `uin`은 권한 부여 계정으로 값을 비워둘 경우 현재 계정에 권한을 부여한다는 의미입니다.
 - `${DomainName}`에 권한을 부여할 도메인을 입력합니다.
 예시: `qcs::live:ap-guangzhou::domain/cloud.tencent.com`, [성명서 추가]>[다음]>[정책 생성]을 클릭하면 해당 정책이 생성됩니다. 정책 생성 후 상기 두 방법으로 사용자/사용자 그룹을 연결하면 됩니다.
![](https://main.qcloudimg.com/raw/2e28228e7226ad3617880b0985ee5709.png)

>?인터페이스 권한을 서브 계정 사용자에게 부여하고 모든 도메인에 적용할 경우 [리소스] 항목에 \*을 입력합니다.


### 3단계: 서브 계정 사용
서브 계정 자격(루트 계정에서 생성한 서브 계정 ID 및 비밀번호)을 사용해 권한이 부여된 API 인터페이스를 호출(예: "도메인 리스트 조회" 등)하여 해당하는 CSS 정보(예: 해당 계정의 모든 도메인)를 획득할 수 있습니다.

