## 작업 시나리오
CCN은 VPC를 다른 VPC 또는 로컬 IDC와 상호 연결할 수 있습니다. CCN 액세스를 사용하려면 미리 CCN을 통해 VPC 간 및 VPC-IDC 상호 연결을 설정해야 합니다.

이 시나리오에서는 CCN을 사용하여 vpc-광저우, vpc-난징 및 vpc-상하이의 세 네트워크를 상호 연결했으며 광저우 리전의 데이터베이스를 대상 데이터베이스로 마이그레이션할 계획입니다. vpc-난징 또는 vpc-상하이가 CCN과 연결된 VPC로 선택됩니다.

<img src="https://qcloudimg.tencent-cloud.cn/raw/e1897064f911913b554bbafcd1cb45be.png" style="zoom:67%;" />

## 작업 단계
[하나의 계정에서 네트워크 인스턴스 상호 연결](https://intl.cloud.tencent.com/document/product/1003/31986)의 지침에 따라 상호 연결을 설정합니다.

> ?CCN은 모든 리전 간에 10Kbps 미만의 대역폭만 무료로 제공합니다. 그러나 DTS에는 더 높은 대역폭이 필요합니다. 따라서 링크에서 대역폭 설정이 필요합니다.

## 후속 작업
1. [DTS 작업 페이지](https://console.cloud.tencent.com/dts/migration)에서 **CCN**을 선택합니다.
<table>
<thead><tr><th><strong>매개변수</strong></th><th><strong>설명</strong></th><th><strong>매개변수 예시</strong></th></tr></thead>
<tbody><tr>
<td>VPC 기반 CCN 인스턴스</td><td>CCN 인스턴스 이름.</td><td>ccn6-xxxx7d</td></tr>
<tr>
<td>CCN 연결 VPC</td>
<td>원본 데이터베이스의 VPC와 이름 및 리전이 다른 VPC를 선택합니다. 예를 들어 광저우 리전의 데이터베이스를 원본 데이터베이스로 사용하는 경우 vpc-난징 또는 vpc-상하이를 CCN 연결 VPC로 선택해야 합니다. 여기에서는 vpc-난징을 선택합니다.</td>
<td>vpc-난징</td></tr>
<tr>
<td>서브넷</td>
<td>선택한 VPC의 서브넷 이름입니다.<br>서브넷을 가져올 수 없으면 계정에 문제가 있을 수 있습니다. ‘CCN 연결 VPC’의 계정은 마이그레이션 계정과 동일해야 합니다.<br>예를 들어, 계정 A의 데이터베이스를 계정 B로 마이그레이션하려면 계정 B를 사용하여 작업을 생성해야 합니다. 따라서 ‘CCN 연결 VPC’는 계정 B에 있어야 합니다.</td>
<td>vpc-난징-서브넷</td></tr>
<tr>
<td>호스트 주소</td><td>원본 데이터베이스 서버의 IP 주소입니다.</td><td>172.16.0.0</td></tr>
<tr>
<td>포트</td>
<td>원본 데이터베이스에서 사용하는 포트입니다. 다음은 공통 데이터베이스의 기본 포트입니다(수정된 경우 실제 포트 입력)<ul><li>MySQL: 3306</li><li>SQL Server: 1433</li><li>PostgreSQL: 5432</li><li>MongoDB: 27017</li><li>Redis: 6379</li></ul></td>
<td>3306</td></tr>
</tbody></table>

2. **연결 테스트**를 클릭합니다. 테스트 실패 시 다음과 같이 문제를 해결하십시오.
   - Telnet 테스트 실패.
     CCN 연결 VPC(이 예에서는 vpc-난징)에서 CVM 인스턴스를 구입하고 여기에서 원본 데이터베이스 서버 주소를 ping합니다.
     - 주소를 ping할 수 없는 경우.
      - [원본 데이터베이스가 있는 서버에 보안 그룹 또는 방화벽이 설정되어 있음](https://intl.cloud.tencent.com/document/product/571/42552).
      - [SNAT IP 주소가 원본 데이터베이스에서 차단됨](https://intl.cloud.tencent.com/document/product/571/42552).
      - 원본 데이터베이스의 포트 설정 오류.
      - CCN 인스턴스 일부 라우팅 테이블의 IP 대역 충돌로 인한 활성화 실패.
     - 주소 ping 가능한 경우 원본 데이터베이스와 CCN 간의 라우팅은 정상입니다.     
      - CCN 연결 VPC 선택 오류.       
         CCN 연결 VPC와 호스트 주소는 동일한 리전에 있을 수 없습니다(원본 데이터베이스의 네트워크 환경이 광저우의 VPC인 경우 광저우의 다른 VPC를 CCN 연결 VPC로 선택할 수 없음). CCN 연결 VPC와 호스트 주소는 동일한 VPC에 있을 수 없습니다(원본 데이터베이스의 네트워크 환경이 VPC-A인 경우 VPC-A를 CCN 연결 VPC로 선택할 수 없음).       
      - 해결 지원을 위해 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하십시오.    
 - Telnet 테스트 통과, Database Connect 실패.
     - 마이그레이션 계정 권한 부여 문제. [데이터 마이그레이션](https://intl.cloud.tencent.com/document/product/571/42645) 및 [데이터 동기화](https://intl.cloud.tencent.com/document/product/571/42624)의 해당 시나리오의 지침에 따라 다시 권한을 부여합니다.
     - 계정 또는 비밀번호 오류.

 

