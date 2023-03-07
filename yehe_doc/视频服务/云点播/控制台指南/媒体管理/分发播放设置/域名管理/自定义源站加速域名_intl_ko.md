## 작업 시나리오

VOD(Video-on-Demand) 개방형 CDN 호스팅 기능은 사용자가 자체 원본 사이트에서 미디어 리소스를 배포하고 자체 원본 사이트 및 타사 객체 스토리지 사이트의 Origin-pull 기능을 지원하는 데 도움이 됩니다. 사용자 지정 도메인 이름을 생성하고 원본 사이트 유형, Origin-pull 요청 프로토콜 및 원본 사이트 주소를 구성함으로써 사용자는 사용자 지정 원본 사이트 기능을 구현할 수 있습니다(사용자 지정 Origin-pull 기능을 구성하기 위해 사용자 지정 도메인 이름만 지원됨).

## 구성 가이드
1. [VOD 콘솔](https://console.cloud.tencent.com/vod)에 로그인하여 왼쪽 사이드바에서 **애플리케이션 관리**를 클릭하여 애플리케이션 목록 페이지로 들어갑니다.
2. 설정할 애플리케이션을 찾고 애플리케이션 이름을 클릭하여 애플리케이션 관리 페이지로 들어갑니다.
3. 기본적으로 **미디어 자산 관리**>**오디오/비디오 관리**, ‘업로드됨’ 페이지로 이동합니다.
4. 왼쪽 탐색 바에서 **배포 재생 설정**>[**도메인 관리**](https://console.cloud.tencent.com/vod/distribute-play/domain)를 선택하여 **도메인 관리** 페이지로 이동합니다.
5. 가속화된 원본 사이트의 상위 **사용자 지정 원본 서버 도메인**을 클릭하여 ‘사용자 지정 원본 서버 도메인’ 목록 페이지로 들어갑니다.
![img](https://qcloudimg.tencent-cloud.cn/raw/f0536b39ee6156173e7cd27b3642f791.png)
6. **도메인 추가**를 클릭하여 실제 필요에 따라 도메인 이름 구성 및 원본 서버 구성을 완료합니다.
 - 도메인 구성
도메인 이름을 입력하고 도메인 이름 가속 영역을 선택합니다. 관련 정보는 [도메인 추가](https://intl.cloud.tencent.com/document/product/266/35572)를 참고하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/ceb83e97ffdd3118c4890c13a68c6971.png)
 - 원본 구성
![](https://qcloudimg.tencent-cloud.cn/raw/43279ccef236c0211c4b996f8ff92fd6.png)

**원본 유형**
VOD는 자체 소유 원본 사이트 및 타사 객체 스토리지의 세 가지 Origin-pull 유형을 제공하며 사용자는 실제 필요에 따라 구성을 선택할 수 있습니다.
<table>
   <tr>
      <td >자체 소유 서버</td>
      <td >이미 안정적으로 실행되는 비즈니스 서버(즉 원본 사이트)가 있고 해당 IP 주소 목록을 입력하거나 도메인 이름을 원본 사이트 주소로 입력합니다.</td>
   </tr>
   <tr>
      <td>타사 객체 스토리지</td>
      <td>현재 지원되는 Tencent Cloud 이외의 타사 객체 스토리지는 Alibaba Cloud 및 AWS입니다.</td>
   </tr>
</table>


**Origin-pull 프로토콜**
VOD 가속 노드가 사용자의 원본 사이트, HTTP 또는 HTTPS로 돌아갈 때 사용되는 프로토콜입니다.
<table>
   <tr>
      <td>HTTP Origin-pull</td>
      <td>HTTP origin-pull은 액세스가 HTTP 또는 HTTPS일 때 사용됩니다.</td>
   </tr>
   <tr>
      <td>HTTPS Origin-pull</td>
      <td>HTTPS origin-pull은 액세스가 HTTP 또는 HTTPS일 때 사용됩니다.</td>
   </tr>
	    <tr>
      <td>프로토콜 팔로우</td>
      <td>HTTP 요청은 HTTP Origin-pull을 사용하고 HTTPS 요청은 HTTPS Origin-pull을 사용합니다.</td>
   </tr>
</table>

>? HTTPS origin-pull의 경우 원본 사이트가 HTTPS 액세스를 지원하는지 확인하십시오. 그렇지 않으면 origin-pull이 실패합니다.

**원본 주소**

<table>
   <tr>
      <td>자체 소유 서버</td>
      <td>여러 IP 원본 사이트 또는 도메인 이름 원본 사이트(쉼표로 구분) 채우기를 지원합니다.</td>
   </tr>
   <tr>
      <td>타사 객체 스토리지</td>
      <td><li>리소스가 타사 객체 스토리지에 저장된 경우 원본 사이트로 유효한 스토리지 버킷 액세스 주소를 입력하십시오(`http://` 또는 `http://` 프로토콜 헤더를 포함할 수 없음). 현재 지원되는 타사는 Alibaba Cloud OSS 및 AWS S3입니다. </li><br><li>타사 개인 스토리지 버킷으로 origin-pull하려면 유효한 키를 입력하고 원본 인증을 활성화해야 합니다. 즉, 개인 스토리지 버킷에 대한 액세스를 활성화해야 합니다.</li> </td>
   </tr>
</table>


>? 원본 사이트는 origin-pull HOST를 지정할 수 있으며, origin-pull HOST는 origin-pull 시 CDN 노드가 원본에서 방문하는 사이트의 도메인 이름/ip의 특정 사이트를 지정하는 데 사용됩니다. origin-pull HOST가 지정되지 않은 경우 현재 생성된 가속 도메인 이름이 기본적으로 사용됩니다.
4. 도메인 이름 레졸루션. 추가된 사용자 지정 가속 도메인 이름의 경우 사용자가 도메인 이름을 통해 비디오 미디어에 액세스할 수 있도록 도메인 이름으로 지정된 DNS 서비스 제공 업체에 CNAME을 구성해야 합니다. 자세한 내용은 [VOD 가속 도메인 이름-도메인 이름 레졸루션](https://intl.cloud.tencent.com/document/product/266/35572#.E8.A7.A3.E6.9E.90.E5.9F.9F.E5.90.8D)을 참고하십시오.


## Origin-pull 구성 수정
추가된 사용자 지정 도메인 이름은 사용자의 실제 요구에 따라 조정 및 수정할 수 있습니다. 수정 방법은 다음과 같습니다.
1. [**도메인 관리**](https://console.cloud.tencent.com/vod/distribute-play/domain)>**사용자 지정 원본 서버 도메인** 페이지에서 수정할 사용자 지정 도메인 이름을 선택하고 **설정**을 클릭한 후 세부 정보 페이지로 들어갑니다.
2. 기존 구성 정보를 수정하려면 **수정**을 클릭합니다. 수정된 결과가 적용되려면 5분이 걸립니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5df5f46ec7dc7fdc55f9bc3b780f8ac7.png)

>?
>- 사용자 지정 원본 사이트가 VOD 원본 사이트로 전환되면 먼저 사용자 지정 원본 사이트의 도메인 이름을 비활성화하고 삭제한 후 해당 도메인 이름을 VOD의 가속 도메인 이름에 추가해야 합니다.
>- 사용자가 원본으로 돌아가기 위해 사용자 지정 원본 사이트를 사용하려면 먼저 온디맨드 가속 도메인 이름에 구성된 도메인 이름을 비활성화 및 삭제 후 사용자 지정 원본 사이트 가속 도메인 이름으로 이동하여 추가해야 합니다.