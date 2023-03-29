본문에서는 요청을 필터링하고 스트리밍 콘텐츠에 대한 액세스를 제어하기 위해 IP 얼로우/블록리스트를 설정하는 방법을 보여줍니다.

## 설정 원리
- IP **얼로우리스트**: 목록에 있는 IP 주소만 스트리밍 콘텐츠에 액세스할 수 있습니다.
- IP **블록리스트**: 목록에 있는 IP 주소는 스트리밍 콘텐츠에 액세스할 수 없습니다.

## 참고 사항
- IP 블록리스트/얼로우리스트 구성이 완료되면 약 5분 후에 적용됩니다.
- IP 블록리스트/얼로우리스트 구성 완료 후, 진행 중인 라이브 스트림을 중지하고 다시 푸시해야만 적용됩니다.

## 전제 조건
- CSS 서비스가 활성화되어 있고 [CSS 콘솔](https://console.cloud.tencent.com/live/livestat)에 로그인되어 있어야 합니다.
- [재생 도메인 이름](https://intl.cloud.tencent.com/document/product/267/35970)을 추가했습니다.

[](id:set)
## IP 얼로우/블록리스트 설정
1. [도메인 관리](https://console.cloud.tencent.com/live/domainmanage)를 선택하고 IP 얼로우리스트/블록리스트를 설정할 대상 **재생 도메인**을 클릭하거나 오른쪽의 **관리**를 클릭하여 도메인 관리 페이지로 이동합니다.
2. **액세스 제어** > **IP 블록리스트 설정**에서 IP 얼로우리스트/블록리스트 설정을 활성화 또는 비활성화할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/de64819fab139753ecde2ee7f20a5f63.png)
3. ![](https://qcloudimg.tencent-cloud.cn/raw/b64d8a4343b3a1e340db3adb9002db60.png)을(를) 클릭하여 IP 얼로우/블록리스트 활성화를 선택하고 다음과 같이 설정합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a9cc1a4e8f9485c9fb057c0edaba177b.png)

<table>
<thead><tr><th>구성 항목</th><th>설명</th></tr></thead>
<tbody><tr>
<td>인증 유형</td>
<td>얼로우리스트 또는 블록리스트: <ul style="margin:0">
<li>얼로우리스트와 블록리스트를 둘 다 선택할 수는 없습니다. </li>
<li>얼로우리스트를 설정하면 목록에 있는 IP 주소만 스트리밍 콘텐츠에 액세스할 수 있습니다.</li>
<li>블록리스트를 설정하면 목록의 IP 주소가 스트리밍 콘텐츠에 액세스할 수 없습니다.</li></ul></td>
</tr><tr>
<td>IP 리스트</td>
<td>최대 200개의 항목을 추가할 수 있습니다. 줄 바꿈으로 구분하십시오.<ul style="margin:0">
<li>IP 주소와 CIDR(/8/16/24)은 지원하지만 포트 번호는 지원하지 않습니다.</li>
<li>IP v6 미지원</li></ul></td>
</tr>
</tbody></table>

4. **저장**을 클릭하여 설정을 저장합니다(설정이 적용되는 데 시간이 걸립니다).
![](https://qcloudimg.tencent-cloud.cn/raw/8a0bf90247475062eef4aa43d34eb08f.png)

[](id:change)
## IP 얼로우/블록리스트 설정 수정
1. [도메인 관리](https://console.cloud.tencent.com/live/domainmanage)를 선택하고 IP 얼로우리스트/블록리스트 설정을 수정할 타깃 **재생 도메인**을 클릭하거나 우측의 **관리**를 클릭하여 도메인 관리 페이지로 이동합니다.
2. **액세스 제어** > **IP 얼로우리스트/블록리스트**에서 **편집**을 클릭합니다.
3. 설정을 수정하고 **저장**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f60c0cdf3fe6cb94f15867f349bc4cc3.png)

[](id:close)
## IP 얼로우/블록리스트 비활성화
IP 얼로우/블록리스트를 비활성화하려면 아래 단계를 따르십시오.
1. [도메인 관리](https://console.cloud.tencent.com/live/domainmanage)를 선택하고 설정할 대상 **재생 도메인**을 클릭하거나 오른쪽의 **관리**를 클릭하여 도메인 관리 페이지로 이동합니다.
2. **액세스 제어> IP 얼로우/블록리스트**에서, ![img](https://main.qcloudimg.com/raw/e72f89a0deb6858428dc3e93ce7e7088.png)을(를) 클릭해 IP 얼로우/블록리스트 비활성화를 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/226d47604696996735ec23b887931d35.png)