내부/공인 네트워크로 MySQL 인스턴스에 액세스할 수 없는 경우, 연결 진단 툴로 내부/공인 네트워크의 액세스 문제를 간편하게 진단할 수 있습니다.

CVM을 통한 MySQL 액세스에 오류가 발생한 경우, MySQL 콘솔에서 제공하는 연결 진단 툴로 내부/공인 네트워크의 연결 관련 문제를 진단할 수 있습니다. 간단한 조작만으로 내부/공인 네트워크의 연결 장애 문제가 해결됩니다.

## 내부 네트워크 연결 진단
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 후, 진단이 필요한 인스턴스를 선택하고 인스턴스 이름을 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. 인스턴스 관리 페이지에서 [연결 진단]>[내부 네트워크 진단] 페이지를 선택합니다.
3. 내부 네트워크 연결 문제 진단 시 [해당 인스턴스에 액세스하는 CVM 추가]를 클릭하여 해당 MySQL에 액세스하는 CVM을 추가해야 합니다.
>?CVM 선택 시 기본적으로 리전 내 CVM만 제공됩니다. 리전 간 액세스가 필요한 경우 [CCN](https://intl.cloud.tencent.com/document/product/1003)을 통해 네트워크 통신을 구현하십시오.
>
4. 추가 완료 후 [진단 시작]을 클릭합니다. 작업이 완료되면 진단 보고서가 생성됩니다.
![](https://main.qcloudimg.com/raw/e233a1cd63718cfdc31347da83153fd8.png)

5. 진단 보고서의 '상태' 열에서 [보고서 조회]를 클릭하면 진단 결과를 조회할 수 있습니다.
 - 진단 상태가 [정상]인 경우, CVM에서 내부 네트워크를 통해 해당 MySQL 인스턴스에 정상적으로 액세스할 수 있음을 의미합니다.
 - 진단 상태가 [오류]인 경우, CVM에서 내부 네트워크를 통해 해당 MySQL 인스턴스에 정상적으로 액세스할 수 없음을 의미합니다. 권장 처리 방법을 참조하여 변경한 후 다시 연결하시기 바랍니다.
<table>
<thead><tr><th>진단 항목</th><th>오류 및 처리 방법</th></tr></thead>
<tbody><tr>
<td>MySQL 인스턴스 상태</td>
<td>MySQL 인스턴스가 폐기되었습니다. 폐기를 원하지 않는 경우 <a href="https://console.cloud.tencent.com/mysql/recycle">휴지통</a>에서 복구할 수 있습니다.</td></tr>
<tr>
<td rowspan=2>CVM 인스턴스 상태</td>
<td>CVM 인스턴스가 폐기되었습니다. 폐기를 원하지 않는 경우 <a href="https://console.cloud.tencent.com/cvm/recycler/cvm">휴지통</a>에서 복구할 수 있습니다.</td></tr>
<tr>
<td>CVM 인스턴스가 비활성화되어 있습니다. 해당 CVM 인스턴스를 계속 사용해야 할 경우 <a href="https://console.cloud.tencent.com/cvm/instance">콘솔</a>에서 해당 CVM 인스턴스를 활성화하십시오.</td></tr>
<tr>
<td rowspan=2>CVM과 MySQL이 위치하는 VPC</td>
<td>CVM과 MySQL의 네트워크 유형이 다릅니다. CVM은 MySQL과 네트워크 유형이 동일해야 합니다. <a href="https://intl.cloud.tencent.com/document/product/236/37864">네트워크 문제</a>를 참조하여 네트워크 유형을 수정하십시오.</td></tr>
<tr>
<td>CVM과 MySQL의 VPC IP 대역이 다릅니다. CVM은 MySQL과 동일한 리전의 동일한 VPC에 있어야 합니다. <a href="https://intl.cloud.tencent.com/document/product/236/37864#wlwt">네트워크 문제</a>를 참조하여 VPC를 수정하십시오.</td></tr>
<tr>
<td>CVM 보안 그룹 정책</td>
<td>CVM에 바인딩된 보안 그룹의 <strong>아웃바운드 규칙</strong>이 IP 포트를 개방하지 않았습니다. <a href="https://intl.cloud.tencent.com/document/product/236/37864#caqzpzyw">CVM 보안 그룹 설정 오류</a>를 참조하여 아웃바운드 규칙을 개방하십시오.</td></tr>
<tr>
<td>MySQL 보안 그룹 정책</td>
<td>MySQL 인스턴스에 바인딩된 보안 그룹의 <strong>인바운드 규칙</strong>이 IP 포트를 개방하지 않았습니다. <a href="https://intl.cloud.tencent.com/document/product/236/37864#maqzpzyw">MySQL 보안 그룹 설정 오류</a>를 참조하여 인바운드 규칙을 개방하십시오.</td></tr>
</tbody></table>
<img src="https://main.qcloudimg.com/raw/b183b27af9c6b5a28cdb708f8a5c44d8.png">

## 공인 네트워크 연결 진단
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 후, 진단이 필요한 인스턴스를 선택하고 인스턴스 이름을 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. 인스턴스 관리 페이지에서 [연결 진단]>[공인 네트워크 진단] 페이지를 선택합니다.
2. 공인 네트워크 연결 문제를 진단하려면 [해당 인스턴스에 액세스하는 공인 네트워크 서버 추가]를 클릭해 해당 MySQL 인스턴스에 액세스할 공인 네트워크 서버를 추가해야 합니다.
3. 추가 완료 후 [진단 시작]을 클릭합니다. 작업이 완료되면 진단 보고서가 생성됩니다.
![](https://main.qcloudimg.com/raw/43d9e61c2052797740e7ef6817251f5e.png)
4. 진단 보고서의 '상태' 열에서 [보고서 조회]를 클릭하면 진단 결과를 조회할 수 있습니다.
 - 진단 상태가 [정상]인 경우, 공인 네트워크 서버에서 공인 네트워크를 통해 해당 MySQL 인스턴스에 정상적으로 액세스할 수 있음을 의미합니다.
 - 진단 상태가 [오류]인 경우, 공인 네트워크 서버에서 공인 네트워크를 통해 해당 MySQL 인스턴스에 정상적으로 액세스할 수 없음을 의미합니다. 권장 처리 방법을 참조하여 변경한 후 다시 연결하시기 바랍니다.
<table>
<thead><tr><th>진단 항목</th><th>오류 및 처리 방법</th></tr></thead>
<tbody><tr>
<td>MySQL 인스턴스 상태</td><td>MySQL 인스턴스가 폐기되었습니다. 폐기를 원하지 않는 경우 <a href="https://console.cloud.tencent.com/mysql/recycle">휴지통</a>에서 복구할 수 있습니다.</td></tr>
<tr>
<td>공인 네트워크 활성화 상태</td>
<td>MySQL 인스턴스에 공인 네트워크가 활성화되어 있지 않습니다. <a href="https://intl.cloud.tencent.com/document/product/236/37788">공인 네트워크 활성화</a>를 참조하십시오.</td></tr>
</tbody></table>
<img src="https://main.qcloudimg.com/raw/01998fb06fe6d8a762dd5a2a9a5eb26c.png">
