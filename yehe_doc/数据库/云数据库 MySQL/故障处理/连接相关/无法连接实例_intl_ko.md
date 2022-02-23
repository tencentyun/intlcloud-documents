
## 현상 설명
- [현상1](id:xz1): CVM에서 TencentDB for MySQL에 로그인 시 연결 실패
- [현상2](id:xz2): 로컬 PC에서 TencentDB for MySQL에 로그인 시 연결 실패
- [현상3](id:xz3): 데이터베이스 관리 DMC 플랫폼에서 TencentDB for MySQL에 로그인 시 연결에 실패합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6fd9149e439cab91ff45bb8f9192ec66.png)

## 예상 원인
<table>
<thead><tr><th width=15%>예상 원인</th><th width=35%>설명</th><th width=15%>예상 원인</th><th width=35%>설명</th></tr></thead>
<tbody><tr>
<td><a href="#cvmj">네트워크 문제1</a></td><td>CVM은 VPC를 사용하고, MySQL은 기본 네트워크를 사용한 경우</td>
<td><a href="#sjkzhzjpzyw">계정이 권한을 부여한 호스트 주소 문제</a></td><td>액세스하는 호스트 주소를 데이터베이스 계정이 제한한 경우</td></tr>
<tr>
<td><a href="#cjmv">네트워크 문제2</a></td><td>CVM은 기본 네트워크를 사용하고, MySQL은 VPC를 사용한 경우</td>
<td><a href="#ljyfwt">연결 구문 문제</a></td><td>연결 명령어에 오류가 있는 경우</td></tr>
<tr>
<td><a href="#cmvbt">네트워크 문제3</a></td><td>CVM과 MySQL이 동일한 리전에 있지만 서로 다른 VPC 네트워크에 속해 있는 경우</td>
<td><a href="#idyw">IP 및 포트 문제</a></td><td>명령 라인 또는 구성 파일의 IP 및 포트에 오류가 있는 경우</td></tr>
<tr>
<td><a href="#dywt">네트워크 문제4</a></td><td>CVM과 MySQL이 서로 다른 리전에 있고, 서로 다른 VPC 네트워크에 속해 있는 경우</td>
<td>MySQL 인스턴스 상태</td><td>MySQL 인스턴스가 격리 중인 경우 <a href="https://console.cloud.tencent.com/mysql/recycle">휴지통</a>에서 복구 가능</td></tr>
<tr>
<td><a href="#caqzpzyw">보안 그룹 설정 문제</a></td><td>CVM 보안 그룹 설정에 오류가 있는 경우</td>
<td>CVM 인스턴스 상태</td><td>CVM 인스턴스가 격리 중이거나 비활성화된 경우 <a href="https://console.cloud.tencent.com/cvm/instance">콘솔</a>에서 복구 가능</td></tr>
<tr>
<td><a href="#maqzpzyw">보안 그룹 설정 문제</a></td><td>MySQL 보안 그룹 설정에 오류가 있는 경우</td>
<td>외부 네트워크 활성화 상태</td><td>MySQL 인스턴스에 외부 네트워크가 활성화되어 있지 않은 경우 <a href="https://intl.cloud.tencent.com/document/product/236/37788">외부 네트워크 활성화</a> 참고</td></tr>
</tbody></table>

