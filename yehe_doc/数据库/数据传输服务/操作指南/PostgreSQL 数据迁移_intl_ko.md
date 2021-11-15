
## 작업 시나리오
데이터 전송 서비스 DTS는 데이터 마이그레이션 기능을 지원하여 자체구축 PostgreSQL 데이터베이스를 TencentDB의 연속 데이터로 복사할 수 있습니다. 사용자는 무정지 상황에서 데이터를 온라인 핫 마이그레이션을 할 수 있습니다. 공용 네트워크를 보유한 IP/Port 혹은 Tencent Cloud DC의 로컬 IDC, Tencent Cloud CVM의 PostgreSQL 데이터베이스에 마이그레이션할 수 있습니다.

>!현재 데이터 마이그레이션을 지원하는 PostgreSQL 데이터베이스의 버전은 9.3.x와 9.5.x이며, 9.3.x는 증분 동기화를 지원하지 않습니다. 9.5.x는 온라인 [동기화 플러그 인](https://main.qcloudimg.com/raw/97b6b39254c963fcafc228a9c565a2e0.zip) 으로만 지원하며, 상세한 설정은 [동기화 플러그인 설정](#.E5.90.8C.E6.AD.A5.E6.8F.92.E4.BB.B6.E9.85.8D.E7.BD.AE)을 참조하십시오.

## 작업 순서

### DTS 데이터 마이그레이션 작업 생성
[DTS 콘솔](https://console.cloud.tencent.com/dts)에 로그인해 데이터 마이그레이션 페이지에서 [마이그레이션 작업 생성]을 클릭합니다.


### 소스와 타깃 데이터베이스 설정
페이지 리디렉션 후 작업 설정, 소스 라이브러리 설정과 객체 라이브러리 설정 등 정보를 작성합니다.
#### 작업 설정
* 작업 이름: 작업 이름을 지정합니다.
* 예약 실행: 마이그레이션 작업 시작 시간을 지정합니다.

#### 소스 라이브러리와 객체 라이브러리 설정
소스 라이브러리 유형: 지금은 공인 IP의 PostgreSQL, CVM의 자체구축 PostgreSQL, DC Tencent Cloud의 PostgreSQL, VPN 액세스 PostgreSQL, TencentDB for PostgreSQL 5가지 소스 라이브러리 유형이 있습니다.

| 소스 라이브러리 유형 | 설명 |
|---------|---------|
| 공인 IP가 있는 PostgreSQL |  공인 IP로 액세스 할 수 있는 PostgreSQL 데이터베이스. 필요 정보:<br><li>PostgreSQL 호스트 주소<li>PostgreSQL 포트<li>PostgreSQL 계정<li>PostgreSQL 암호 |
| CVM의 자체구축 PostgreSQL |  기본 네트워크와 사설 네트워크, 두 가지 환경을 지원하는 CVM을 기반으로 한 자체구축 PostgreSQL 데이터베이스. 사용 시 지정 CVM의 인스턴스 ID와 네트워크 환경 필요. 필요 정보:<br><li>소속 리전: 현재는 리전 내의 CVM 자체구축 PostgreSQL의 TencentDB 마이그레이션만 지원. CVM과 TencentDB이 다른 리전에 있을 경우 CVM 공용 네트워크를 사용해 [공인 IP가 있는 PostgreSQL] 옵션을 선택해 마이그레이션 <li>CVM 네트워크 구현 가능: 기본 네트워크와 사설 네트워크 지원<li>사설네트워크: 사설 네트워크 선택 시 소속 사설 네트워크 및 서브넷 선택 필요<li>CVM 인스턴스 ID<li>PostgreSQL 포트<li>PostgreSQL 계정<li>PostgreSQL 암호 |
| DC의 PostgreSQL |  로컬 IDC 자체구축 PostgreSQL 사용 [DC](https://intl.cloud.tencent.com/product/dc) Tencent Cloud 연결 후 Tencent Cloud로 DTS 데이터 마이그레이션 사용 가능. 필요 정보:<br><li> 전용 게이트웨이: Tencent Cloud의 데이터베이스 서버 액세스 시 사용하는 전용 게이트웨이, [전용 게이트웨이 알아보기](https://intl.cloud.tencent.com/document/product/216/19256)<li>사설 네트워크: 전용 게이트웨이 소속의 사설 네트워크<li> PostgreSQL호스트 주소: IDC 내의 PostgreSQL 호스트 주소, DTS 데이터 마이그레이션은 전용 게이트웨이 IP 매핑 후 액세스<li>PostgreSQL 포트<li>PostgreSQL 계정<li>PostgreSQL 암호		 |
| VPN 액세스 PostgreSQL |  로컬 IDC 자체구축 PostgreSQL는 [VPN 연결 서비스](https://intl.cloud.tencent.com/product/vpn) 혹은 CVM의 자체구축 VPN 서버 액세스와 Tencent Cloud 연결 후DTS로 Tencent Cloud로 데이터 마이그레이션 가능. 필요 정보:<br><li>소속 리전: 현재는 리전 내의 VPN 서비스만 지원<li>VPN 유형: [클라우드 VPN 서비스](https://intl.cloud.tencent.com/product/vpn) 혹은 CVM의 자체구축 VPN<li>VPN 게이트웨이: [클라우드 VPN 서비스](https://intl.cloud.tencent.com/product/vpn)에만 VPN 게이트웨이 정보 보충 필요, [VPN 알아보기](https://intl.cloud.tencent.com/product/vpn)<li>사설 네트워크: VPN 서비스 소속의 사설 네트워크<li>PostgreSQL 호스트 주소: IDC 내의 PostgreSQL 호스트 주소, DTS 데이터 마이그레이션은 전용 게이트웨이를 통해 IP 매핑 후 액세스<li>PostgreSQL 포트<li>PostgreSQL 계정<li>PostgreSQL 암호		 |
| 클라우드 데이터베이스 PostgreSQL |TencentDB for PostgreSQL 클라우드 데이터베이스 인스턴스. 필요 정보:<br><li>PostgreSQL 인스턴스 ID<li>PostgreSQL 계정<li>PostgreSQL 암호   |

![](https://main.qcloudimg.com/raw/a5c20fabbb3dc7994f33439042226a65.png)

### 마이그레이션이 필요한 데이터베이스 선택
마이그레이션이 필요한 데이터베이스(모두 마이그레이션 샤딩 마이그레이션 선택 가능)를 선택합니다.
![](https://main.qcloudimg.com/raw/ebb6a7e26b857b22957a0295fa5947a5.png)

### 마이그레이션 작업 인증
[다음 단계: 인증 작업]을 클릭해 마이그레이션 작업 정보를 인증합니다. 모든 항목의 인증을 통과해야 마이그레이션 작업을 실행할 수 있습니다. 인증 완료 후 [실행]을 클릭하시면 됩니다.
작업 인증은 3가지 상태가 있습니다.
 - 통과: 인증 통과를 의미합니다.
 - 경고: 인증 미통과를 의미하며, 마이그레이션 과정 혹은 마이그레이션 후 데이터베이스의 정상적인 실행에 영향을 줄 수 있습니다. 하지만 마이그레이션 작업의 실행에는 영향을 주지 않습니다.
 - 실패: 인증에 통과하지 못해 마이그레이션을 진행할 수 없다고 표시됩니다. 인증 실패 시 오류가 발생한 인증 페이지에 따라 마이그레이션 작업 정보를 체크하고 수정한 후 다시 인증하십시오.
![](https://main.qcloudimg.com/raw/234b7900b1d1049204bb42977c5fa2c6.png)

### 마이그레이션 실행
인증 통과 후 데이터 마이그레이션 리스트로 돌아가 [작업] 열에서 [즉시 실행]을 클릭해 데이터 마이그레이션을 시작합니다. 마이그레이션 작업을 예약한 경우, 마이그레이션 작업이 설정된 시간에 정렬되고 시작되니 주의하시기 바랍니다. 작업 시간을 설정하지 않은 경우에는 즉시 마이그레이션 작업이 시작됩니다.
마이그레이션 실행 후에는 마이그레이션 작업에서 해당 작업의 진행 정보를 보실 수 있습니다. 커서를 절차 뒤의 느낌표에 대면 마이그레이션의 필요 과정과 현재 단계가 표시됩니다.

>!시스템 설계의 한계 때문에 1회성 제출 혹은 다수의 마이그레이션 작업을 정렬하는 경우에는 정렬 순서에 따라 순차적으로 실행됩니다.

### 증분 동기화
마이그레이션 작업 생성 시 증량 동기화 옵션은 반드시 선택해야 합니다. 데이터 마이그레이션 완료 후에는 타깃 TencentDB for PostgreSQL 데이터베이스가 원본 데이터베이스의 백업 데이터베이스가 되며, 마스터/슬레이브 동기화로 마이그레이션을 할 시 소스 라이브러리에 추가된 데이터가 타깃 TencentDB for PostgreSQL 데이터베이스에 동기화됩니다. 이 때 소스 라이브러리의 수정 사항은 모두 타깃 TencentDB for PostgreSQL로 동기화됩니다.
마이그레이션 완료 후에는 수동으로 [완료] 버튼을 클릭해야 소스 라이브러리와 객체 라이브러리의 동기화가 종료되고 마이그레이션이 완료됩니다.

>!동기화를 종료하기 전에는 타깃 데이터베이스의 인스턴스에 데이터를 입력할 수 없습니다. 그러지 않을 경우에는 소스 라이브러리와 객체 라이브러리 데이터가 불일치 함으로 인해 데이터 대조에 실패하고, 마이그레이션에 실패할 수 있습니다.

### 마이그레이션 중지
마이그레이션 과정 중 마이그레이션을 정지해야 할 경우에는 마이그레이션 작업의 [작업] 열에서 [취소]를 클릭해 중지하실 수 있습니다.

>!
>- 다시 실행 시 인증에 실패하거나 작업에 실패할 수 있습니다. 수동으로 객체 라이브러리 내에서 충돌이 발생할 수 있는 데이터베이스 혹은 리스트를 삭제해야 마이그레이션 작업을 다시 실행하실 수 있습니다.
>- 단독 리스트를 마이그레이션할 시 반드시 모든 외래 키에 종속된 테이블이 마이그레이션이 되어야 합니다.

### 마이그레이션 완료
![](https://main.qcloudimg.com/raw/1bd1e0106ab6ac0b40765e030dc3b102.png)

## 동기화 플러그 인 설정
1.  [dts_decoding](https://main.qcloudimg.com/raw/97b6b39254c963fcafc228a9c565a2e0.zip) 다운로드 후 PostgreSQL 설치 경로의 lib 목록에 복사합니다.
![](https://main.qcloudimg.com/raw/1fdb249844a331ffb073cf0544ac8c3f.png)
2. 데이터 디렉터리의 postgresql.conf 프로파일을 수정합니다.
```
wal_level >= logical
  max_replication_slots >= 마이그레이션 데이터베이스 수량을 사용할 수 있습니다.
  max_wal_senders       >= 마이그레이션 데이터베이스 수량을 사용할 수 있습니다.
```
![](https://main.qcloudimg.com/raw/1a6819eff953e9d885175f0ff7cdde42.png)
![](https://main.qcloudimg.com/raw/41a8bb56280c4f6e82c9a9025e611b49.png)
3. 데이터 디렉터리의 pg_hba.conf 프로파일을 수정합니다.
 replication 연결을 설정해야 합니다. 
![](https://main.qcloudimg.com/raw/9ea1ec694a672b98f168a81ee7080c6a.png)
4. 원본 인스턴스를 재시작합니다.
>!DB 테이블 기능을 사용할 시, 테이블에 rule을 사용했거나 다른 테이블과 연결이 되어 있을 경우 증분 마이그레이션 데이터 삽입이 실패할 수 있는데, 일부 SQL이 마이그레이션의 지원 기능에 없는 것이 원인입니다. 이런 문제가 발생한 경우 스키마 마이그레이션 기능 혹은 모든 인스턴스 마이그레이션 기능을 사용하시기 바랍니다.





