## 개요

Tencent Cloud StreamPackage는 Tencent Cloud가 새롭게 출시한 고품질의 비디오 캡슐화 및 원본 서버 플랫폼입니다. 전세계 사용자들에게 전문적이고 안정적이며 안전한 비디오 캡슐화 및 딜리버리 서비스 제공에 주력하고 있습니다. 비디오 패키지 전송의 난이도를 낮추고 원본의 엘라스틱(Origin Resiliency) 성능을 강화하였습니다. 이에 따라 비디오 공급자는 대용량 비디오 스트림 미디어를 안전하고 안정적으로 배포할 수 있습니다.

StreamPackage콘솔은 channel 차원에서 관리하며, 비디오 콘텐츠를 재구성하고 인코딩 및 압축된 비디오 트랙과 오디오 트랙을 특정 포맷으로 라이브 방송 원본 서버에 배치함으로써, 비디오 제공자가 대량의 비디오 스트림 미디어를 안정적으로 안전하게 배포할 수 있도록 합니다.

## 콘솔 개요

StreamPackage콘솔은 여러가지 유용한 기능과 쉽고 유연한 액세스 경험을 제공합니다. StreamPackage콘솔은 channel 차원에서 관리하며, 크게 Channel, Input, Endpoint, CDN 구성 4개 모듈로 나뉩니다.