## 해결 방법
### [현상1, 2](#xz1) 해결 방법
1. **진단 툴로 원인 진단**
TencentDB for MySQL 콘솔에서 [원클릭 연결 진단 툴](#step1)을 제공합니다. 연결에 실패하는 원인을 진단하고 안내에 따라 수정 후 다시 인스턴스에 연결합니다.
2. **원인 자가 진단**
원클릭 연결 진단 툴로 문제의 원인을 알 수 없는 경우 [아래에서 설명하는 실패 원인을 통해 자체적으로 실패 원인을 파악할 수 있습니다](#step2).

### [현상3](#xz3) 해결 방법
1. 로그인 계정의 호스트 제한에서 해당 리전 데이터베이스 관리 콘솔 서버의 모든 IP 권한을 확인합니다. 권한 부여에 대한 자세한 내용은 [액세스 권한이 있는 호스트 주소 수정](https://intl.cloud.tencent.com/document/product/236/31903)을 참고바랍니다. 직접 %를 사용하여 모든 IP를 개방할 수 있으며, 보안 그룹으로만 데이터베이스 액세스 출처를 제한할 수 있습니다.
2. IP에 권한이 부여되어 있다면 계정 비밀번호 오류일 수 있습니다. 정확한 비밀번호를 다시 입력하거나, [비밀번호 재설정](https://intl.cloud.tencent.com/document/product/236/31901) 또는 [필요한 권한이 부여된 임시 계정 생성](https://intl.cloud.tencent.com/document/product/236/31900)을 진행할 수 있습니다.

## 해결 단계
### 현상1, 2: CVM, 로컬 연결 실패 시 처리 방법
#### [1단계: 원클릭 연결 진단 툴을 통한 원인 파악 및 처리](id:step1)
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 후, 진단이 필요한 인스턴스를 선택하고, 인스턴스ID를 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. 인스턴스 관리 페이지에서 **연결 진단** > **내부 네트워크 진단** 또는 **공용 네트워크 진단** 페이지를 선택합니다.
>?내부/외부 네트워크 주소 여부는 인스턴스 상세 페이지의 기본 정보에서 확인할 수 있습니다.
3. 해당 MySQL 인스턴스에 액세스할 CVM 또는 공용 네트워크 서버를 추가합니다.
 - 내부 네트워크 진단: 해당 MySQL 인스턴스에 액세스할 CVM을 추가합니다.
 - 공용 네트워크 진단: 해당 MySQL 인스턴스에 액세스할 공용 네트워크 서버를 추가합니다.
4. 추가 완료 후 **진단 시작**을 클릭합니다. 작업이 완료되면 진단 보고서가 생성됩니다.
5. 진단 보고서에 따라 문제를 파악하고, 권장 처리 방법에 따라 변경한 뒤 MySQL을 다시 연결합니다.
   - 내부 네트워크 진단의 진단 항목 및 권장 처리 방법은 다음과 같습니다.
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
<td rowspan=2>CVM과 MySQL이 동일한 VPC에 위치</td>
<td>CVM과 MySQL의 네트워크 유형이 다릅니다. CVM은 MySQL과 네트워크 유형이 동일해야 합니다. <a href="#wlwt">네트워크 문제</a>를 참고하여 네트워크 유형을 수정하십시오.</td></tr>
<tr>
<td>CVM과 MySQL의 VPC IP 대역이 다릅니다. CVM은 MySQL과 동일한 리전의 동일한 VPC에 있어야 합니다. <a href="#wlwt">네트워크 문제</a>를 참고하여 VPC를 수정하십시오.</td></tr>
<tr>
<td>CVM 보안 그룹 정책</td>
<td>CVM에 바인딩된 보안 그룹의 <strong>아웃바운드 규칙</strong>이 IP 포트에 대한 액세스를 개방하지 않았습니다. <a href="#caqzpzyw">CVM 보안 그룹 설정 오류</a>를 참고하여 아웃바운드 규칙을 개방하십시오.</td></tr>
<tr>
<td>MySQL 보안 그룹 정책</td>
<td>MySQL 인스턴스에 바인딩된 보안 그룹의 <strong>인바운드 규칙</strong>이 IP 포트에 대한 액세스를 개방하지 않았습니다. <a href="#maqzpzyw">MySQL 보안 그룹 설정 오류</a>를 참고하여 인바운드 규칙을 개방하십시오.</td></tr>
</tbody></table>
<img src="https://qcloudimg.tencent-cloud.cn/raw/9af6e13c4dea0f77e49c9192026a0846.png">

   - 외부 네트워크 진단의 진단 항목 및 권장 처리 방법은 다음과 같습니다.
<table>
<thead><tr><th>진단 항목</th><th>오류 및 처리 방법</th></tr></thead>
<tbody><tr>
<td>MySQL 인스턴스 상태</td><td>MySQL 인스턴스가 폐기되었습니다. 폐기를 원하지 않는 경우 <a href="https://console.cloud.tencent.com/mysql/recycle">휴지통</a>에서 복구할 수 있습니다.</td></tr>
<tr>
<td>외부 네트워크 활성화 상태</td>
<td>MySQL 인스턴스에 외부 네트워크가 활성화되어 있지 않습니다. <a href="https://intl.cloud.tencent.com/document/product/236/37788">외부 네트워크 활성화</a>를 참고하시기 바랍니다.</td></tr>
</tbody></table>
<img src="https://qcloudimg.tencent-cloud.cn/raw/def8a3aa846e5ef72efd4d27adc06fe0.png">

#### [2단계: 툴 진단으로 문제를 해결하지 못한 경우 참고할 수 있는 원인](id:step2)
[**비밀번호 오류**](id:mmwt)
연결 시 사용하는 비밀번호 오류일 수 있습니다. [비밀번호 재설정](https://intl.cloud.tencent.com/document/product/236/31901) 또는 [필요한 권한이 부여된 임시 계정 생성](https://intl.cloud.tencent.com/document/product/236/31900)을 진행하여 데이터베이스에 로그인하십시오.

[**연결 구문 오류**](id:ljyfwt)
연결 명령어에 오류가 없는지 확인합니다. 표준 연결 명령어를 참고하십시오(내부 네트워크 연결: `mysql -h hostname -u username -p`, 공용 네트워크 연결: `mysql -h hostname -P port -u username -p`). 자세한 순서는 [MySQL 인스턴스 연결](https://intl.cloud.tencent.com/document/product/236/37788)을 참고하십시오.

[**명령 라인 또는 구성 파일의 IP 및 포트 오류**](id:idyw)
[MySQL 콘솔](https://console.cloud.tencent.com/cdb)에서 인스턴스의 IP 포트 및 명령 라인, 구성 파일 정보의 일치 여부를 확인합니다.

[**계정 권한 설정 오류**](id:sjkzhzjpzyw)
데이터베이스 계정은 보안 그룹, 서브넷 등 네트워크 환경 제한 이외에도 MySQL 자체 계정 시스템의 제한을 받습니다. 데이터베이스 계정이 특정 호스트 주소를 지정했다면 다른 주소로는 MySQL에 연결할 수 없습니다.
MySQL 콘솔에서 데이터베이스 계정이 권한을 부여한 호스트 주소를 수정하여 데이터베이스에 대한 연결을 제한하고 연결 보안을 강화할 수 있습니다.
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 후, 인스턴스 리스트에서 인스턴스 ID를 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. **데이터베이스 관리** > **계정 관리** 탭을 선택하고 호스트를 수정해야 하는 계정을 찾은 다음 **작업** 열에서 **더보기** > **호스트 수정**을 선택합니다.
3. 팝업 창에서 새로운 호스트 주소를 입력하고 **확인**을 클릭하면 계정이 권한을 부여한 호스트 주소가 즉시 수정됩니다.
>?호스트 주소는 IP 형식의 주소를 지원하며, %(IP 범위를 제한하지 않음을 의미)값의 입력도 지원합니다. 여러 호스트는 세퍼레이터로 구분하며, 세퍼레이터, 줄 바꿈 부호, 스페이스 및 '; , |' 를 지원합니다.
>- 예시1: %는 IP 범위를 제한하지 않으며, 모든 IP 주소의 클라이언트가 해당 계정으로 데이터베이스에 연결할 수 있음을 의미합니다.
>- 예시2: 10.5.10.%는 IP 범위 10.5.10.% 이내의 클라이언트만 해당 계정으로 데이터베이스에 연결할 수 있음을 의미합니다.

### [현상3: 데이터베이스 관리 콘솔 플랫폼 로그인 실패 처리 방법](id:dptdlsbclff)
1. 로그인 계정의 호스트 제한에서 해당 리전 데이터베이스 관리 콘솔 서버의 모든 IP 권한을 확인합니다. 권한 부여에 대한 자세한 내용은 [액세스 권한이 있는 호스트 주소 수정](https://intl.cloud.tencent.com/document/product/236/31903)을 참고하십시오. 또한 직접 %를 사용하여 모든 IP를 개방할 수 있으며, 보안 그룹으로만 데이터베이스 액세스 출처를 제한할 수 있습니다.
2. IP에 권한이 부여되어 있다면 계정 비밀번호 오류일 수 있습니다. 정확한 비밀번호를 다시 입력하거나, [비밀번호 재설정](https://intl.cloud.tencent.com/document/product/236/31901) 또는 [필요한 권한이 부여된 임시 계정 생성](https://intl.cloud.tencent.com/document/product/236/31900)을 진행할 수 있습니다.

## 부록1
### [네트워크 문제 솔루션](id:wlwt)
CVM과 MySQL의 네트워크 유형이 다른 경우, CVM은 내부 네트워크를 통해 MySQL에 직접 연결할 수 없습니다.

#### [CVM은 VPC를 사용하고, MySQL은 기본 네트워크를 사용한 경우](id:cvmj)
- **솔루션1(권장)**: MySQL을 기본 네트워크에서 VPC로 전환합니다. 자세한 내용은 [네트워크 변경](https://intl.cloud.tencent.com/document/product/236/31915)을 참고하십시오.
>!
>- 변경한 후에는 두 인스턴스 모두 동일한 VPC 네트워크에 있어야만 내부 네트워크로 통신할 수 있습니다.
>- 기본 네트워크를 VPC 네트워크로 변경한 후에는 다시 되돌릴 수 없습니다.
>- 네트워크를 전환하면 해당 인스턴스의 내부 IP가 변경될 수 있습니다. 기존 IP 주소의 회수 시간이 지나면 기존 액세스 IP는 유효하지 않습니다. 클라이언트 프로그램을 즉시 변경하시기 바랍니다.
>  기존 IP 주소의 보관 시간은 기본 24시간이며, 최대 168시간까지 지원됩니다. 기존 IP 주소의 회수 시간을 0시간으로 설정하면 네트워크 전환 후 기존 IP 주소가 즉시 회수됩니다.
>- 기본 네트워크를 VPC로 전환한 후에는 되돌릴 수 없으며, CDB를 VPC로 전환한 후에는 다른 VPC 및 기본 네트워크의 클라우드 서비스와 통신할 수 없습니다.
>- 전환된 CDB가 마스터 인스턴스이고 읽기 전용 인스턴스 또는 재해 복구 인스턴스가 마운트되어 있는 경우, 마스터 인스턴스에서 네트워크를 전환하더라도 마운트되어 있는 읽기 전용 인스턴스 또는 재해 복구 인스턴스의 네트워크는 자동 전환되지 않습니다. 수동 전환이 필요합니다.
- **솔루션2**: 기본 네트워크의 CVM을 재구매합니다(CVM은 VPC에서 기본 네트워크로의 마이그레이션을 지원하지 않음). 기본 네트워크보다 안전한 VPC 사용을 권장합니다.
- **솔루션3**: CVM에서 MySQL의 공용 네트워크 연결 주소를 사용하여 MySQL에 연결합니다. 해당 방식은 성능, 보안성, 안정성이 떨어지므로 VPC 사용을 권장합니다.

#### [CVM은 기본 네트워크를 사용하고, MySQL은 VPC를 사용한 경우](id:cjmv)
- **솔루션1(권장)**: CVM을 기본 네트워크에서 VPC로 전환합니다. 자세한 내용은 [VPC 전환 서비스](https://intl.cloud.tencent.com/document/product/213/20278)를 참고하십시오.
>!  
>- 변경한 후에는 두 인스턴스 모두 동일한 VPC 네트워크에 있어야만 내부 네트워크로 통신할 수 있습니다.
>- 마이그레이션하기 전에 내부/외부 네트워크의 CLB 및 ENI를 바인딩 해제하고, 주 ENI의 보조 IP를 릴리스한 다음 마이그레이션 후 다시 바인딩하시기 바랍니다.
>- 마이그레이션 과정 중 인스턴스를 재시작해야 하므로 다른 작업은 진행하지 마시길 바랍니다.
>- 마이그레이션 후 인스턴스의 실행 상태, 내부 네트워크 연결 및 원격 로그인이 정상적으로 작동하는지 확인합니다.
>- 기본 네트워크를 VPC 네트워크로 변경한 후에는 다시 되돌릴 수 없으며, CVM을 VPC 네트워크로 변경한 후에는 다른 기본 네트워크의 클라우드 서비스와 통신할 수 없습니다.
- **솔루션2**: [클래식 네트워크 사용하기] (https://intl.cloud.tencent.com/document/product/215/31807).
- **솔루션3**: CVM에서 MySQL의 공용 네트워크 연결 주소를 사용하여 MySQL에 연결합니다. 해당 방식은 성능, 보안성, 안정성이 떨어지므로 VPC 사용을 권장합니다.

#### [CVM과 MySQL이 동일한 리전에 있지만 서로 다른 VPC에 속해 있는 경우](id:cmvbt)
기본적으로 CVM과 MySQL의 네트워크 유형이 모두 VPC이고, 둘 다 동일 VPC에 있어야만 내부 네트워크로 통신할 수 있습니다. 동일한 리전에 있지만 VPC가 다를 경우 다음 방법으로 문제를 해결할 수 있습니다.
- **솔루션1(권장)**: MySQL을 CVM이 있는 VPC로 마이그레이션합니다. 자세한 내용은 [네트워크 변경](https://intl.cloud.tencent.com/document/product/236/31915)을 참고하십시오.
- **솔루션2**: 두 VPC 사이에 [CCN](https://intl.cloud.tencent.com/document/product/1003)을 구축합니다.
  위의 솔루션을 사용하지 않는다면, 서로 다른 VPC 네트워크에 있는 CVM과 MySQL은 공용 네트워크를 통해서만 통신할 수 있습니다. 이런 방식은 성능, 보안성 및 안정성이 떨어집니다.

#### [CVM과 MySQL이 동일한 리전에 있지 않고 서로 다른 VPC에 속한 경우](id:dywt)
CVM과 MySQL이 동일한 리전에 있지 않고 서로 다른 VPC에 속한 경우, CVM은 내부 네트워크를 통해 MySQL에 직접 연결할 수 없습니다.
- **솔루션1(권장)**: MySQL과 동일 VPC의 CVM으로 연결을 진행합니다.
- **솔루션2**: 두 VPC 사이에 [CCN](https://intl.cloud.tencent.com/document/product/1003)을 구축합니다.
- **솔루션3**: CVM에서 MySQL의 공용 네트워크 연결 주소를 사용하여 MySQL에 연결합니다. 해당 방식은 성능, 보안성, 안정성이 떨어지므로 VPC 사용을 권장합니다.

### [보안 그룹 설정 문제 솔루션](id:aqzpzwt)
CVM 및 MySQL의 보안 그룹 설정에 오류가 있는 경우 CVM은 내부 또는 외부 네트워크를 통해 MySQL에 직접 연결할 수 없습니다.

#### [CVM 보안 그룹 설정 오류](id:caqzpzyw)
CVM을 사용해 MySQL에 연결하려면 CVM의 보안 그룹에 아웃바운드 규칙을 설정해야 합니다. **아웃바운드 규칙의 타깃 설정이 0.0.0.0/0이 아니고 프로토콜 포트가 ALL이 아니라면** MySQL의 IP 및 포트를 아웃바운드 규칙에 추가해야 합니다.

1. [보안 그룹 콘솔](https://console.cloud.tencent.com/cvm/securitygroup)에 로그인하고, 보안 그룹명을 클릭하여 CVM에 바인딩된 보안 그룹의 상세 페이지로 이동합니다.
2. **아웃바운드 규칙** 탭을 선택하고 **규칙 추가**를 클릭합니다.
'유형'은 MySQL(3306)을 선택하고, '타깃'에는 MySQL의 IP 주소(대역)를 입력한 다음, '정책'에는 허용을 선택합니다.

#### [MySQL 보안 그룹 설정 오류](id:maqzpzyw)
지정 CVM을 MySQL 인스턴스에 연결하려면 MySQL 보안 그룹에 인바운드 규칙을 설정해야 합니다. **인바운드 규칙의 원본 설정이 0.0.0.0/0이 아니고 프로토콜 포트가 ALL이 아닐 경우** CVM 인스턴스의 IP 및 포트를 인바운드 규칙에 추가해야 합니다. 

1. [보안 그룹 콘솔](https://console.cloud.tencent.com/cvm/securitygroup)에 로그인한 후, 보안 그룹 이름을 클릭하여 MySQL에 바인딩된 보안 그룹 상세 페이지로 이동합니다.
2. **인바운드 규칙** 탭을 선택하고 **규칙 추가**를 클릭합니다.
액세스를 허용할 IP 주소(대역) 및 개방이 필요한 포트 정보(MySQL 내부 네트워크 포트)를 입력하고, 포트 개방 허용을 선택합니다.
'유형은 MySQL(3306)을 선택하고, '출처'는 CVM의 IP 주소(대역)를 입력한 다음, '정책'에는 허용을 선택합니다.
>!TencentDB for MySQL을 연결하려면 반드시 MySQL 인스턴스 포트를 개방해야 합니다.
>- MySQL 내부 네트워크의 기본 포트는 3306이며 사용자 정의 포트도 지원합니다. 기본 포트 번호를 수정했다면, 보안 그룹에서 MySQL의 새로운 포트 정보를 다시 개방해야 합니다.
>- MySQL 외부 네트워크 포트는 시스템에 의해 자동으로 할당되며 사용자 정의를 지원하지 않습니다. 외부 네트워크 활성화 후 보안 그룹의 네트워크 액세스 정책에 의해 제어됩니다. 보안 정책 구성 시 내부 네트워크 액세스 포트를 개방을 해야 합니다. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 후 인스턴스 ID를 클릭하여 세부 정보 페이지로 들어가 포트를 확인할 수 있습니다.
  ![](https://main.qcloudimg.com/raw/9f471c644eb9a5aa86bd092fdebd0255.png)

## 부록2
### [내부/외부 네트워크 주소 확인](id:nwwpdff)
[MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 후, 인스턴스 ID를 클릭하면 인스턴스 상세 페이지에서 내부/외부 네트워크 주소를 조회할 수 있습니다.
![](https://main.qcloudimg.com/raw/322c89b12772441c4fd8e83f597092ed.png)

### [네트워크 유형/VPC 판단 방법](id:wllxvpdff)
내부 네트워크 주소를 통해 CDB에 연결하려면, CVM과 MySQL의 계정이 동일해야 하고, 동일한 VPC 내(동일한 리전)에 있거나 기본 네트워크가 동일해야 합니다.
>?CVM과 MySQL의 계정은 반드시 동일해야 합니다.
>- 인스턴스 리스트의 **네트워크** 필드에 모두 ‘기본 네트워크’ 또는 ‘VPC’라고 표시되면, CVM 및 MySQL의 네트워크가 동일한 유형임을 의미합니다.
>- 인스턴스 리스트의 **네트워크** 필드에 모두 동일한 ‘VPC’(동일 리전)가 표시되면, CVM 및 MySQL가 동일한 VPC임을 의미합니다.
>
- **CVM 네트워크 유형/VPC 조회**: [CVM 콘솔](https://console.cloud.tencent.com/cvm/instance)에 로그인하여, 인스턴스 리스트에서 '네트워크'를 조회합니다.
  ![](https://main.qcloudimg.com/raw/ce2550045bc286172f841f4fcceb0cc4.png)
- **MySQL 네트워크 유형/동일 VPC 조회**: [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인하여, 인스턴스 리스트에서 '네트워크'를 조회합니다.
  ![](https://main.qcloudimg.com/raw/2cc5396f1b3f8af2028d75ae642a5126.png)

