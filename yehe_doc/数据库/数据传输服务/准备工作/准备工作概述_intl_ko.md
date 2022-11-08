## 작업 시나리오

마이그레이션, 동기화 또는 구독 작업을 생성할 때 원본 데이터베이스의 배포 조건에 따라 다른 액세스 유형을 선택해야 합니다. 이 문서에서는 액세스 유형을 선택하고 그에 따라 준비하는 방법을 설명합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2cbf69b4ea09960c7c1c6c94ce516bc4.png)

## 준비 작업

>!액세스 유형을 미리 결정하십시오. 동일한 원본 및 대상 데이터베이스에 대해 ‘공중망’과 같은 액세스 유형을 선택하고 연결 확인을 통과하면 ‘DC((Direct Connect))’와 같은 다른 액세스 유형으로 전환할 수 없습니다. 그렇지 않으면 연결 확인 중에 오류가 보고됩니다.

- 원본 데이터베이스가 IDC 기반 자체 구축 데이터베이스 또는 타사 클라우드 데이터베이스인 경우 일반적으로 ‘공중망’을 선택할 수 있습니다. 더 높은 전송 성능이 필요한 경우 실제 네트워크 조건에 따라 ‘VPN 액세스’, ‘DC’ 또는 ‘CCN(Cloud Connect Network)’을 선택할 수 있습니다.
- 원본 데이터베이스가 TencentDB 인스턴스인 경우 ‘데이터베이스’를 선택합니다.
- 원본 데이터베이스가 CVM 기반 자체 구축 데이터베이스인 경우 ‘CVM에서 자체 구축’을 선택합니다.


<table >
<thead><tr><th width="15%"><strong>액세스 유형</strong></th><th width="25%"><strong>사용 사례</strong></th><th width="60%"><strong>운영 가이드</strong></th></tr></thead>
<tr>
<td>공용 네트워크</td>
<td><li>원본 데이터베이스는 공중망 IP를 통해 액세스할 수 있습니다.</li><li>공중망 옵션은 전송 대역폭을 보장할 수 없으며 전송 성능 요구 사항이 낮은 시나리오에 적용할 수 있습니다.</li></td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/49651">데이터베이스 얼로우리스트에 DTS IP 주소 추가의 지침에 따라 DTS 서버의 SNAT IP를 자체 구축 데이터베이스의 얼로우리스트에 수동으로 추가하여</a>(일반적으로 방화벽), 원본 데이터베이스와 DTS 인스턴스를 연결합니다.</td></tr>
<tr>
<td>DC/VPN 액세스</td>
<td><ul><li>원본 데이터베이스는 <a href="https://intl.cloud.tencent.com/document/product/1037">VPN 연결</a> 또는 <a href="https://intl.cloud.tencent.com/document/product/216">DC</a>를 통해 VPC와 상호 연결할 수 있습니다. </li><li>DC의 네트워크 대역폭이 보장됩니다.</li></ul></td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/571/42651">VPN과 IDC 간의 상호 연결</a>을 구성합니다.</li>
<li><a href="https://intl.cloud.tencent.com/document/product/571/49651">Adding DTS IP Address to Database Allowlist</a>의 지침에 따라 DTS 서버의 SNAT IP를 자체 구축 데이터베이스의 얼로우리스트에 수동으로 추가하여(일반적으로 방화벽), 원본 데이터베이스와 DTS 인스턴스를 연결합니다.</li></ul></td></tr>
<tr>
<td>CCN</td>
<td>원본 데이터베이스는 <a href="https://intl.cloud.tencent.com/document/product/1003">CCN</a>을 통해 VPC와 상호 연결할 수 있습니다.</td>
<td><ul><li><a href="https://intl.cloud.tencent.com/document/product/571/42650">CCN을 통해 VPC-IDC 상호 연결</a>을 구성합니다.</li>
<li><a href="https://intl.cloud.tencent.com/document/product/571/49651">Adding DTS IP Address to Database Allowlist</a>의 지침에 따라 DTS 서버의 SNAT IP를 자체 구축 데이터베이스의 얼로우리스트(일반적으로 방화벽)에 수동으로 추가합니다.</li></ul></td></tr>
<tr>
<td>자체구축 CVM</td>
<td>원본 데이터베이스는 <a href="https://intl.cloud.tencent.com/document/product/213">CVM 인스턴스</a>에 배포됩니다.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/49651">Adding DTS IP Address to Database Allowlist</a>의 지침에 따라 DTS 서버의 SNAT IP를 CVM 인스턴스의 보안 그룹에 수동으로 추가하여, 원본 데이터베이스와 DTS 인스턴스를 연결합니다.</td></tr>
<tr>
<td>VPC</td>
<td>원본 및 대상 데이터베이스는 모두 Tencent Cloud VPC에 배포됩니다.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/49651">Adding DTS IP Address to Database Allowlist</a>에 설명된 대로 DTS 서버의 SNAT IP 주소를 원본 데이터베이스의 보안 그룹에 수동으로 추가합니다</a>. <br>VPC 액세스 유형을 사용하려면 <a href="https://console.cloud.tencent.com/workorder/category">티켓 제출</a>하여 신청하십시오.</td></tr>
<tr>
<td>데이터베이스</td>
<td>원본 데이터베이스는 TencentDB 인스턴스입니다.</td>
<td><ul><li>원본 데이터베이스가 MySQL, PostgreSQL, TDSQL-C PostgreSQL, TDSQL TDStore, TDSQL PostgreSQL, TDSQL-A PostgreSQL인 경우 DTS는 DTS 서버의 SNAT IP 주소를 원본 데이터베이스의 보안 그룹 규칙에 자동으로 추가합니다. </li><li>다른 데이터베이스 유형의 경우 <a href="https://intl.cloud.tencent.com/document/product/571/49651">Adding DTS IP Address to Database Allowlist</a>에 설명된 대로 수동으로 수행해야 합니다.</li></ul></td></tr>
</table>

> ? 
> - DTS 서버의 SNAT IP 주소를 원본 데이터베이스의 보안 그룹이나 얼로우리스트에 수동 또는 자동으로 추가하면 원본 데이터베이스에 특정 보안 위험이 발생할 수 있습니다. 따라서 이러한 작업을 수행할 때 보안 보호 조치를 강화해야 합니다. 예를 들어, 계정 비밀번호 관리를 표준화하고, API 통신을 위한 인증을 요구하고, 불필요한 IP 범위를 제한할 수 있습니다. 귀하의 DTS 사용은 리스크의 존재를 인정하는 것으로 간주합니다. 높은 보안 요구 사항이 있는 경우 DC, VPN 또는 VPC를 사용하여 액세스하는 것이 좋습니다.
> - DTS 사용 후 보안 그룹 또는 방화벽에서 DTS IP 주소를 즉시 삭제하는 것이 좋습니다.

