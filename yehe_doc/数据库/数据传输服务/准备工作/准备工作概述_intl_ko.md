## 작업 시나리오

마이그레이션, 동기화 또는 구독 작업을 생성할 때 원본 데이터베이스의 배포 조건에 따라 다른 액세스 유형을 선택해야 합니다. 이 문서에서는 액세스 유형을 선택하고 그에 따라 준비하는 방법을 설명합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2cbf69b4ea09960c7c1c6c94ce516bc4.png)

## 준비 작업

<table >
<tr><th width="25%"><strong>적용 시나리오</strong></th><th width="15%"><strong>액세스 유형</strong></th><th width="60%"><strong>작업 가이드</strong></th></tr>
<tr>
<td>원본 데이터베이스는 공용 IP를 통해 액세스 가능</td>
<td>공용 네트워크</td>
<td>DTS 서버의 SNAT IP를 자체 구축 데이터베이스의 얼로우 리스트(일반적으로 방화벽)에 추가하여 원본 데이터베이스와 DTS 마이그레이션 인스턴스를 연결합니다.</td></tr>
<tr>
<td rowspan="2">데이터베이스는 VPN 또는 Direct Connect를 통해 VPC와 상호 연결된 자체 구축 IDC에 있습니다.</td>
<td>DC/VPN 액세스</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/571/42651">VPN과 IDC 간의 상호 연결</a>을 구성합니다.</li>
<li>DTS 서버의 SNAT IP를 자체 구축 데이터베이스의 얼로우 리스트(일반적으로 방화벽)에 추가하여 원본 데이터베이스와 DTS 마이그레이션 인스턴스를 연결합니다.</li></td></tr>
<tr>
<td>CCN</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/571/42650">CCN을 통해 VPC-IDC 상호 연결</a>을 구성합니다.</li>
<li>자체 구축 데이터베이스의 얼로우 리스트(일반적으로 방화벽)에 DTS 서버의 SNAT IP를 추가합니다.</li></td></tr>
<tr>
<td>원본 데이터베이스는 CVM 인스턴스에 배포</td>
<td>자체구축 CVM</td>
<td>이 시나리오에서 DTS는 DTS 서버의 SNAT IP 주소를 CVM 인스턴스의 보안 그룹 규칙에 자동으로 추가하므로 수동으로 추가할 필요가 없습니다.</td></tr>
<tr>
<td>원본 및 타깃 데이터베이스는 모두 Tencent Cloud VPC에 배포</td>
<td>VPC</td>
<td>원본 데이터베이스의 보안 그룹 규칙에 DTS 서버의 SNAT IP 주소를 추가합니다.<br>데이터 동기화 기능은 VPC 액세스 유형을 지원합니다. 이용하시려면 <a href="https://console.cloud.tencent.com/workorder/category">티켓 제출</a>하십시오.</td></tr>
<tr>
<td>원본 데이터베이스는 TencentDB 데이터베이스</td>
<td>데이터베이스</td>
<td>원본 데이터베이스의 보안 그룹 규칙에 DTS 서버의 SNAT IP 주소를 추가합니다.</li></td></tr>
</table>

타사 클라우드 데이터베이스의 경우 **액세스 유형**으로 일반적으로 공용 네트워크를 선택하거나 실제 네트워크 조건에 따라 VPC 액세스, DC 또는 CCN을 선택할 수 있습니다.
