본 문서는 COS 콘솔에서 CDN을 통해 COS의 리소스에 대한 액세스를 가속화하는 방법을 설명합니다.

## 전제 조건
1. Tencent Cloud 계정 가입 및 실명 인증을 완료합니다
2. CDN 서비스를 활성화합니다. 자세한 내용은 [CDN 시작하기](https://intl.cloud.tencent.com/document/product/228/5734)를 참고하십시오.

## 운영 가이드
### 버킷 생성
버킷 생성 작업 절차 및 방법은 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309)을 참고하십시오.

### 가속 구성
1. 버킷을 생성한 후 구성 관리 페이지로 직접 들어갑니다. 버킷 리스트에서 버킷의 작업 열에서 **구성 관리**를 클릭하여 해당 구성 관리 페이지로 이동할 수도 있습니다. 그 다음 **도메인 관리**를 선택합니다.
2. **기본 CDN 가속 도메인** 활성화
시스템에서 생성된 **기본 CDN 가속 도메인**은 CDN 캐시 노드를 통과하는 도메인 이름입니다. 활성화 또는 비활성화하도록 선택할 수 있습니다.
(1) [편집]을 클릭하여 기본 CDN 가속 도메인을 수동으로 활성화합니다.
![](https://main.qcloudimg.com/raw/260fde070f4b2f999c0d9d09bec13d55.png)
(2) 기본 CDN 가속 설정:
![](https://main.qcloudimg.com/raw/2b72c25d2bf11f0c53a2e8286fcecf07.png)
**원본 서버 유형**: **기본 원본 서버**로 설정됩니다. 원본 서버 버킷에 대해 정적 웹 사이트를 활성화하고 정적 웹 사이트에 대한 콘텐츠 전달을 가속화하려면 **정적 웹 사이트 원본 서버**를 선택하십시오.
**Origin-pull 인증**: 공개 읽기 버킷의 경우 Origin-pull 인증을 활성활 필요가 없으며 개인 읽기 버킷의 경우 CDN 서비스 인증을 추가해야 하며 Origin-pull 인증을 수동으로 활성화해야 합니다. 자세한 내용은 [Origin-pull 인증 활성화](https://intl.cloud.tencent.com/document/product/436/31505)를 참고하십시오.
**CDN 서비스 인증**: **CDN 서비스 인증 추가**를 클릭하여 CDN의 버킷 리소스 액세스 동의를 선택하십시오.
![](https://main.qcloudimg.com/raw/41e745800445225d042ef82c6febcc19.png)
(3) 구성 완료 후, **저장**을 클릭하여 CDN 가속을 활성화합니다.
![](https://main.qcloudimg.com/raw/5ffc31cb49410b4685316e75860c9385.png)
>!
>- 개인 읽기 버킷의 경우 origin-pull 인증과 CDN 권한 부여가 모두 활성화되면 CDN을 통해 원본 서버에 액세스하는 데 서명이 필요하지 않으며 CDN의 캐시된 리소스가 공중망을 통해 배포되므로 데이터 보안에 영향을 미칩니다. 따라서 CDN 인증을 활성화하는 것이 좋습니다.
>- 2022년 5월 9일 부터 Cloud Object Storage(COS)는 사용 이력이 없는 버킷에 대한 기본 CDN 가속 도메인 지원을 중단합니다. 이 변경 사항은 기본 CDN 가속 도메인을 사용 중이거나 사용 이력이 있는 버킷에는 영향을 미치지 않으나, 사용자 정의 CDN 가속 도메인으로 전환하는 것이 좋습니다. 사용자 정의 CDN 가속 도메인 작업 가이드는 [사용자 정의 CDN 가속 도메인 이름 활성화](https://intl.cloud.tencent.com/document/product/436/31506) 문서를 참고하십시오.
>
3. **사용자 지정 CDN 가속 도메인** 활성화
이미 ICP 비안이 완료된 **사용자 지정 도메인 이름**을 버킷에 바인딩하고 CDN 가속을 활성화할 수 있습니다.
>?COS 콘솔에 최대 10개의 사용자 정의 도메인 이름을 추가할 수 있습니다.
>
>(1) **사용자 지정 CDN 가속 도메인** 모듈에서 [도메인 이름 추가]를 클릭하여 ICP 비안이 완료된 사용자 지정 도메인 이름을 추가합니다.
>![](https://main.qcloudimg.com/raw/eda34cc24d82cebf109e3507a2ae142f.png)
>(2) 도메인 이름 추가:
>**도메인**: 바인딩할 사용자 지정 도메인 이름을 입력합니다(예: `www.example.com`). 도메인 이름 ICP 비안이 완료되어 있고 해당 CNAME이 DNS 서비스 제공 업체에서 구성되었는지 확인하십시오. 자세한 내용은[CNAME 설정](https://intl.cloud.tencent.com/document/product/228/3121)을 참고하십시오.
>**Origin-pull 인증**: 개인 읽기 버킷의 경우 원본 서버를 보호하기 위해 Origin-pull 인증을 수동으로 활성화하십시오.
>구성 완료 후 **저장**을 클릭합니다.
>![](https://main.qcloudimg.com/raw/e21189d91929209ded554581d267a505.png)
>!
>
>- 개인 읽기 버킷의 경우 origin-pull 인증과 CDN 권한 부여가 모두 활성화되면 CDN을 통해 원본 서버에 액세스하는 데 서명이 필요하지 않으며 CDN의 캐시된 리소스가 공중망을 통해 배포되므로 데이터 보안에 영향을 미칩니다. 따라서 CDN 인증을 활성화하는 것이 좋습니다.
>- 2022년 5월 9일 부터 Cloud Object Storage(COS)는 사용 이력이 없는 버킷에 대한 기본 CDN 가속 도메인 지원을 중단합니다. 이 변경 사항은 기본 CDN 가속 도메인을 사용 중이거나 사용 이력이 있는 버킷에는 영향을 미치지 않으나, 사용자 정의 CDN 가속 도메인으로 전환하는 것이 좋습니다. 사용자 정의 CDN 가속 도메인 작업 가이드는 [사용자 정의 CDN 가속 도메인 이름 활성화](https://intl.cloud.tencent.com/document/product/436/31506) 문서를 참고하십시오.
>
>(3) 구성이 저장되면 **CDN 인증** 열에 CDN 인증 스위치가 표시됩니다. 사용자 지정 도메인 이름에 대해 CDN 인증을 수동으로 활성화할 수 있습니다.
>**CDN 인증:** 악의적인 사용자의 도용을 방지하기 위해 타임스탬프 인증을 구성할 수 있습니다. 도메인 이름을 추가한 후 기능을 활성화할 수 있습니다.

COS 콘솔에서 CDN 가속을 구성하는 방법에 대한 자세한 내용은 [COS 도메인 관리 개요](https://intl.cloud.tencent.com/document/product/436/18424)를 참고하십시오.


## 권장 구성
1. 모든 설정을 완료한 후 [CDN 콘솔](https://console.cloud.tencent.com/cdn)로 이동하여 COS의 정적 리소스 파일을 CDN 노드로 미리 프리패치하면 원본 서버의 부담이 줄어들고 응답 및 다운로드가 빨라집니다. 자세한 내용은 [캐시 프리패치](https://intl.cloud.tencent.com/document/product/228/39000)를 참고하십시오.
2. 교차 원본 액세스 헤더를 구성합니다. 리소스의 원본 간 권한에 대한 자세한 내용은 [HTTP 응답 헤더 설정](https://intl.cloud.tencent.com/document/product/228/35320)을 참고하십시오.
3. 원본 서버에서 리소스가 수정된 경우 다시 프리패치하기 전에 캐시를 퍼지하는 것이 좋습니다. 자세한 내용은 [캐시 퍼지](https://intl.cloud.tencent.com/document/product/228/6299)를 참고하십시오.