![img](https://main.qcloudimg.com/raw/2d70be467d74639158d0be4ea94692d2.png)

## 전제 조건

- CDN 재생에 사용되는 도메인(Tencent Cloud 라이브 방송 CDN으로 배포해야 하는 경우)입니다.
- [Tencent Cloud 라이브 방송 서비스 활성화](https://console.cloud.tencent.com/live)가 완료되어 있어야 합니다
- [Tencent Cloud StreamPackage콘솔](https://console.cloud.tencent.com/mdp/channel)에 로그인합니다.

## 작업 순서

### 1.   가용존 선택

Tencent Cloud StreamPackage는 현재 인도 뭄바이, 태국 방콕, 한국 서울 세 개의 가용존을 제공하고 있으며 이 중에서 사용자의 소재 리전을 선택할 수 있습니다. 일본 도쿄 등 리전은 현재 배포 및 런칭을 준비 중에 있습니다. 기타 다른 가용존에 대한 배포를 요청하시려면 [고객센터](https://intl.cloud.tencent.com/contact-sales)로 문의주시기 바랍니다.

![img](https://main.qcloudimg.com/raw/d939a324316775e3ccef4c4658599b48.png)

### 2.   Channel 생성

Channel은 StreamPackage입력 스트림 및 출력 스트림의 기본 구성으로, 사용자는 생성된 Channel을 기반으로 기존 프로토콜의 라이브 방송 스트림을 입력할 수 있으며, 라이브 방송 스트림의 출력과 배포를 위한 엔드포인트(Endpoint)를 생성할 수도 있습니다.

1. [Create Channel]을 클릭하여 새로운 Channel을 생성합니다.

2. Channel Name을 입력하고 Channel을 선택한 뒤 프로토콜(HLS/DASH 지원)을 입력합니다.

![img](https://main.qcloudimg.com/raw/f545e69458ff80b55c6775219d574374.png)

3. 선택한 HLS/DASH 프로토콜 관련 매개변수를 입력합니다.

- **Max Segment Duration**은 해당 Channel로 푸시하는 HLS/DASH 포맷 스트림 ts/m4s 조각의 최대 멀티 파트 시간을 나타내며, 이 구성 매개변수의 기본값은 15s입니다.
- **Max Playlist Duration**은 해당 Channel로 푸시하는 HLS/DASH 포맷 스트림 m3u8/mpd 리스트의 최대 총 시간을 나타내며, 이 구성 매개변수의 수 기본값은 600s입니다. 푸시한 m3u8/mpd 리스트의 실제 상황에 따라 수정이 가능합니다.

>? 생성한 해당 Channel이 기본/보조 스트림을 동시에 푸시하는 경우, 기본 스트림 오류 발생 시 보조 스트림으로의 빠른 전환을 위해 이 구성 매개변수를 멀티 파트의 실제 최대 시간보다 약간 더 크게 설정하는 것을 권장합니다.

4. [Create]를 클릭하여 생성을 완료합니다.

### 3.   Channel 조회

#### Channel 정보 조회

생성 후 Channel의 상세 내용 페이지(Channel 이름 또는 우측의 [Info]를 클릭해도 Channel 상세 내용 페이지로 이동 가능)로 전환합니다. 상세 내용 페이지에는 Channel의 Name, ID(백그라운드에서 자동 생성), 지정된 입력 프로토콜 및 관련 구성 매개변수가 표시됩니다. 또한 지정된 프로토콜을 기반으로 2개의 입력 포인트(Input)가 자동 생성됩니다.

![img](https://main.qcloudimg.com/raw/d962c942d07f8303832d070c7d0d2a26.png)

#### Input 조회

Input은 Channel 입력의 기본 단위로, 백그라운드가 생성된 Channel을 기반으로 2개의 Input 노드와 해당 입력 URL을 자동으로 생성하면 사용자가 라이브 방송 스트림을 노드의 URL로 푸시할 수 있습니다.

![img](https://main.qcloudimg.com/raw/9fc040a6cb575be7411327476f0fe7a1.png)

Input 모듈은 Authentication 작업을 지원하며, 사용자는 각 입력 포인트에 대해 독립적으로 Authentication을 구성할 수 있습니다. 작업 열의 [Authentication]을 클릭한 뒤 팝업창에서 ![img](file:///C:/Users/JACKYS~1/AppData/Local/Temp/msohtmlclip1/01/clip_image012.jpg)Authentication 구성 열기를 클릭하면 백그라운드가 해당 입력 노드에 대해 자동으로 Username과 Password를 설정하고, http 인증 모드를 통해 인증을 진행합니다. [Rotate credentials]를 클릭하여 Authentication 구성을 완료합니다.

![img](https://main.qcloudimg.com/raw/6927ebe8232a26cb341aa1b69f008e45.png)

>! Rotate credentials를 진행하면 기존의 Channel credential이 무효화됩니다.

#### Endpoints 생성

사용자는 각 Channel에 대해 Origin-pull 풀 스트림 Endpoint 노드를 생성할 수 있습니다.

1. [Create Endpoint]를 클릭하여 노드를 생성합니다.

![img](https://main.qcloudimg.com/raw/ce143b55735dee33f7e708c5ea19f89a.png)

2. Endpoint Name을 입력합니다. Endpoint Type은 기본적으로 Channel의 입력 프로토콜과 동일합니다.

3. 사용자는 필요에 따라 IP 블랙리스트/화이트리스트, Authkey 등 기능의 활성화 여부를 선택할 수 있습니다.

- IP 블랙리스트/화이트리스트: 합법적인 IP를 고정하여 푸시 스트림을 진행하거나 비정상 IP의 푸시 스트림을 거부합니다.
- Authkey 구성 지원: X-TENCENT-PACKAGE를 통한 http-header의 인증을 지원합니다.

![img](https://main.qcloudimg.com/raw/d6a261b21e2c020365f6aa789c95e0dd.png)

4. [Create]를 클릭하여 설정을 저장하고 생성을 완료합니다. 생성된 Endpoint는 편집 및 삭제가 가능합니다. 사용자는 생성된 Endpoint URL을 기반으로 한 Origin-pull 풀 스트림을 통해 라이브 방송 스트림을 배포할 수 있습니다.

![img](https://main.qcloudimg.com/raw/219346607e144822c43173ba1e055905.png)

#### CDN 배포 구성

StreamPackage는 Channel에서의 라이브 방송 CDN 구성을 지원하며, 구성이 완료되면 StreamPackageChannel의 라이브 방송 스트림을 라이브 방송 CDN을 통해 직접 배포할 수 있습니다. 이를 위해 먼저 CSS를 활성화하고 StreamPackage와 CSS에 대한 **양방향 인증** 작업을 완료해야 합니다.

다음 내용을 열람하기 전에 관련 용어에 관한 다음 설명을 확인하십시오.

- 해당 기능을 통합하고 다중화함으로써 StreamPackageChannel의 라이브 방송 스트림이 LVB의 CDN을 통해 빠르게 배포 및 재생되도록 합니다.
- CDN 도메인/CDN 재생 도메인: LVB CDN의 재생 도메인으로, 라이브 방송 스트림의 배포에 사용됩니다.

1. LVB 서비스 활성화

Tencent Cloud CDN을 구성하기 전에 먼저 [Tencent Cloud 라이브 방송 서비스 활성화](https://console.cloud.tencent.com/live?from=product-banner-use-lvb) 여부를 확인하십시오.

2. StreamPackage의 LVB 액세스 권한 부여

StreamPackage콘솔로 돌아가서 CDN을 구성하여 배포할 Channel의 상세 내용 페이지를 열어 CDN 설정을 선택하고 하단의 [Authorization]을 클릭하여 StreamPackage에 LVB 액세스 권한을 부여하는 작업을 시작합니다.

>? StreamPackage에 LVB 액세스 권한을 부여하면 StreamPackage는 Channel에 대한 라이브 방송 재생 도메인을 생성할 수 있습니다.

![img](https://main.qcloudimg.com/raw/d0f1bc546937e0fbbb111bd6d97f2557.png)

**[Click here]을 클릭해StreamPackage에LVB CDN사용 권한을 부여합니다.** MDP 기능을 사용하려면 StreamPackage가 사용자의 일부 리소스에 액세스할 수 있도록 허용해야 하며, 서비스 역할을 통해 권한을 부여받은 리소스에 액세스하여 기능을 구현하게 됩니다. [Authorization Now]를 클릭하여 [역할 관리]로 전환하고, [Grant]를 클릭하여 StreamPackage에 관련 서비스 API에 대한 액세스 권한을 부여합니다.

![img](https://main.qcloudimg.com/raw/c2e6a9006094003091539f31d1d4c63c.png)

![img](https://main.qcloudimg.com/raw/a6476145b574ebbfe7f828dbbbfce984.png)

![img](https://main.qcloudimg.com/raw/b18b2fbb7440d557ee82093d44660258.png)

자동으로 StreamPackage콘솔로 돌아간 뒤 [Authorize completed]를 클릭하면, StreamPackage가 LVB CDN 사용 권한을 부여 받았다는 알림이 표시됩니다.

![img](https://main.qcloudimg.com/raw/2e7a6e29600485b593323658cf738b7d.png)

![img](https://main.qcloudimg.com/raw/3374604fff9c19ec580eb6a43af7f86e.png)

[Next]를 클릭하여 다음 단계로 넘어갑니다.

3. LVB에 StreamPackage액세스 권한 부여

**[Click here]를 클릭하여CDN콘솔로 전환하고 LVB CDN에MediaPackags사용 권한을 부여합니다. LVB콘솔의 권한 부여 상태가 [Activated]로 변경되었습니다.**

![img](https://main.qcloudimg.com/raw/3be8efcd4c8302b15df46be54daebed4.png)

![img](https://main.qcloudimg.com/raw/c63def0152b6d95901929b7abc093d59.png)

StreamPackage콘솔 인터페이스로 돌아간 뒤 [Complete]를 클릭하여 권한 부여 작업을 완료합니다.

![img](https://main.qcloudimg.com/raw/2616575aa0b6d56323eafcfac0aec9f8.png)

이때 LVB CDN에 StreamPackage사용 권한이 부여되었음이 표시됩니다. 하단의 [Authorization Completed]를 클릭하면 **StreamPackage와 LVB의 양방향 권한 부여 작업이 완료됩니다(즉, StreamPackage의 Channel을 통해CDN재생 도메인을 빠르게 생성할 수 있으며, LVB도Channel로Origin-pul하여 풀 스트림 및 배포가 가능함)**

![img](https://main.qcloudimg.com/raw/5e3084a78e0ce61a0a9eabd5a61c9a90.png)

4. CDN 재생 도메인의 빠른 구성

위와 같은 양방향 권한 부여 작업 완료 후, CDN 옵션 메뉴에서 [Edit Configuration]을 클릭하면 CDN을 빠르게 구성할 수 있습니다.

![img](https://main.qcloudimg.com/raw/4d2031b1fe8c42a1a05c7b619291e1dd.png)

CDN 재생에 사용할 도메인을 입력하고 [Confirm]을 클릭하면 구성이 완료됩니다.

![img](https://main.qcloudimg.com/raw/ee8a3bf7ab68b655bba010df76bac910.png)

![img](https://main.qcloudimg.com/raw/1fd6d414ef8fb41cee52c0a489c79395.png)

>?
>- 신규 생성한 재생 도메인 추가가 완료되면 시스템에서 자동으로 CNAME 도메인(뒤에 .liveplay.myqcloud.com이 붙음)을 할당합니다. CNAME 도메인은 직접 액세스할 수 없으며, 도메인 서비스 제공 업체에서 CNAME 설정을 완료하고, 설정이 적용되어야만 CSS 서비스를 이용할 수 있습니다. CNAME 작업 관련 상세 내용은 다음을 참조하십시오. [CNAME 설정](https://intl.cloud.tencent.com/document/product/267/31057)
>- StreamPackage에 구성된 CDN 재생 도메인의 재생 리전은 기본적으로 중국 대륙 외의 해외 리전(중국홍콩, 중국대만, 중국마카오 포함)으로 설정되어 있습니다. 중국 대륙에서 라이브 방송을 배포해야 하는 경우, 중국 대륙의 관련 법규에 따라 재생 도메인에 대한 ICP비안을 진행해야 합니다. [Go to LVB CDN console]을 클릭하여 라이브 방송 콘솔에서 더 많은 작업을 수행하십시오.

#### 구성된 재생 도메인을 통한 재생

StreamPackage의 Channel 구성을 CDN 재생 도메인에 바인딩한 후, Endpoint의 재생 주소의 도메인을 CDN 재생 도메인으로 변경하면 정상적으로 재생이 가능합니다.

예시:

Channel의 Endpoint 풀 스트림 주소가 다음과 같은 경우.

http://123456789.ap-seoul.StreamPackage.srclivepull.myqcloud.com/v1/017697a3513109df73abda3c4b26/017697a918bf09dfabc033b04d43/main.m3u8

CDN 재생 주소는 다음과 같습니다.

http://CDN 재생 도메인/v1/017697a3513109df73abda3c4b26/017697a918bf09dfabc033b04d43/main.m3u8

구성 완료 후 더욱 개선된 효과를 위해 고객센터를 통해 구성을 최적화할 수 있습니다.

>? 라이브 방송 CDN을 이용한 배포 및 재생으로 라이브 방송 트래픽 비용이 발생할 수 있습니다. 자세한 내용은 [CSS 요금](https://intl.cloud.tencent.com/document/product/267/2818)을 참조하십시오.

### 4.   Channel 편집 및 삭제

Channel 리스트 페이지에서 생성된 모든 Channel을 관리할 수 있습니다. 작업 열 왼쪽의 [Info]/[Edit]/[Delete]를 클릭하면 Channel 상세 내용을 조회할 수 있고 Channel을 다시 편집하거나 삭제할 수 있습니다. Channel에 이미 endpoint 노드가 있는 경우 삭제할 수 없습니다. 만약 Channel을 삭제해야 하는 경우에는 먼저 포함되어 있는 모든 Endpoint 노드를 삭제해야 합니다.

![img](https://main.qcloudimg.com/raw/bd7b3e8c0033d6591f5b61b2974dc12a.png)