CSS 서비스의 본질은 일종의 방송 프로세스로, 방송국의 라이브 방송 프로그램이 유선 TV 네트워크를 통해 수많은 가구로 전송되는 것과 유사합니다. 해당 프로세스를 완료하기 위해서는 CSS에 수집 및 스트리밍 디바이스(예: 카메라), CSS 서비스(예: 방송국의 유선 TV 네트워크)와 재생 디바이스(예: TV)가 필요합니다. 수집 및 스트리밍 디바이스와 재생 디바이스는 휴대폰, PC, Pad 등 스마트 단말기 및 Web 브라우저가 될 수 있으며, Tencent Cloud에서는 해당 디바이스의 푸시 스트리밍 소프트웨어의 완벽한 Demo를 제공하고 있습니다.

[](id:step1)
## 준비 작업
1. [Tencent CSS 서비스](https://console.cloud.tencent.com/live?from=product-banner-use-lvb)를 활성화합니다.
2. [[도메인 관리]](https://console.cloud.tencent.com/live/domainmanage)를 선택하고, [도메인 추가]를 클릭하여 ICP 비안을 받은 푸시 도메인을 추가합니다. 자세한 내용은 [자체 도메인 추가](https://intl.cloud.tencent.com/document/product/267/35970)를 참조하십시오.
>? CSS에서는 `xxx.livepush.myqcloud.com` 포맷의 기본 푸시 도메인을 제공합니다. 단, 정식 비즈니스에 해당 도메인을 푸시 도메인으로 사용하는 것은 권장하지 않습니다.

[](id:push_add)
## 푸시 스트리밍 주소 가져오기
CSS 콘솔의 [라이브 방송 툴박스]>[[주소 생성기]](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)에서 푸시 스트리밍 주소를 생성하고 해당 페이지에서 다음과 같이 설정합니다.
- 생성 유형을 **푸시 도메인**으로 선택합니다.
- 도메인 관리에 추가된 푸시 도메인을 선택합니다.
- AppName을 입력합니다. AppName은 동일한 도메인의 여러 App주소 경로를 구분하며, 기본값은 live로 설정되어 있습니다.
- 사용자 정의 스트림 이름 StreamName을 작성합니다. (예시: `liveteststream`)
- 주소 만료 시간을 선택합니다. (예시: ` 2019-10-18  23:59:59`)
- [주소 생성]을 클릭합니다. 

>!
>- 라이브 방송 보안을 위해 시스템에서 자동으로 푸시 스트리밍 인증을 활성화합니다. [도메인 관리](https://console.cloud.tencent.com/live/domainmanage)에서 수정할 푸시 도메인을 선택하고 오른쪽에 있는 [관리]를 클릭하여 도메인 상세 페이지의 [푸시 스트리밍 설정]에서도 인증 정보를 사용자 정의 설정할 수 있습니다. 푸시 스트리밍 주소 포맷은 다음과 같습니다.
`rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`
>-  상기 방법 이외에도 CSS 콘솔의 [[도메인 관리]](https://console.cloud.tencent.com/live/domainmanage)에서 푸시 도메인 선택 후 [관리]를 클릭하고, [푸시 스트리밍 설정]을 선택하여 푸시 스트리밍 주소의 만료 시간과 사용자 정의 스트림 이름 StreamName을 입력 후 [푸시 스트리밍 주소 생성]을 클릭하면 푸시 스트리밍 주소가 생성됩니다.
>- **장기적으로 유효한 푸시 스트리밍 주소**가 필요한 경우, [[도메인 관리]](https://console.cloud.tencent.com/live/domainmanage)에서 푸시 도메인 선택 후 [관리]를 클릭하고, [푸시 스트리밍 설정]을 선택하여 [푸시 스트리밍 주소 예시 코드]에 있는 예시 코드를 참고하여 연산해 생성합니다. 자세한 확인 방법은 [푸시 스트리밍 예시 코드는 어떻게 확인하나요?](https://intl.cloud.tencent.com/document/product/267/31059)를 참조하십시오.

[](id:live_push)
## 라이브 방송 푸시 스트리밍
비즈니스 시나리오에 따라 다음의 방식으로 라이브 방송 푸시 스트리밍을 구현할 수 있습니다.

[](id:pc)
### 시나리오1: PC에서의 푸시 스트리밍
PC(Windows/Mac)에서 푸시 스트리밍 시, 실제 상황에 따라 [OBS](https://obsproject.com/download) 또는 [XSplit](https://www.xsplit.com/zh-cn)을 선택하여 설치할 수 있습니다. OBS는 Windows/Mac/Linux 등의 시스템을 지원하며, 비디오 녹화 및 비디오 실시간 스트리밍 무료 오픈 소스 소프트웨어입니다. XSplit은 유료이며, 게임 라이브 방송 전용 설치 패키지가 있습니다. 게임 라이브 방송이 아닌 경우 BroadCaster 사용을 권장합니다.
![](https://main.qcloudimg.com/raw/dcb203971ac99415258ea0b0ee1529a8.png)
본 문서에서는 OBS를 설치하여 푸시 스트리밍하는 작업 방법을 예로 들어 소개하며, 작업 순서는 다음과 같습니다. 준비된 푸시 스트리밍 주소가 다음과 같다고 가정합니다.

```
rtmp://3891.livepush.myqcloud.com/live/3891_test?bizid=3891&txSecret=xxx&txTime=58540F7F
```


1. [OBS 공식 홈페이지](https://obsproject.com/download)로 이동하여 푸시 스트리밍 툴을 다운로드 및 설치합니다.
2. OBS를 실행하여 아래 툴 란에서 [소프트웨어 제어]>[설정] 버튼을 클릭하여 설정 화면으로 넘어갑니다.
3. [푸시 스트리밍]을 클릭해 푸시 스트리밍 설정 페이지로 이동하고, 다음과 같이 설정합니다.
  1. 서비스 유형을 사용자 정의로 선택합니다.
  1. 서버에 푸시 스트리밍 주소 앞쪽 부분을 입력합니다. (예시: `rtmp://3891.livepush.myqcloud.com/live/`)
  1. 스트림 키에 푸시 스트리밍 주소 뒤쪽 부분을 입력합니다. (예시: `3891_test?bizid=3891&txSecret=xxx&txTime=58540F7F`)
  1. 오른쪽 하단에 있는 [확인]을 클릭합니다.
![](https://main.qcloudimg.com/raw/7b5365a0be590c3694fbb6d0ded8e5e3.png)
4. 툴 란의 [소프트웨어 제어]>[푸시 스트리밍 시작]을 클릭하면 푸시 스트리밍 테스트가 진행됩니다. OSB 작업 방법에 대한 자세한 내용은 [OBS 푸시 스트리밍](https://intl.cloud.tencent.com/document/product/267/31569)을 참조하십시오.

[](id:web)
### 시나리오2: Web에서의 푸시 스트리밍
1. CSS 콘솔에 로그인합니다.
2. [보조 툴]>[[Web 푸시]](https://console.cloud.tencent.com/live/tools/webpush)을 선택합니다.
3. Web 푸시 스트리밍 페이지에서 다음을 설정합니다.
  1. 푸시 도메인을 선택합니다.
  2. AppName을 입력합니다. AppName은 동일한 도메인의 여러 App주소 경로를 구분하며, 기본값은 live로 설정되어 있습니다.
  2. 사용자 정의 스트림 이름 StreamName을 작성합니다. (예시: `liveteststream`)
  3. 만료 시간을 선택합니다. (예시: `2019-10-30 23:59:59`)
  4. [푸시 스트리밍 시작]을 클릭하고 카메라 호출 권한을 허용하면 푸시 스트리밍을 시작할 수 있습니다.

>! Web 푸시 스트리밍 기능은 디바이스에 카메라가 설치되어 있어야 하며 브라우저에서 Flash 플러그 인의 카메라 호출 권한을 지원해야 합니다.

![](https://main.qcloudimg.com/raw/9da7489bb2387049859131e792364124.png)

[](id:mobile)
### 시나리오3: 모바일에서의 푸시 스트리밍
1. 휴대폰으로 QR 코드를 스캔해 모바일 비디오 클라우드 툴 패키지 를 다운로드 및 설치합니다.
2. 툴 패키지를 실행해 [MLVB]>[카메라 푸시 스트리밍]을 선택합니다.
3. 휴대폰으로 QR 코드를 스캔하거나 [푸시 스트리밍 주소](#step1)를 입력합니다.
4. 왼쪽 하단에 있는 시작 버튼을 클릭해 푸시 스트리밍을 시작합니다.

>? 푸시 스트리밍 주소를 사전에 준비하지 않은 경우, 카메라 푸시 스트리밍 페이지에서 푸시 스트리밍 주소 오른쪽에 있는 [NEW]를 클릭하면 시스템에서 자동으로 푸시 스트리밍 주소를 입력하고 상응하는 재생 주소를 제공합니다. 해당 재생 주소를 통해 라이브 방송 푸시 스트리밍 효과를 확인할 수 있습니다.

[](id:sdk)
### 시나리오4: 라이브 방송 SDK에서의 푸시 스트리밍
현재 App에 라이브 방송 푸시 스트리밍 기능을 통합해야 하는 경우 다음 순서에 따라 빠르게 구현할 수 있습니다.
1. MLVB SDK 개발 패키지를 다운로드합니다.
2. 연결 문서를 참조하여 (iOS & Android)에 액세스합니다.

라이브 방송 SDK는 모바일 단말에서의 라이브 방송 통합 솔루션으로, 무료 소스 코드 형태로 CSS, VOD, IM, COS 등 몇 가지 서비스를 조합하여 사용자에게 적합한 라이브 방송 솔루션을 제공합니다. 


## FAQ
- [라이브 방송 재생은 어떻게 구현하나요?](https://intl.cloud.tencent.com/document/product/267/31559)
- [푸시 스트리밍 URL은 어떻게 자체적으로 조합하나요?](https://intl.cloud.tencent.com/document/product/267/38393)
- [링크 도용 방지는 어떻게 계산하나요?](https://intl.cloud.tencent.com/document/product/267/31560)

