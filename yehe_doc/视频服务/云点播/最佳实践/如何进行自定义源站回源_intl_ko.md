## 소개

사용자 지정 Origin-pull 기능은 VOD(Video-on-demand) CDN 기능에 의존합니다. 사용자 지정 도메인 이름을 생성하고 Origin-pull 정보를 구성하면 사용자는 VOD의 도움으로 타사 원본 사이트에 저장된 미디어 파일의 배포를 가속화하여 사용자에게 멀티 클라우드 시나리오에서 미디어 배포 스키마를 제공할 수 있습니다. 이 문서에서는 VOD 사용자 지정 Origin-pull 기능을 구성하고 사용하는 방법을 소개합니다.

## 시나리오

- **원본 사이트 마이그레이션 비용 높음**: 사용자의 미디어 리소스는 다른 타사 원본 사이트에 저장되어 있으며 원본 사이트의 콘텐츠는 타사 플랫폼과 고도로 결합되어 원본 사이트를 마이그레이션하기 어렵습니다. 사용자 지정 Origin-Pull 기능을 기반으로 원본 사이트를 마이그레이션하지 않고 사용할 수 있으며 VOD의 CDN으로 콘텐츠 배포를 가속화합니다.
- **높은 재생 품질 요구 사항**: 사용자의 콘텐츠가 네트워크 딜레이 및 랙에 대한 요구 사항이 높으면 다른 타사 플랫폼으로 사용자 요구를 충족하기 어렵습니다. 사용자 지정 Origin-pull 기능은 고객에게 보다 부드러운 오디오 및 비디오 재생을 보장하여 서비스 품질을 보장할 수 있습니다.
- **멀티 클라우드 공존으로 리스크 감소**: 사용자의 콘텐츠와 비즈니스에는 비즈니스 안정성을 보장하고 재해 복구 기능을 개선하기 위해 여러 콘텐츠 가속 채널이 필요합니다. 가속 오디오 및 비디오 배포를 위해 Tencent Cloud VOD CDN을 선택할 수 있습니다.

## 전제 조건

