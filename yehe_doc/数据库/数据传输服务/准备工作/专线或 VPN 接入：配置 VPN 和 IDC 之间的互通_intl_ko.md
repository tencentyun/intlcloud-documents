## 작업 시나리오
액세스 유형이 VPN 게이트웨이인 경우 VPC와 VPN을 생성하고 상호 연결을 위해 VPN과 IDC 사이에 터널을 설정해야 합니다.

이 시나리오에서 VPC는 ‘TomVPC’이고 서브넷은 ‘서브넷 A’이며 ‘서브넷 A’의 IP 대역은 `192.168.1.0/24`입니다. 생성된 VPN 게이트웨이는 ‘TomVPNGW’, VPN 게이트웨이의 공용 IP는 `203.195.147.82`, IDC의 서브넷 IP 대역는 `10.0.1.0/24`, IDC에 있는 VPN 게이트웨이의 공용 IP는 `202.108.22.5`, 원본 데이터베이스 서버의 IP 주소는 `10.0.1.8`입니다.

![](https://qcloudimg.tencent-cloud.cn/raw/86936527e538a841b69bb703ac8a0837.png)

## 작업 단계
[VPC에서 IDC로의 연결 구성](https://intl.cloud.tencent.com/document/product/1037/32689)을 참고하십시오.

## 후속 작업
1. VPN이 IDC에 연결되면 [DTS 작업 페이지](https://console.cloud.tencent.com/dts/migration)에서 **VPN 액세스**를 선택합니다.
<table>
<thead><tr><th><strong>매개변수</strong></th><th><strong>설명</strong></th><th><strong>매개변수 예시</strong></th></tr></thead>
<tbody><tr>
<td>VPN 게이트웨이</td>
<td>VPC에서 생성된 VPN 게이트웨이의 이름입니다.</td>
<td>TomVPNGW</td></tr>
<tr>
<td>VPC</td>
<td>VPC의 이름입니다.</td>
<td>TomVPC</td></tr>
<tr>
<td>서브넷</td>
<td>VPC의 서브넷 이름입니다.</td>
<td>서브넷 A</td></tr>
<tr>
<td>호스트 주소</td>
<td>원본 데이터베이스 서버의 IP 주소입니다.</td>
<td>10.0.1.8</td></tr>
<tr>
<td>포트</td>
<td>원본 데이터베이스에서 사용하는 포트입니다. 다음은 공통 데이터베이스의 기본 포트입니다(수정된 경우 실제 포트 입력).<br><ul><li>MySQL: 3306</li><li>SQL Server: 1433</li><li>PostgreSQL: 5432</li><li>MongoDB: 27017</li><li>Redis: 6379</li></ul></td>
<td>3306</td></tr>
</tbody></table>
2. **연결 테스트**를 클릭합니다. 테스트 실패 시 다음과 같이 문제를 해결하십시오.
   - Telnet 테스트 실패.
     생성된 VPC(이 예시에서는 TomVPC)에서 CVM 인스턴스를 구입하고 여기에서 원본 데이터베이스 서버 주소를 ping합니다.
      - 주소를 ping할 수 없는 경우.
        - [원본 데이터베이스에 보안 그룹 또는 방화벽이 구성되어 있음](https://intl.cloud.tencent.com/document/product/571/42552).
        - [SNAT IP 주소가 원본 데이터베이스에서 차단됨](https://intl.cloud.tencent.com/document/product/571/42552).
        - 원본 데이터베이스의 포트 설정 문제.     
      - 주소가 ping 가능한 경우.
        해결 지원을 위해 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하십시오.
   - Telnet 테스트 통과, Datebase Connect 실패.
     - 마이그레이션 계정 권한 부여 문제. [데이터 마이그레이션](https://intl.cloud.tencent.com/document/product/571/42645) 및 [데이터 동기화](https://intl.cloud.tencent.com/document/product/571/42624)의 해당 시나리오의 지침에 따라 다시 권한을 부여합니다.
     - 계정 또는 비밀번호 오류.
     

 

 
