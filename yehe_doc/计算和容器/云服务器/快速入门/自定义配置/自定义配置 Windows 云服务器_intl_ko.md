CVM 빠른 설정과 비교하여 사용자 정의 설정은 더 많은 이미지 플랫폼과 스토리지, 대역폭 및 보안 그룹 등 고급 설정을 제공하므로 사용자는 필요에 따라 적합한 설정을 선택할 수 있습니다. 본 문서에서는 사용자 정의 설정을 예로 들어 소개합니다.


## 가입 및 인증

CVM를 사용하기 전 다음과 같은 준비 작업을 완료해야 합니다.
1. Tencent Cloud 계정 생성 및 실명 인증을 완료합니다.
신규 사용자의 Tencent Cloud 공식 사이트 [가입](https://www.tencentcloud.com/account/register) 관련 자세한 내용은 [Signing Up](https://www.tencentcloud.com/document/product/378/17985)을 참고하십시오.
2. [Cloud Virtual Machine 소개 페이지](https://www.tencentcloud.com/products/cvm)에서 **구매하기**를 클릭합니다.


## 기본 구성 선택[](id:SelectType)

<dx-alert infotype="notice" title="">
처음으로 계정을 구매할 경우 **빠른 설정** 페이지로 진입합니다. 사용자가 이미 CVM을 구매한 경우 기본으로 **사용자 정의 설정** 페이지로 이동합니다. CVM을 구매하지 않은 경우 **사용자 정의 설정**을 선택하고 작업을 실행합니다.
</dx-alert>

1. 페이지 알림에 따라 다음 정보를 설정합니다.
<table>
  <tr>
	<th style="width: 20%">유형</th>
	<th style="width: 12%">필수/옵션</th>
	<th>설정 설명</th>
  </tr>
  <tr>
	<td>
	  <a href="https://intl.cloud.tencent.com/document/product/213/2180">과금 방식</a>
	</td>
	<td>필수</td>
	<td>필요에 따라 선택하십시오:
	<ul>
	  <li>
	  <b>종량제</b>: 이커머스 타임 세일과 같이 수요가 급격하고 갑작스럽게 변동하는 시나리오에 적합한 유연한 과금 방식입니다.</li>
	  <li>
	  <b>스팟 인스턴스</b>: 빅 데이터 컴퓨팅, 로드 밸런싱이 있는 온라인 비즈니스 및 웹 사이트 서비스와 같은 시나리오에 적합합니다. 일반적인 가격 범위는 종량제 인스턴스의 10%
	  - 20%입니다.</li>
	</ul></td>
  </tr>
  <tr>
	<td>리전</td>
	<td>필수</td>
	<td>고객과 가장 가까운 리전을 선택하여 액세스 지연 시간을 줄이고 액세스 속도를 높입니다.</td>
  </tr>
  <tr>
	<td>가용존</td>
	<td>필수</td>
	<td>필요에 따라 가용존을 선택합니다.
	<br />여러 CVM 인스턴스를 구매하려는 경우 재해 복구를 구현하기 위해 다른 가용존을 선택하는 것이 좋습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/6091">리전 및 가용존</a>을 참고하십시오.</td>
  </tr>
	<tr>
	<td>인스턴스</td>
	<td>필수</td>
	<td>
	Tencent Cloud는 기본 하드웨어를 기반으로 다양한 인스턴스 유형을 제공합니다. 최적의 성능을 위해 차세대의 인스턴스 유형을 사용하는 것이 좋습니다. 
	<br />인스턴스에 대한 자세한 내용은  
	<a href="https://intl.cloud.tencent.com/document/product/213/11518">인스턴스 스펙</a>을 참고하십시오.</td>
  </tr>
	<tr>
	<td>이미지</td>
	<td>필수</td>
	<td>Tencent Cloud는 공용 이미지, 사용자 정의 이미지 및 공유 이미지를 제공합니다. 
	<a href="https://intl.cloud.tencent.com/document/product/213/4941">이미지 유형</a>을 참고하십시오.</td>
	<br />Tencent Cloud를 사용하기 시작했다면 공용 이미지를 선택하는 것이 좋습니다.</td>
  </tr>
	 <tr>
	<td>
	  <a href="https://intl.cloud.tencent.com/document/product/362/31636">Cloud Disk Types</a>
	</td>
	<td>필수</td>
	<td>운영 체제를 설치하는 데 사용됩니다. 기본 용량은 50GB입니다.
	<br />사용 가능한 CBS(Cloud Block Storage) 유형은 리전에 따라 다릅니다. 페이지의 안내에 따라 선택하십시오.
	<br />CBS에 대한 자세한 내용은  
	<a href="https://intl.cloud.tencent.com/document/product/362/31636">Cloud Disk Types</a>를 참고하십시오.</td>
  </tr>
  <tr>
	<td>
	  <a href="https://intl.cloud.tencent.com/document/product/362/31636">데이터 디스크</a>
	</td>
	<td>옵션</td>
	<td>높은 효율성과 안정성을 보장하기 위해 CVM 인스턴스의 스토리지 용량을 확장하는 데 사용됩니다. CBS 데이터 디스크는 기본적으로 추가되지 않습니다.
	<br />CBS에 대한 자세한 내용은  
	<a href="https://intl.cloud.tencent.com/document/product/362/31636">Cloud Disk Types</a>를 참고하십시오.</td>
  </tr>
  <tr>
	<td>정기 스냅샷</td>
	<td>옵션</td>
	<td>시스템 디스크 또는 데이터 디스크에 대해 정기 스냅샷 정책을 설정할 수 있습니다. 자세한 내용은  
	<a href="https://intl.cloud.tencent.com/document/product/362/35238">Scheduled Snapshots</a>를 참고하십시오.</td>
  </tr>
	<tr>
	<td>수량</td>
	<td>필수</td>
	<td>구매할 CVM 인스턴스 수량입니다.</td>
  </tr>
</table>

2. **다음 단계: 네트워크 및 호스트 설정**을 클릭하고 호스트 설정 페이지로 들어갑니다.




## 네트워크 및 호스트 설정
1. 페이지 안내에 따라 다음 정보를 설정합니다.
<table>
  <tr>
	<th style="width: 20%">유형</th>
	<th style="width: 12%">필수/옵션</th>
	<th>설정 설명</th>
  </tr>
	 <tr>
	<td>네트워크</td>
	<td>필수</td>
	<td>
	Tencent Cloud에 구축된 논리적으로 격리된 네트워크 공간입니다. VPC에는 하나 이상의 서브넷이 포함됩니다. 시스템은 각 리전에 대한 기본 VPC 및 서브넷을 제공합니다.
	<br />기존 VPC 또는 서브넷이 요구 사항을 충족하지 않는 경우 VPC 콘솔에서 VPC 또는 서브넷을 생성할 수 있습니다.
	<br />
	<b>참고</b>:
	<ul>
	  <li>동일한 VPC의 리소스는 사설망 내에서 공유될 수 있습니다.</li>
	  <li>CVM 인스턴스를 구매할 때 CVM 인스턴스와 CVM 인스턴스가 생성되는 서브넷의 가용존이 동일한지 확인하십시오.</li>
	</ul></td>
  </tr>
  <tr>
	<td>공용 IP</td>
	<td>옵션</td>
	<td>CVM에 공중망 액세스가 필요한 경우 CVM에 공용 IP를 할당해야 합니다. CVM을 생성할 때 공용 IP를 할당하도록 선택하거나 CVM이 생성된 후 CVM에 대한 <a href="https://intl.cloud.tencent.com/document/product/213/5733">Elastic IP</a>를 구성할 수 있습니다. </td>
	</tr>
	<tr>
	<td>대역폭 과금 방식</td>
	<td>옵션</td>
	<td>Tencent Cloud는 두 가지 네트워크 과금 방식을 제공합니다. 필요에 따라 값을 설정합니다.
	<ul>
	  <li>
	  <b>트래픽별 과금</b>: 실제로 사용된 트래픽을 기반으로 과금됩니다. 대역폭 상한을 지정하여 예기치 않은 트래픽으로 인해 발생하는 요금을 방지할 수 있습니다. 순간 대역폭이 이 값을 초과하면 패킷 손실이 발생합니다. 네트워크 연결이 크게 변동하는 시나리오에 적합합니다.</li>
	  <li>
	  <b>대역폭 패키지</b>: 공용 네트워크 인스턴스에 서로 다른 시간대의 트래픽 피크가 있는 경우 이 통합 과금을 선택합니다. 공중망을 통해 서로 다른 인스턴스 간에 트래픽이 시차를 둘 수 있는 대규모 비즈니스에 적합합니다.
	  <br />대역폭 패키지는 현재 베타 테스트 중입니다. 사용을 원하시면  
	  <a href="https://console.intl.cloud.tencent.com/workorder/category">티켓 제출</a>하십시오.</li>
	</ul>자세한 내용은  <a href="https://intl.cloud.tencent.com/document/product/213/10578">공용 네트워크 과금 방식</a>을 참고하십시오.
	</td>
  </tr>
	<tr>
	<td>대역폭 값</td>
	<td>옵션</td>
	<td>필요에 따라 CVM의 공용 네트워크 대역폭 최댓값을 설정할 수 있습니다. 자세한 내용은  <a href="https://intl.cloud.tencent.com/document/product/213/12523">공용 네트워크 대역폭 최댓값</a>을 참고하십시오.</td>
	</tr>
  <tr>
	<td>보안 그룹</td>
	<td>필수</td>
	<td>단일 또는 다중 CVM 설정을 위한 네트워크 액세스 제어.
	<br />
	<b>3389 로그인 포트가 열려 있는지 확인하십시오</b>, 더 많은 정보는 다음을 참고하십시오. 
	<a href="https://intl.cloud.tencent.com/document/product/213/12452">보안 그룹</a>.</td>
  </tr>
	<tr>
	<td>태그</td>
	<td>옵션</td>
	<td>클라우드 리소스를 분류, 검색 및 집계하는 데 사용되는 필요에 따라 CVM에 대한 태그를 추가할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/651/13334">Tag</a>를 참고하십시오.</td>
  </tr>
	<tr>
	<td>인스턴스 이름</td>
	<td>옵션</td>
	<td>생성할 CVM의 이름을 나타냅니다.
	<br />사용자 사용자 정의, ‘CVM-01’로 권장합니다.</td>
  </tr>
  <tr>
	<td>로그인 방법</td>
	<td>필수</td>
	<td>사용자가 CVM에 로그인하는 방식을 설정합니다. 실제 필요에 따라 설정하십시오.
	<ul>
	  <li>
	  <b>비밀번호 설정</b>: 인스턴스에 로그인하기 위한 비밀번호를 사용자 정의합니다.</li>
	  <li>
	  <b>비밀번호 자동 생성</b>: 자동 생성된 비밀번호는 <a href="https://console.cloud.tencent.com/message">메시지 센터</a>를 통해 발송됩니다.</li>
	</ul></td>
  </tr>
	<tr>
	<td>인스턴스 폐기 방지</td>
	<td>옵션</td>
	<td>기본적으로 비활성화되어 있습니다. 필요에 따라 활성화할 수 있습니다. 활성화 하면 콘솔이나 API를 통해 인스턴스를 폐기할 수 없습니다. 자세한 내용은 <a href="https://www.tencentcloud.com/document/product/213/47383">인스턴스 폐기 방지 활성화</a>를 참고하십시오.</td>
  </tr>
  <tr>
	<td>보안 강화</td>
	<td>옵션</td>
	<td>기본적으로 무료로 활성화되어 있으며 사용자가 데이터 유출을 방지하기 위한 서버 보안 시스템을 구축할 수 있도록 도와줍니다.</td>
  </tr>
  <tr>
	<td>클라우드 모니터링</td>
	<td>옵션</td>
	<td>
	기본적으로 무료로 활성화하며 3차원 CVM 데이터 모니터링, 스마트한 데이터 분석, 실시간 장애 알람 및 개성화된 데이터 리포트 설정을 제공하여 사용자가 서비스와 CVM 상태를 정확하게 파악할 수 있습니다.</td>
  </tr>
	<tr>
	<td>TAT</td>
	<td>옵션</td>
	<td>기본적으로 무료로 활성화하며 Cloud Virtual Machine의 네이티브 유지보수 배포 툴로 인스턴스에 원격 연결 없이 Shell을 일괄 자동 실행할 수 있습니다.
	자동화된 유지보수 스크립트 실행, 프로세스 폴링, 소프트웨어 설치/언마운트, 애플리케이션 업데이트 및 패치 설치 등의 작업을 완료하기 위한 명령어입니다.</td>
  </tr>
  <tr>
	<td>고급 설정</td>
	<td>옵션</td>
	<td>실제 필요에 따라 인스턴스에서 더 많은 구성을 수행합니다.
	<ul>
	  <li>
	  <b>호스트 이름</b>: 사용자는 CVM 운영 체제 내에서 PC 이름을 사용자 정의할 수 있으며, CVM이 성공적으로 생성된 후 CVM에 로그인하여 확인할 ​​수 있습니다.</li>
		<li>
	  <b>프로젝트</b>: 기본 프로젝트가 선택됩니다. 다른 CVM 인스턴스를 관리하기 위해 필요에 따라 기존 프로젝트를 선택할 수 있습니다.</li>
	  <li>
	  <b>CAM 역할</b>: 역할 설정 후 해당 역할을 통해 CVM에 Tencent Cloud의 서비스, 운영 및 리소스에 대한 액세스 권한을 부여할 수 있습니다. <a href="https://intl.cloud.tencent.com/document/product/213/45917">인스턴스 역할 관리</a>를 참고하여 설정할 수 있습니다.</li>
	  <li>
	  <b>배치 그룹</b>: 서비스 가용성을 향상시키기 위해 필요에 따라 배치 그룹에 인스턴스를 추가할 수 있습니다. <a href="https://intl.cloud.tencent.com/document/product/213/15486">배치 그룹</a>을 참고하여 설정할 수 있습니다.</li>
	  <li> <b>사용자 정의 데이터</b>: 인스턴스를 설정하려면 사용자 정의 데이터를 지정합니다. 즉, 인스턴스가 실행될 때 설정된 스크립트를 실행합니다. 한 번에 여러 CVM을 구매하면 사용자 정의 데이터가 모든 CVM에서 실행됩니다. Windows 
	  운영 체제는 PowerShell 형식을 지원하며 최대 16KB의 원시 데이터를 지원합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/17526">사용자 정의 데이터를 설정 (Windows CVM)</a>을 참고하십시오.
	  <br />
	  <b>참고</b>: 사용자 정의 데이터 구성은 Windows 공용 이미지만 지원합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/17526#.E6.B3.A8.E6.84.8F.E4.BA.8B.E9.A1.B9">주의 사항</a>을 참고하십시오.</li>
	</ul></td>
  </tr>
</table>

2. **다음 단계: 설정 정보 확인**을 클릭하고 설정 정보 확인 페이지로 이동합니다.





## 설정 정보 확인
1. 구매할 CVM 인스턴스 정보와 각 구성 항목의 비용 세부 정보를 확인합니다.
2. ‘<Tencent Cloud 서비스 약관>’을 읽고 동의 체크합니다.
3. 실제 필요에 따라 다음 작업을 수행합니다.
    - **실행 템플릿으로 저장** 선택: 인스턴스의 설정을 실행 템플릿으로 저장하면 빠른 인스턴스 생성에 사용할 수 있습니다. 자세한 내용은 [인스턴스 실행 템플릿 관리](https://intl.cloud.tencent.com/document/product/213/45221)를 참고하십시오.
    - **API Explorer 모범 사례 스크립트 생성** 선택: 선택된 설정에 해당하는 인스턴스를 생성하여 OpenAPI 모범 사례 스크립트 코드를 생성하고, 동일한 설정으로 클라우드 서버 구입을 위한 코드를 저장할 수 있습니다. 자세한 내용은 [인스턴스 생성을 위한 API Explorer 모범 사례 스크립트 생성](https://intl.cloud.tencent.com/document/product/213/39811)을 참고하십시오.
4. **즉시 구매** 또는 **활성화**를 클릭하여 결제를 완료합니다.
결제 완료 후 [CVM 콘솔](https://console.cloud.tencent.com/cvm)로 이동하여 CVM 가격을 조회할 수 있습니다.
CVM 인스턴스 이름, 공용 IP 주소, 내부 IP 주소, 로그인 이름, 초기 로그인 비밀번호 등 정보는 [메시지 센터](https://console.cloud.tencent.com/message)를 통해 계정에 전송됩니다. 이 정보로 인스턴스를 로그인 및 관리할 수 있으며 호스트의 보안성을 보장하기 위해 CVM 로그인 비밀번호를 변경하십시오.

## 인스턴스 로그인 및 연결

CVM 작업 완료 후, Tencent Cloud 콘솔을 통해 CVM에 로그인하여 실제 요구 사항에 따라 스테이션 구축 등 작업을 실행할 수 있습니다.
Tencent Cloud 콘솔을 통한 CVM 로그인은 실제 요구 사항에 따라 해당하는 로그인 방식을 선택하십시오.
- [표준 로그인 방식으로 Windows 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/41018)
- [RDP 파일을 통한 Windows 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/5435)
- [원격 데스크탑을 사용하여 Windows 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32498)

## 데이터 디스크 포맷과 파티션

[모델 선택](#SelectType) 시 데이터 디스크를 추가한 경우 인스턴스에 로그인한 후 데이터 디스크에 대해 포맷 및 파티션을 실행해야 합니다. **데이터 디스크를 추가하지 않은 경우 이 단계를 건너뛸 수 있습니다.**
디스크 용량 크기, CVM 운영 체제 유형에 따라 적합한 작업 가이드를 선택하십시오.
- 디스크 용량이 2TB 미만인 경우
[Initializing Cloud Disks (<2 TB)](https://intl.cloud.tencent.com/document/product/362/31597)
- 디스크 용량이 2TB 이상인 경우
[Initializing Cloud Disks (≥2 TB)](https://intl.cloud.tencent.com/document/product/362/31598)

더 자세한 작업 가이드는 [Initialization Scenarios](https://intl.cloud.tencent.com/document/product/362/31596)를 참고하십시오.
