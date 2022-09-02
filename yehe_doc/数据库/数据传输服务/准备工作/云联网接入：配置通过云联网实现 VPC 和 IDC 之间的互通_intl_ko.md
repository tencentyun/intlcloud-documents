## 작업 시나리오
CCN은 VPC를 다른 VPC 또는 로컬 IDC와 상호 연결할 수 있습니다. CCN 액세스를 사용하려면 미리 CCN을 통해 VPC 간 및 VPC-IDC 상호 연결을 설정해야 합니다.

본 시나리오에서는 CCN을 통해 VPC-광저우, VPC-청두, VPC-상하이 3개의 네트워크 간의 인터랙션을 구축하였으며, 사용자가 데이터베이스를 광저우에 자체 구축하여 원본 데이터베이스(광저우 리전)를 리전 타깃 데이터베이스(난징 리전)로 마이그레이션할 계획이며, ‘VPC-청두’를 ‘액세스 VPC’로 선택하였습니다.

## 구성 원칙

CCN 액세스 방식을 선택할 경우 원본 데이터베이스는 CCN을 통해 DTS 마이그레이션/동기화 링크의 원본과 연결되어야 하며, 연결 경로는 원본 데이터베이스 > VPC 액세스 > 마이그레이션/동기화 링크의 원본으로, 이미지의 주황색 부분에 해당합니다.

<img src="https://qcloudimg.tencent-cloud.cn/raw/731aafbd4595e86f9a59ba173f0e4662.jpg" style="zoom:67%;" />

전체 DTS 작업에서 VPC 액세스, 마이그레이션/동기화 링크 원본 데이터베이스의 네트워크 연결 원칙은 다음과 같습니다.

- 마이그레이션/동기화 링크의 원본 데이터베이스는 아래 이미지와 같이 작업 구매 시 선택한 원본 데이터 리전 네트워크입니다.
   구매 시 선택한 원본 데이터베이스 리전은 액세스 VPC 리전과 동일해야 하며, 그렇지 않으면 네트워크가 상호 통신할 수 없습니다. 동일하지 않은 경우, DTS는 구매 작업에서 선택한 원본 데이터베이스 리전을 액세스 VPC 리전으로 변경합니다.
  <img src="https://qcloudimg.tencent-cloud.cn/raw/be0a5f791aa2c827a7936d01bd48cc5f.png" style="zoom:50%;" />

- 액세스 VPC: 액세스 VPC는 CCN에서 마이그레이션/동기화 링크에 연결된 VPC를 말하며, 아래 이미지와 같이 원본 및 타깃 데이터베이스를 설정하는 단계에서 구성됩니다.
   액세스 VPC와 원본 데이터베이스가 속한 VPC는 CCN을 통해 연결되어 상호 통신할 수 있습니다.


