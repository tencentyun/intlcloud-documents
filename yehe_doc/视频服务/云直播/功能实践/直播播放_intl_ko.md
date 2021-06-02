## 준비 작업
1. [Tencent CSS 서비스](https://console.cloud.tencent.com/live?from=product-banner-use-lvb)가 활성화되어 있고 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)이 완료되어야 합니다. 실명 인증을 하지 않은 사용자는 중국 내 CSS 인스턴스를 구매할 수 없습니다.
2. [CSS 콘솔](https://console.cloud.tencent.com/live/livestat)에 액세스하여 푸시 스트리밍 주소를 획득해 라이브 방송 푸시 스트리밍을 구현합니다. 자세한 방법은 [라이브 방송 푸시 스트리밍](https://intl.cloud.tencent.com/document/product/267/31558)을 참조하십시오.
3. [도메인 관리](https://console.cloud.tencent.com/live/domainmanage)를 선택해 [도메인 추가]를 클릭하여 ICP비안을 받은 도메인을 입력하고 [재생 도메인] 유형을 선택한 후 [저장]을 클릭합니다.
>!
>
>- 재생 도메인이 없는 경우 [[도메인 등록]](https://intl.cloud.tencent.com)을 통해 도메인을 구매할 있습니다. 다른 도메인 서비스 제공 업체를 통해서도 도메인을 구매할 수 있습니다.
4. [도메인 서비스 콘솔](https://console.cloud.tencent.com/domain)에 로그인하여 추가된 재생 도메인의 CNAME을 설정합니다. 자세한 방법은 [도메인 CNAME 설정](https://intl.cloud.tencent.com/document/product/267/31057)을 참조하십시오.

## 재생 주소 획득
CSS 콘솔의 [라이브 방송 툴박스]>[[주소 생성기]](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)에서 재생 주소를 생성하고 해당 페이지에서 다음과 같이 설정합니다.
- 생성 유형을 **재생 도메인**으로 선택합니다.
- 도메인 관리에 추가된 재생 도메인을 선택합니다.
- 푸시 스트리밍 주소와 동일한 StreamName을 입력합니다. 재생 주소 StreamName이 푸시 스트리밍 주소 StreamName과 일치해야만 해당 스트림을 재생할 수 있습니다.
- 주소 만료 시간을 선택합니다. (예시: `2019-12-13  23:59:59`)
- [주소 생성]을 클릭합니다.
![](https://main.qcloudimg.com/raw/a2f130098eb40df252956ffb3752d230.png)
>?상기 방법 이외에도 CSS 콘솔의 [[도메인 관리]](https://console.cloud.tencent.com/live/domainmanage)에서 재생 도메인 선택 후 [관리]를 클릭하고, [재생 설정]을 선택하여 푸시 스트리밍 주소의 만료 시간과 사용자 정의 스트림 이름 StreamName 입력 후 [재생 주소 생성]을 클릭하면 푸시 스트리밍 주소가 생성됩니다.

## 라이브 방송 재생
먼저 [라이브 방송 푸시 스트리밍](https://intl.cloud.tencent.com/document/product/267/31558)을 진행해야 하며, 푸시 스트리밍을 완료해야만 재생 주소를 통해 라이브 방송 화면을 확인할 수 있습니다. 비즈니스 시나리오에 따라 다음의 방식으로 라이브 방송 테스트를 진행할 수 있습니다.

### 시나리오 1: PC에서의 재생
[VLC](https://intl.cloud.tencent.com/document/product/267/32483), FFmepg, [TCPlayerDemo](https://imgcache.qq.com/open/qcloud/video/player/demo/player.html) 등의 툴을 사용해 재생할 수 있습니다.
### 시나리오2: 모바일 재생
1. [Tencent 비디오 클라우드 Demo](https://intl.cloud.tencent.com/document/product/1071/38147)를 다운로드 및 설치합니다.
2. [MLVB]>[라이브 방송 풀 스트리밍]을 선택합니다.
3. 입력창에 재생 주소를 입력하거나 재생 주소 QR코드를 스캔하여 입력합니다.
4. 왼쪽 하단에 있는 재생 버튼을 클릭하여 재생합니다.

>? App에서 푸시 스트리밍/재생하는 경우 [MLVB SDK](https://intl.cloud.tencent.com/product/mlvb)를 통합하여 CSS 서비스와 결합해 사용할 수 있으며, MLVB SDK는 RTMP, HTTP-FLV, HLS 재생 프로토콜을 지원합니다.

### 시나리오4: Web 재생
SDK의 TCPlayerLite로 재생하는 것을 권장합니다. 해당 플레이어는 Tencent Cloud의 강력한 백그라운드 능력과 AI기술을 기반으로 뛰어난 비디오 라이브 방송 및 VOD 재생 기능을 제공합니다. Player+는 Tencent CSS, VOD 서비스를 융합하여 원활하고 안정적인 재생 성능을 자랑하며 광고 삽입, 데이터 모니터링 등의 기능이 통합되어 있습니다.
>! 현재 시중의 대다수 모바일 브라우저는 HTTP-FLV 재생을 지원하지 않으므로, Web 재생 시 PC 브라우저에서는 HTTP-FLV 프로토콜, 모바일 브라우저에서는 HLS 프로토콜을 사용한 라이브 방송 스트리밍 재생을 권장합니다.


## FAQ
- [어떤 재생 프로토콜을 지원하나요?](https://intl.cloud.tencent.com/document/product/267/7968)
- [재생 주소는 어떻게 구성되나요?](https://intl.cloud.tencent.com/document/product/267/7968)
- [재생 트랜스 코딩은 어떻게 사용하나요?](https://intl.cloud.tencent.com/document/product/267/35598)
- [타임 시프트 다시보기는 어떻게 사용하나요?](https://intl.cloud.tencent.com/document/product/267/35598)
- [HTTPS 재생은 어떻게 사용하나요？](https://intl.cloud.tencent.com/document/product/267/35598)
- [해외 가속 노드 재생은 어떻게 사용하나요?](https://intl.cloud.tencent.com/document/product/267/35598)
- [재생 링크 도용 방지 기능은 어떻게 활성화하나요?](https://intl.cloud.tencent.com/document/product/267/35598)

