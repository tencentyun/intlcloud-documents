CSS는 CAM 액세스 제어를 통해 권한을 관리하여 계정의 CSS 도메인, 설정, 데이터 정보를 편리하게 관리할 수 있습니다. 사용자(그룹)를 생성, 관리, 삭제할 수 있으며, 서브 계정(그룹)에 각기 다른 인터페이스 권한을 부여하여 신분 관리 및 정책을 제어할 수 있습니다.
CAM을 사용할 경우 정책을 하나의 사용자 또는 하나의 사용자 그룹과 연결할 수 있으며, 정책을 통해 사용자가 지정된 리소스로 지정된 작업을 완료할 수 있도록 권한을 부여하거나 거부할 수 있습니다.

## 기본 개념

- 루트 계정: 등록된 Tencent Cloud 계정입니다.
- 서브 계정: 루트 계정을 통해 생성되며, 루트 계정에 완전히 종속되는 계정입니다.
- 협업 파트너: 루트 계정의 신분을 보유하고 있으며 현 루트 계정의 협업 파트너로 추가된 계정으로, 현 루트 계정의 서브 계정 중 하나입니다.
- 사용자 그룹: 동일한 권한을 가진 일련의 사용자 그룹입니다. 정책과 연결할 수 있어 일괄적인 권한 관리가 용이합니다.