1. Tencent Cloud 계정 [가입](https://intl.cloud.tencent.com/register?&s_url=https%3A%2F%2Fcloud.tencent.com%2F) 및 [로그인](https://intl.cloud.tencent.com/login?s_url=https%3A%2F%2Fcloud.tencent.com%2F) 후, 계정 실명 인증을 완료합니다.
2. Tencent Cloud VOD 서비스를 활성화합니다. 활성화되지 않은 경우 [VOD 서비스](https://console.cloud.tencent.com/vod/overview)를 활성화하십시오.

## 지원되는 원본 유형

- **자체 원본 서버**
- **타사 스토리지**

## 실행 순서

### 1단계: 사용자 지정 도메인 이름 생성 및 origin-pull 정보 구성

1. 사용자 지정 Origin-pull이 활성화된 후 VOD 콘솔에 로그인하고 왼쪽 탐색 바에서 **배포 재생 설정** > [**도메인 관리**](https://console.cloud.tencent.com/vod/distribute-play/domain)를 선택하여 **도메인 관리** 페이지로 들어갑니다.
2. 상단의 원본 사이트 가속의 **사용자 정의 원본 서버 도메인**을 클릭하여 원본 사이트 가속의 **사용자 지정 도메인 이름** 페이지로 들어갑니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e68e04641c3ad616450a70c72d5d3dcd.png)
3. **도메인 추가**를 클릭하고 등록된 도메인 이름을 입력하고 가속 리전을 선택합니다. 자세한 내용은 [온디맨드 가속 도메인](https://intl.cloud.tencent.com/document/product/266/35572)을 참고하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/0fbcc49821fd7eebffd9ad17a81072b1.png)
4. 사용자의 실제 Origin-pull 요구 사항에 따라 원본 스테이션 구성을 입력합니다. 현재 **자체 소유 서버** 및 **타사 스토리지**가 지원됩니다. 구체적인 구성 지침은 다음과 같습니다.     
![](https://qcloudimg.tencent-cloud.cn/raw/9ac80033d6fb055e299a2f355d0d1825.png) 

**자체 원본 서버**
사용자가 VOD CDN의 도움으로 미디어 파일 배포를 가속화하기 위해 안정적으로 실행되는 비즈니스 서버를 원본 사이트로 사용하려면 다음과 같이 원본 사이트를 구성하십시오.
<table>
   <tr>
      <th width="0px" style="text-align:center">구성 항목</td>
      <th width="0px"  style="text-align:center">설명</td>
   </tr>
   <tr>
      <td>원본 유형</td>
      <td>선택<b>자체 소유 서버</b></td>
   </tr>
   <tr>
      <td>Origin-pull 프로토콜</td>
      <td>원본 사이트의 지원에 따라 HTTP, HTTPS 및 다음 프로토콜을 지원하는 Origin-pull 요청 프로토콜을 선택합니다</td>
   </tr>
	   <tr>
      <td>Origin-pull 주소</td>
      <td>여러 IP 원본 사이트(쉼표로 구분) 또는 도메인 이름 원본 사이트 채우기 지원</td>
   </tr>
	 <tr>
      <td>Origin-pull HOST</td>
      <td>자체 원본 사이트는 Origin-pull HOST를 지정할 수 있으며,origin-pull HOST는 origin pull시 CDN 노드가 액세스하는 사이트의 도메인 이름/IP의 특정 사이트를 지정하는데 사용됩니다. <br>Origin-pull HOST를 지정하지 않으면 기본적으로 현재 가속 도메인 이름이 사용됩니다.</td>
   </tr>
</table>

<dx-alert infotype="explain" title="">
- 원본 사이트 주소는 VOD의 기본 도메인 이름을 지원하지 않습니다.
- 프로토콜 팔로우는 HTTP 액세스는 HTTP Origin-pull을 사용하며, HTTPS 액세스는 HTTPS Origin-pull(원본 사이트는 HTTPS 액세스를 지원해야 함)을 사용합니다.
- Origin-pull 주소로 도메인 이름을 선택할 수 있으며, 이 도메인 이름은 비즈니스 가속 도메인 이름과 같을 수 없습니다.
</dx-alert>
<b>타사 객체 스토리지</b><br>
VOD CDN 기능의 도움으로 타사 객체 스토리지에 저장된 미디어 파일의 배포를 가속화하려면 원본 사이트를 다음과 같이 구성하십시오.              
<table>
   <tr>
      <th width="0px" style="text-align:center">구성 항목</td>
      <th width="0px"  style="text-align:center">설명</td>
   </tr>
   <tr>
      <td>원본 유형</td>
      <td>선택<b>타사 객체 스토리지</b></td>
   </tr>
   <tr>
      <td>타사 객체 스토리지</td>
      <td>현재 지원되는 타사 객체 스토리지에는 Alibaba Cloud 및 AWS가 포함됩니다</td>
   </tr>
	   <tr>
	<td>Origin-pull 프로토콜</td>
	  <td>HTTP, HTTPS 지원</td>
   </tr>
	 <tr>
      <td>Origin-pull 주소</td>
      <td>원본 서버로 유효한 버킷 액세스 주소를 입력하십시오(http:// 또는 http:// 프로토콜 헤더를 포함할 수 없음)</td>
   </tr>
</table>

<img src="https://qcloudimg.tencent-cloud.cn/raw/f5ca4759794c94ffba9f6a960b9a8641.png" /><br>
비공개로 액세스한 타사 객체 스토리지 버킷을 원본 사이트로 선택한 경우 Origin-pull 인증을 위해 유효한 액세스 ID 및 key를 입력해야 합니다. 인증이 통과되면 프라이빗 스토리지 버킷 액세스가 활성화됩니다.<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/66864ace26867520f76172f2901ad138.png" />

### 2단계: 도메인 이름 레졸루션 사용자 지정

추가된 사용자 지정 가속 도메인 이름의 경우 사용자가 가속 도메인 이름을 통해 미디어 파일에 액세스할 수 있도록 도메인 이름으로 지정된 DNS 서비스 제공 업체에 CNAME을 구성해야 합니다. 자세한 내용은 [VOD 가속 도메인 이름 - 도메인 이름 레졸루션](https://intl.cloud.tencent.com/document/product/266/42076)을 참고하십시오.

### 3단계: 사용자 지정 origin-pull의 구성 결과 보기 및 수정
1. 도메인 관리로 이동하여 **사용자 지정 원본 서버 도메인**을 입력하고 생성된 도메인 이름을 선택한 다음 **설정**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/3522690fd01bd3c0f90eb1065dc87965.png)
2. **기본 구성**을 클릭하면 현재 사용자 지정 도메인 이름의 origin-pull 구성 정보를 보고 수정할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/bb04aa08590e9f88680c29eb19a502b9.png)

상기 단계를 통해 사용자는 자신의 원본 사이트 또는 타사 개체 저장소를 기반으로 원본 풀 구성을 완료하고 VOD CDN을 통해 사용자 지정 원본 사이트에 미디어 파일을 배포할 수 있습니다. 구체적인 배포 프로세스는 다음과 같습니다.

1. 사용자가 사용자 지정 도메인 이름(예시: `test.com`)을 추가하고 Origin-pull의 도메인 이름 레졸루션 및 구성을 완료하면 브라우저를 통해 도메인 이름으로 미디어 파일에 액세스할 때(예시: `http://www.test.com/test.mp4`), 먼저 로컬 DNS에 대한 도메인 이름 레졸루션 요청을 시작합니다.
2. Local DNS가 도메인 이름 `test.com`을 리졸브하면 CNAME이 `www.test.com.cdn.dnsv1.com`으로 구성되었음을 확인하고 Tencent GSLB(Global Server Load Balance, Tencent가 독자적으로 개발한 글로벌 로드 밸런싱 시스템)에 대한 요청을 확인합니다.
3. GSLB는 최상의 액세스 노드 IP 목록을 반환하고 Local DNS는 해당 리졸브 IP를 얻습니다.
4. 사용자는 최상의 액세스 IP 노드를 얻습니다.
5. 사용자는 최상의 액세스 IP 노드에 대한 `http://www.test.com/test.mp4`에 대한 액세스 요청을 시작합니다.
6. CDN 노드에 캐시된 test.mp4가 있으면 사용자는 데이터를 가져오고 요청을 종료합니다. CDN 노드가 리소스를 캐시하지 않으면 노드는 구성한 **비즈니스 원본 사이트**에 대한 test.mp4 요청을 시작합니다. 리소스를 얻은 후 기본적으로 현재 노드에 캐시하고 리소스를 사용자에게 반환합니다. 이때 요청을 종료합니다.

>? 사용자가 사용자 지정 Origin-Pull 기능을 사용하여 배포를 가속화하고 미디어 파일을 재생하면 **다운링크 트래픽** 요금과 **Origin-Pull 트래픽** 요금이 발생합니다. 다운링크 트래픽 요금은 VOD에서 부과합니다. 구체적인 규칙은 [트래픽 과금](https://intl.cloud.tencent.com/document/product/266/14666) 및 [트래픽 패키지](https://www.tencentcloud.com/document/product/266/52806#2.-.E6.B5.81.E9.87.8F.E8.B5.84.E6.BA.90.E5.8C.85)를 참고하십시오. 원본 사이트의 트래픽 요금은 원본 사이트에서 부과합니다.