## 작업 단계
[Connecting Network Instances Under the Same Account](https://intl.cloud.tencent.com/document/product/1003/31986)의 지침에 따라 상호 연결을 설정합니다.

> ?CCN은 모든 리전 간에 10Kbps 미만의 대역폭만 무료로 제공합니다. 그러나 DTS에는 더 높은 대역폭이 필요합니다. 따라서 링크에서 대역폭 설정이 필요합니다.

## 후속 작업
1. 사용자는 [데이터 마이그레이션 작업](https://intl.cloud.tencent.com/document/product/571/42645) 또는 [데이터 동기화 작업](https://intl.cloud.tencent.com/document/product/571/47344)에서 관련 매개변수를 구성해야 합니다. 본문은 MySQL 데이터 마이그레이션을 예로 듭니다. 데이터 마이그레이션 작업의 **원본 및 타깃 데이터베이스 설정** 단계에서 **CCN**을 선택하며 주요 매개변수 구성 설명은 다음과 같습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/30832fef580f406d0e19b6e0329724e6.png" style="zoom:50%;" />
<table>
<thead><tr><th><strong>매개변수</strong></th><th><strong>설명</strong></th><th><strong>매개변수 예시</strong></th></tr></thead>
<tbody>
<tr>
<td>호스트 주소</td><td>원본 데이터베이스 서버의 IP 주소입니다.</td><td>172.16.0.0</td></tr>
<tr>
<td>포트</td>
<td>원본 데이터베이스에서 사용하는 포트입니다. 다음은 공통 데이터베이스의 기본 포트입니다(수정된 경우 실제 포트 입력)<ul><li>MySQL: 3306</li><li>SQL Server: 1433</li><li>PostgreSQL: 5432</li><li>MongoDB: 27017</li><li>Redis: 6379</li></ul></td>
<td>3306</td></tr>
<tr>
<td>VPC 기반 CCN 인스턴스</td><td>CCN 인스턴스 이름.</td><td>ccn6-xxxx7d</td></tr>
<tr>
<td>액세스 VPC</td>
<td>액세스 VPC는 클라우드 네트워크의 마이그레이션/동기화 링크에 연결된 VPC를 의미합니다. CCN과 연결된 모든 VPC에서 원본 데이터베이스가 속한 VPC가 아닌 다른 VPC를 선택합니다. <br>예를 들어, 광저우 리전 데이터베이스를 원본 데이터베이스로 할 경우 청두 VPC 또는 상하이 VPC를 선택하여 VPC에 액세스합니다. 여기에선 청두 VPC를 선택합니다.</td>
<td>VPC-청두</td></tr>
<tr>
<td>서브넷</td>
<td>선택한 VPC의 서브넷 이름입니다.<br>서브넷을 가져올 수 없으면 계정에 문제가 있을 수 있습니다. ‘액세스 VPC’의 계정은 마이그레이션 계정과 동일해야 합니다.<br>예를 들어, 계정 A의 데이터베이스를 계정 B로 마이그레이션하려면 계정 B를 사용하여 작업을 생성해야 합니다. 따라서 ‘액세스 VPC’는 계정 B에 있어야 합니다.</td>
<td>VPC-청두-서브넷</td></tr>
<tr>
<td>액세스 VPC 리전</td><td>구매 작업 시 선택한 원본 데이터베이스 리전과 액세스 VPC 리전이 일치해야 하며 일치하지 않을 경우 DTS는 구매 작업 중 선택한 원본 데이터베이스 리전을 액세스 VPC 리전으로 변경합니다. </td><td>청두</td></tr>
</tbody></table>
2. **연결 테스트**를 클릭합니다. 테스트 실패 시 다음과 같이 문제를 해결하십시오.
   - Telnet 테스트 실패.
     CCN 연결 VPC(이 예에서는 vpc-청두)에서 CVM 인스턴스를 구입하고 여기에서 원본 데이터베이스 서버 주소를 ping합니다.
     - 주소를 ping할 수 없는 경우.
      - [원본 데이터베이스의 네트워크 또는 서버에 구성된 보안 그룹 또는 방화벽](https://intl.cloud.tencent.com/document/product/571/42552).
      - [SNAT IP 주소가 원본 데이터베이스에서 차단됨](https://intl.cloud.tencent.com/document/product/571/42552).
      - 원본 데이터베이스의 포트 설정 오류.
      - CCN 인스턴스 일부 라우팅 테이블의 IP 대역 충돌로 인한 활성화 실패.
     - 주소 ping 가능한 경우 원본 데이터베이스와 CCN 간의 라우팅은 정상입니다.     
      - CCN 연결 VPC 선택 오류.       
         CCN 연결 VPC와 호스트 주소는 동일한 리전에 있을 수 없습니다(원본 데이터베이스의 네트워크 환경이 광저우의 VPC인 경우 광저우의 다른 VPC를 CCN 연결 VPC로 선택할 수 없음). CCN 연결 VPC와 호스트 주소는 동일한 VPC에 있을 수 없습니다(원본 데이터베이스의 네트워크 환경이 VPC-A인 경우 VPC-A를 CCN 연결 VPC로 선택할 수 없음).       
      -  해결 지원을 위해 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하십시오.    
 - Telnet 테스트 통과, Database Connect 실패.
     - 마이그레이션 계정 권한 부여 문제. [데이터 마이그레이션](https://intl.cloud.tencent.com/document/product/571/42645) 및 [데이터 동기화](https://intl.cloud.tencent.com/document/product/571/47344)의 해당 시나리오의 지침에 따라 다시 권한을 부여합니다.
     - 계정 또는 비밀번호 오류.

 