>? 자세한 정의 및 권한 관련 내용은 [User Types](https://intl.cloud.tencent.com/document/product/598/13665)를 참고하십시오.

## 작업 단계
### 1단계: 서브 계정/사용자 그룹 생성

루트 계정은 하나 또는 다수의 서브 계정을 생성하여 특정 역할 및 정책을 할당할 수 있습니다. 서브 계정은 확인된 ID와 자격 증명을 가지고 있으며 콘솔에 로그인하여 설정을 완료할 수 있습니다. 동시에 API 액세스 권한도 가지고 있습니다. 다음 이미지와 같이 Tencent Cloud 콘솔에 로그인한 후 [액세스 관리](https://console.cloud.tencent.com/cam/) 페이지로 이동하여 사용자를 생성할 수 있습니다.
![](https://main.qcloudimg.com/raw/809314273b9a8a01dfd9e686775df4bd.png)

>?자세한 방법은 액세스 관리의 [Sub-User](https://intl.cloud.tencent.com/document/product/598/13674) 및 [User Group](https://intl.cloud.tencent.com/document/product/598/33380)을 참고하십시오.

### 2단계: 사용자/사용자 그룹에 정책 추가

사용자/사용자 그룹 관리 및 정책 관리 페이지에서 정책을 추가하고 권한을 부여할 수 있습니다. 자세한 내용은 [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602)를 참고하시기 바라며, 간략한 설명은 다음과 같습니다.
<dx-tabs>
::: 방법1: 사용자 또는 사용자 그룹에 정책 추가
사용자/사용자 그룹 페이지로 이동하여 정책을 추가할 사용자/사용자 그룹을 선택합니다.
- CAM 콘솔의 왼쪽 사이드바에서 **사용자** > **사용자 목록**을 클릭하고 정책을 추가할 사용자/사용자 그룹을 선택한 후 오른쪽에서 **권한 부여**를 클릭하고 해당 CSS 정책을 선택한 후 **확인**을 클릭합니다.
![](https://main.qcloudimg.com/raw/e90b74bc2279512a5c075a57296ea2f1.png)
- 왼쪽 사이드바에서 **사용자** > **사용자 목록** 또는 **사용자 그룹**을 클릭하고 정책을 추가할 사용자/사용자 그룹의 이름을 클릭하여 세부 정보 페이지로 이동합니다. **정책 연결**을 클릭하여 해당 CSS 정책을 선택하고 **확인**을 클릭합니다.
![](https://main.qcloudimg.com/raw/5b5e0dc032934846e39e7aee740ae34b.png)
:::
::: 방법2: 사용자/사용자 그룹과 정책 연결
왼쪽 사이드바에서 **정책**을 클릭하고 추가할 정책을 선택하고 작업 열에서 **사용자/그룹 연결**을 클릭하고 권한을 부여할 사용자/사용자 그룹을 선택하고 **확인**을 클릭합니다.
![](https://main.qcloudimg.com/raw/c7948939b954b8f84a7a2ee9e5041ef4.png)
:::
</dx-tabs>

#### 추가 가능한 정책
- **사전 설정 정책 추가**: 왼쪽 사이드바에서 정책을 클릭하여 기존 정책을 모두 볼 수 있는 정책 페이지로 이동합니다.
   - CSS 시스템의 사전 설정 정책은 [QcloudLIVEFullAccess](https://console.cloud.tencent.com/cam/policy/detail/9545933&QcloudLIVEFullAccess&2)(전체 읽기/쓰기 정책)와 [QcloudLIVEReadOnlyAccess](https://console.cloud.tencent.com/cam/policy/detail/13346800&QcloudLIVEReadOnlyAccess&2)(읽기 전용 정책)가 있습니다.
   - 태그를 사용해야 하는 경우, [QcloudTAGFullAccess](https://console.cloud.tencent.com/cam/policy/detail/1592575&QcloudTAGFullAccess&2) (태그(TAG) 전체 읽기/쓰기 액세스 정책) 권한을 부여해야 합니다.
   - 실시간 로그를 사용해야 하는 경우, [QcloudCamFullAccess](https://console.cloud.tencent.com/cam/policy/detail/596169&QcloudCamFullAccess&2) (사용자 및 권한(CAM) 전체 읽기/쓰기 액세스 권한 정책) 권한을 부여해야 합니다.
   - 스크린샷 및 음란물 감지 기능을 사용하려면 [QcloudAccessFoLVBRoleInSaveLiveScreenshottoCOS](https://console.cloud.tencent.com/cam/policy/detail/115867019&QcloudAccessFoLVBRoleInSaveLiveScreenshottoCOS&2)를 CSS 서비스 역할과 연결하여 COS에 대한 액세스 권한을 부여히야 합니다.

- **사용자 지정 정책**: 정책 페이지로 이동하여 **사용자 지정 정책 생성**을 클릭한 후 **정책 생성기로 생성**을 선택합니다. 자세한 내용은 [Policy](https://intl.cloud.tencent.com/document/product/598/10601)를 참고하십시오.
>? 현재 CSS의 일부 API는 리소스 수준 권한 부여를 지원합니다.

**작업 예시:** 지정된 도메인 이름의 하위 사용자에게 **DescribeLiveDomains** API를 승인해야 하는 경우 아래 단계에 따라 구성하십시오.
	
1. API에 대한 액세스를 허용하는 도메인 수준 정책을 생성하고 정책 생성기 생성 페이지로 이동하여 다음 설정을 완료합니다.
<table>
<tr><th>구성 항목</th><th>필수 입력 여부</th><th>설명</th></tr>
<tr>
<td>효과</td><td>Yes</td><td>선택 <b>허용</b></td>
</tr><tr>
<td>서비스</td><td>Yes</td><td>선택 <b>CSS</b></td>
</tr><tr>
<td>작업</td><td>Yes</td><td>선택 <b>DescribeLiveDomains</b></td>
</tr><tr>
<td>리소스</td><td>Yes</td>
<td>승인할 모든 리소스 또는 특정 리소스를 선택합니다. <ul style="margin:0"><li>인증 단위가 작업 또는 서비스인 Tencent Cloud 서비스<b>는 6-세그먼트 리소스 설명을 지원하지 않습니다. 이를 위해 모든 리소스를 선택합니다</b>. </li><li>리소스 수준 인증을 지원하는 Tencent Cloud 서비스의 경우 특정 리소스를 선택할 수 있습니다. 리소스 설명 방법은 <a href="https://intl.cloud.tencent.com/document/product/598/10588">CAM-Enabled Products</a>의 해당 CAM 가이드를 참고하십시오. Tencent Cloud 서비스의 인증 단위는 <a href="https://intl.cloud.tencent.com/document/product/598/10588">CAM-Enabled Products</a>를 참고하십시오.</li></ul></td>
</tr><tr>
<td>조건</td><td>No</td>
<td>권한이 적용되는 조건을 설정합니다. IP 주소를 입력하면 요청이 지정된 IP 범위에서 오는 경우에만 API에 액세스할 수 있습니다. 다른 조건을 추가할 수도 있습니다. 자세한 내용은 <a href="www.tencentcloud.com/document/product/598/10608">Conditions</a>를 참고하십시오.</td>
</tr></table>

<img src="https://qcloudimg.tencent-cloud.cn/raw/da4b1d1379c74e8d5eeb3f79908191e6.png">

>! 여러 서비스를 승인하려면 **권한 추가**를 클릭하여 이러한 서비스에 대한 권한 부여 정책을 구성할 수 있습니다.

2. **다음**을 클릭하여 정책을 생성합니다. 그 다음 상기 두 가지 방법 중 하나를 사용하여 사용자/사용자 그룹과 연결합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/c88a7d7181c31262d9ed46ce938361db.png)

### 3단계: 서브 계정 사용
서브 계정 자격(루트 계정에서 생성한 서브 계정 ID 및 비밀번호)을 사용해 권한이 부여된 API 인터페이스를 호출(예: ‘도메인 리스트 조회’ 등)하여 해당하는 CSS 정보(예: 해당 계정의 모든 도메인)를 획득할 수 있습니다.