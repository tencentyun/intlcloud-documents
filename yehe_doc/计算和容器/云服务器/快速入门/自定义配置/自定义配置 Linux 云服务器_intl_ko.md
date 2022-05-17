CVM 빠른 설정과 비교하여 사용자 정의 설정은 더 많은 이미지 플랫폼과 스토리지, 대역폭 및 보안 그룹 등 고급 설정을 제공하므로 사용자는 필요에 따라 적합한 설정을 선택할 수 있습니다. 본 문서에서는 사용자 정의 설정을 예로 들어 소개합니다.

## 가입 및 인증

CVM를 사용하기 전 다음과 같은 준비 작업을 완료해야 합니다.
1. Tencent Cloud 계정 생성 및 실명 인증을 완료합니다.
신규 사용자의 Tencent Cloud 공식 사이트 [가입](https://intl.cloud.tencent.com/register) 관련 자세한 내용은 [Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985)을 참고하십시오.
2. [Tencent Cloud CVM 소개 페이지](https://intl.cloud.tencent.com/zh/products/cvm)에서 **구매하기**를 클릭합니다.


## 모델 선택[](id:SelectType)

<dx-alert infotype="notice" title="">
처음으로 계정을 구매할 경우 **빠른 설정** 페이지로 진입합니다. 사용자가 이미 CVM을 구매한 경우 기본으로 **사용자 정의 설정** 페이지로 진입합니다. CVM을 구매하지 않은 경우 **사용자 정의 설정**을 선택하고 작업을 실행합니다.
</dx-alert>

1. 페이지 알림에 따라 다음 정보를 설정합니다.
![](https://main.qcloudimg.com/raw/07493412dd043911fe8aa3ecb0d0bcd4.png)
<table>
<tr><th style="width: 20%">유형</th><th style="width: 12%">필수/옵션</th><th>설정 설명</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/213/2180">과금 방식</a></td><td>필수</td><td>실제 필요에 따라 선택합니다.<ul><li><b>사용량 과금</b>: CVM의 유연한 과금 방식은 이커머스 타임 세일 등 장치 수요 순간 변동폭이 큰 시나리오에 적합합니다.</li><li><b>스팟 인스턴스</b>: 일종의 새 인스턴스 작업 모드로서 빅 데이터 컴퓨팅, CLB, 온라인 서비스 및 네트워크 서비스 등 시나리오에 적합하며 일반 가격 범위는 종량제 요금의 10% - 20%입니다.</li></ul></td></tr>
<tr><td>리전</td><td>필수</td><td>사용자의 고객과 가장 가까운 리전을 선택하여 액세스 딜레이 시간을 낮추고 액세스 속도를 높일 것을 권장합니다.</td></tr>
<tr><td>가용존</td><td>필수</td><td>실제 요구 사항에 따라 선택합니다.</br>여러 대의 CVM을 구매해야 할 경우 서로 다른 가용존을 선택하여 재해 복구 효과를 실현할 것을 권장합니다.</td></tr>
<tr><td>네트워크</td><td>필수</td><td>Tencent Cloud에 구축된 논리적 격리를 나타내는 네트워크 용량으로써 VPC는 최소 하나의 서브넷으로 구성됩니다. 시스템은 사용자를 위해 각 리전에 기본 VPC 및 서브넷을 제공합니다.</br>
기존 VPC/서브넷이 사용자의 요구사항을 충족하지 못한 경우 VPC 콘솔에서 생성할 수 있습니다.</br><b>주의 사항</b>:<ul><li>동일한 VPC에서 리소스는 기본으로 내부 네트워크를 상호 연결합니다.</li><li>구매할 때 CVM과 가용존 속성이 동일한 서브넷에서 CVM을 생성해야 합니다.</li></ul></td></tr>
<tr><td>인스턴스</td><td>필수</td><td>Tencent Cloud는 기본 하드웨어 차이에 따라, 여러 종류의 인스턴스 유형을 제공하고 있습니다. 최적의 성능을 원한다면 최신 인스턴스 유형을 사용하시길 권장합니다.</br>인스턴스에 대한 더 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/11518">인스턴스 사양</a>을 참고하십시오.</td></tr>
<tr><td>이미지</td><td>필수</td><td>Tencent Cloud는 공용 이미지, 사용자 정의 이미지, 공유 이미지, 마켓플레이스 이미지를 제공하므로, <a href="https://intl.cloud.tencent.com/document/product/213/4941">이미지 유형</a>을 참고하여 선택하실 수 있습니다.</br>Tencent Cloud를 처음 사용할 경우, 공용 이미지를 선택하시길 권장합니다.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">시스템 디스크</a></td><td>필수</td><td>운영 체제 설치에 사용되며, 기본 용량은 50GB입니다.</br>리전에 따라 선택 가능한 CBS 유형이 달라질 수 있으므로, 실제 페이지 안내에 따라 선택하시기 바랍니다.</br>CBS에 대한 더 자세한 설명은 <a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS 유형</a>을 참고하십시오.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">데이터 디스크</a></td><td>옵션</td><td>CVM의 스토리지 용량 확장에 사용되며, 안전하고 효율적인 스토리지 디바이스를 제공합니다. 기본적으로 CBS 데이터 디스크가 추가되어 있지 않습니다.</br>CBS에 대한 더 자세한 설명은 <a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS 유형</a>을 참고하십시오.</td></tr>
<tr><td>정기 스냅샷</td><td>옵션</td><td>시스템 디스크 또는 데이터 디스크에 대해 정기 스냅샷 정책을 설정할 수 있습니다. 정기 스냅샷에 대한 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/362/35238">정기 스냅샷</a>을 참고하십시오.</td></tr>
<tr><td>공용 네트워크 대역폭</td><td>필수</td><td>Tencent Cloud는 다음 2가지 네트워크 과금 방식을 제공하므로 실제 필요에 따라 선택하십시오.<ul><li><b>대역폭 과금</b>: 고정적인 대역폭을 선택하여 본 대역폭을 초과할 경우 패킷이 손실됩니다. 네트워크 변동이 적은 시나리오에 적합합니다.</li><li><b>트래픽 과금</b>: 실제 사용한 트래픽에 따라 과금합니다. 피크값 대역폭을 제한하여 예기치 않은 트래픽에 따른 비용을 피할 수 있으며 대역폭이 해당 값을 초과할 경우 패킷이 손실됩니다. 네트워크 변동이 큰 시나리오에 적합합니다.</li></ul></td></tr>
<tr><td>수량</td><td>필수</td><td>구매할 CVM 수량을 표시합니다.</td></tr> 
</table>



2. **다음 단계: 호스트 설정**을 클릭하고 호스트 설정 페이지로 들어갑니다.

## 호스트 설정
1. 페이지 알림에 따라 다음 정보를 설정합니다.
![](https://main.qcloudimg.com/raw/44493e285aee4d9523e009b7690fc616.png)
<table>
  <tr>
	<th style="width: 20%">유형</th>
	<th style="width: 12%">필수/옵션</th>
	<th>설정 설명</th>
  </tr>
  <tr>
	<td>보안 그룹</td>
	<td>필수</td>
	<td>단일 또는 다중 CVM 설정을 위한 네트워크 액세스 제어.
	<br />
	<b>22 로그인 포트가 열려 있는지 확인하십시오</b>, 더 많은 정보는 다음을 참고하십시오. 
	<a href="https://intl.cloud.tencent.com/document/product/213/12452">보안 그룹</a>.</td>
  </tr>
  <tr>
	<td>세부 항목</td>
	<td>필수</td>
	<td>기본은 기본 프로젝트이며, 실제 필요에 따라 다른 CVM을 관리하기 위해 구축된 프로젝트를 선택할 수 있습니다.</td>
  </tr>
  <tr>
	<td>태그</td>
	<td>옵션</td>
	<td>클라우드 리소스의 분류, 검색 및 취합을 위해 필요에 따라 인스턴스에 태그를 추가할 수 있습니다. 태그에 대한 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/651/13334">태그</a>를 참고하십시오.</td>
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
	  <b>즉시 키 연결</b>: SSH 키를 연결하면 SSH 키 방식을 통해 보다 안전하게 CVM에 로그인할 수 있습니다.
		<br />키가 없거나 기존 키가 적합하지 않은 경우 <b>지금 생성</b>을 클릭하여 생성할 수 있습니다. 더 많은 SSH 
	  키 관련 정보는 <a href="https://intl.cloud.tencent.com/document/product/213/6092">SSH 키</a>를 참고하십시오.</li>
	  <li>
	  <b>비밀번호 자동 생성</b>: 자동 생성된 비밀번호는 <a href="https://console.cloud.tencent.com/message">내부 메시지</a> 방식으로 발송됩니다.</li>
	</ul></td>
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
	<td>자동화 어시스턴트</td>
	<td>옵션</td>
	<td>기본적으로 무료로 활성화하며 CVM의 네이티브 유지보수 배포 툴로 인스턴스에 원격 연결 없이 Shell을 일괄 자동 실행할 수 있습니다.
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
	  <b>CAM 역할</b>: 역할 설정 후 해당 역할을 통해 CVM에 Tencent Cloud의 서비스, 운영 및 리소스에 대한 액세스 권한을 부여할 수 있습니다. <a href="https://intl.cloud.tencent.com/document/product/213/38290">인스턴스 역할 관리</a>를 참고하여 설정할 수 있습니다.</li>
	  <li>
	  <b>배치 그룹</b>: 서비스 가용성을 향상시키기 위해 필요에 따라 배치 그룹에 인스턴스를 추가할 수 있습니다. <a href="https://intl.cloud.tencent.com/document/product/213/15486">배치 그룹</a>을 참고하여 설정할 수 있습니다.</li>
	  <li>
	  <b>사용자 정의 데이터</b>: 인스턴스를 설정하려면 사용자 정의 데이터를 지정합니다. 즉, 인스턴스가 실행될 때 설정된 스크립트를 실행합니다. 한 번에 여러 CVM을 구매하면 사용자 정의 데이터가 모든 CVM에서 실행됩니다. Linux 
	  운영 체제는 Shell 형식을 지원하며 최대 16KB의 원시 데이터를 지원합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/17525">사용자 정의 데이터</a>를 참고하십시오.
	  <br />
	  <b>주의</b>: 사용자 정의 데이터 설정은 Cloudinit 서비스를 통해 일부 공용 이미지만 지원하며, 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/19670">Cloud-Init</a>를 참고하십시오.</li>
	</ul></td>
  </tr>
</table>


2. **다음 단계: 설정 정보 확인**을 클릭하고 설정 정보 확인 페이지로 이동합니다.


## 설정 정보 확인

1. 각 설정 비용에 대한 자세한 내용은 구매한 CVM 정보를 확인합니다.
2. ‘<Tencent Cloud 서비스 계약>에 동의’를 읽고 체크합니다.
3. 실제 필요에 따라 다음 작업을 수행합니다.
   - **실행 템플릿으로 저장** 선택: 인스턴스의 설정을 실행 템플릿으로 저장하면 빠른 인스턴스 생성에 사용할 수 있습니다. 자세한 내용은 [인스턴스 실행 템플릿 관리](https://intl.cloud.tencent.com/document/product/213/45221)를 참고하십시오.
   - **API Explorer 모범 사례 스크립트 생성** 선택: 선택된 설정에 해당하는 인스턴스를 생성하여 OpenAPI 모범 사례 스크립트 코드를 생성하고, 동일한 설정으로 클라우드 서버 구입을 위한 코드를 저장할 수 있습니다. 자세한 내용은 [인스턴스 생성을 위한 API Explorer 모범 사례 스크립트 생성](https://intl.cloud.tencent.com/document/product/213/39811)을 참고하십시오.
4. **구매하기** 또는 **활성화**를 클릭하여 결제를 완료합니다. 결제를 완료하면 [CVM 콘솔](https://console.cloud.tencent.com/cvm)에서 CVM을 확인하실 수 있습니다.
CVM 인스턴스 이름, 공용 IP 주소, 개인 IP 주소, 로그인 이름, 초기 로그인 비밀번호 등 정보는 [내부 메시지](https://console.cloud.tencent.com/message)로 계정에 전송됩니다. 이 정보로 인스턴스를 로그인 및 관리할 수 있으며 호스트의 보안성을 보장하기 위해 CVM 로그인 비밀번호를 변경하십시오.

## 인스턴스 로그인 및 연결

CVM 작업 완료 후, Tencent Cloud 콘솔을 통해 CVM에 로그인하여 실제 요구 사항에 따라 스테이션 구축 등 작업을 실행할 수 있습니다.
Tencent Cloud 콘솔을 통한 CVM 로그인은 실제 요구 사항에 따라 해당하는 로그인 방식을 선택하십시오.
- [표준 로그인 방식으로 Linux 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5436)
- [원격 로그인 소프트웨어를 사용하여 Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32502)
- [SSH를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)

## 데이터 디스크 파티션 및 포맷

[모델 선택](#SelectType) 시 데이터 디스크를 추가한 경우 인스턴스에 로그인한 후 데이터 디스크에 대해 포맷 및 파티션을 실행해야 합니다. **데이터 디스크를 추가하지 않은 경우 이 단계를 건너뛸 수 있습니다.**
디스크 용량 크기, CVM 운영 체제 유형에 따라 적합한 작업 가이드를 선택하십시오.
- 디스크 용량이 2TB 미만인 경우
 [CBS 초기화(Linux)](https://intl.cloud.tencent.com/document/product/362/31597)
- 디스크 용량이 2TB 이상인 경우
 [CBS 초기화(Linux)](https://intl.cloud.tencent.com/document/product/362/31598)

더 자세한 작업 가이드는 [초기화 시나리오 설명](https://intl.cloud.tencent.com/document/product/362/31596)을 참고하십시오.
