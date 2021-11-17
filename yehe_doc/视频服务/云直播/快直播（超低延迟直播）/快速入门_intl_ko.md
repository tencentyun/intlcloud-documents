본 튜토리얼은 LEB 서비스를 빠르게 이해할 수 있도록 안내합니다. 혼동을 피하기 위해, LEB를 이용하기 전 LEB [가격 리스트](https://intl.cloud.tencent.com/document/product/267/2819)를 미리 읽어보시고 **유료 항목** 및 **가격**을 알아보시기를 권장합니다.

[](id:step0)
## 준비 작업
1. [Tencent Cloud 계정](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fproduct%2Flvb)을 생성하고 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)을 완료합니다. 실명 인증을 하지 않은 사용자는 중국 내 CSS 인스턴스를 구매할 수 없습니다.
2. [Tencent Cloud CSS 서비스 활성화 페이지](https://console.cloud.tencent.com/live?from=product-banner-use-lvb)에서 <Tencent Cloud 서비스 약관>에 체크하여 동의하고 **활성화 신청**을 클릭하면 CSS 서비스가 활성화됩니다.
>?  
>- CSS 서비스 활성화 신청 후 중국 국내 재생 트래픽 20GB를 무료 체험용으로 제공합니다.
>- 도메인 구성은 LVB와 동일하며, LVB에 액세스한 경우, [4단계: 재생 주소 획득](#step4) 부분에서 LEB 풀 스트림에 대해 알아볼 수 있습니다.

[](id:step1)

## 1단계: 도메인 추가
CSS 서비스 이용 시 **푸시 스트림 도메인**과 **재생 도메인**을 포함하는 최소 **2**개의 도메인이 필요하며, 푸시 스트림과 재생은 동일한 도메인을 사용할 수 없습니다.
[**외부 도메인 추가**](https://intl.cloud.tencent.com/document/product/267/35970)를 통해 ICP비안이 완료된 외부 도메인을 추가할 수 있습니다.

1. 도메인을 준비합니다. 만일 중국에서 사용할 경우 도메인 ICP비안을 완료해야 합니다.

2. CSS 콘솔에 로그인하여 [ **도메인 관리**](https://console.cloud.tencent.com/live/domainmanage) 페이지로 이동합니다.

3. 외부 도메인 추가 페이지로 이동한 후 **도메인 추가**를 클릭합니다.

   ![](https://main.qcloudimg.com/raw/771bbce97962dcd1cffdd94324941280.png)
>?
>- CSS에서 기본적으로 테스트 도메인 `xxxx.livepush.myqcloud.com`을 제공합니다. 해당 도메인으로 푸시 스트림을 테스트할 수 있습니다. 단, 정식 서비스에서 해당 도메인을 푸시 도메인으로 사용하는 것은 권장하지 않습니다.
>- 도메인 추가가 완료되면 **도메인 관리**의 도메인 목록에서 도메인 정보를 조회할 수 있습니다. 이미 추가된 도메인 관리가 필요한 경우, [도메인 관리](https://intl.cloud.tencent.com/document/product/267/31056)를 참고하시기 바랍니다.
>- 라이브 방송 도메인에 관한 자세한 내용은 [라이브 방송 기본 관련](https://intl.cloud.tencent.com/document/product/267/7968)을 참고하시기 바랍니다.
5. 도메인 추가가 완료되면 시스템에서 자동으로 하나의 CNAME 도메인(`.tlivecdn.com` 또는 `.tlivepush.com`을 접미사로 함)을 할당합니다. CNAME 도메인은 직접 액세스할 수 없으며, 도메인 서비스 공급자 측에서 CNAME 구성을 완료한 후 구성이 적용되면 CSS 서비스를 이용할 수 있습니다. DNS 서비스 제공 업체가 Tencent Cloud인 경우의 CNAME 레코드 추가 작업 단계는 다음과 같습니다. [](id:step1_1_1)
    1. [도메인 서비스 콘솔](https://console.cloud.tencent.com/domain)에 로그인합니다.
    2. CNAME을 추가할 도메인을 선택하고 **리졸브**를 클릭합니다.
    3. 도메인 리졸브 페이지에서 **레코드 추가**를 클릭합니다.
    4. 신규 열에 도메인 접두사를 호스트 레코드로 입력합니다. 기록 유형을 CNAME으로 선택하고 CNAME 도메인을 기록값으로 입력합니다.
    5. **저장**을 클릭하면 CNAME 레코드가 추가됩니다.
>!
>- CNAME 성공 후 적용되기까지 일정 시간이 소요되며, CNAME 실패 시 CSS를 이용할 수 없습니다.
>- 도메인 CNAME 성공 시 CSS 콘솔의 [**도메인 관리**](https://console.cloud.tencent.com/live/domainmanage) 목록의 도메인 CNAME 주소 상태 표시가 ![](https://main.qcloudimg.com/raw/0fc346399ae095d69113d4944e511a20.png)로 변경됩니다.
>- CNAME 작업 후 점검에 계속 실패하는 경우, 도메인 등록 서비스 제공 업체에 문의하시기 바랍니다.
>- 다른 DNS 서비스 제공 업체를 이용하는 경우 자세한 내용은 [도메인 CNAME 설정](https://intl.cloud.tencent.com/document/product/267/31057)을 참고하시기 바랍니다.

## 2단계: 푸시 스트림 주소 가져오기

1. **라이브 방송 툴박스**>[**주소 생성기**](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)를 선택합니다.
2. 주소 생성기 페이지에서 다음과 같이 설정합니다.
   1. 생성 유형 선택: **푸시 스트림 도메인**을 선택합니다.
   2. 도메인 관리에서 이미 추가된 푸시 스트림 도메인을 선택합니다.
   3. 사용자 정의 스트림 이름 StreamName을 입력합니다. (예시: `liveteststream`)
   4. 주소 만료 시간을 선택합니다. 예: `2021-05-25  23:59:59`.
   5. **주소 생성**을 클릭하여 푸시 스트림 주소 생성을 완료합니다.
![](https://main.qcloudimg.com/raw/5a377614d5da22c5193bef68f4a3a6e7.png)

>? 
>- 푸시 스트림 주소 구조는 다음과 같습니다. `live`는 AppName 기본값이고, `txSecret`은 푸시 스트림 재생을 위한 서명이며, `txTime`은 푸시 스트림 주소의 유효 시간입니다.
>- 상기 방법 이외에도 CSS 콘솔의 [**도메인 관리**](https://console.cloud.tencent.com/live/domainmanage)에서 푸시 스트림 도메인 선택 후, **관리**를 클릭하고, **푸시 스트림 설정**을 선택합니다. 푸시 스트림 주소의 만료 시간과 사용자 정의 스트림 이름 StreamName 입력 후, **푸시 스트림 주소 생성**을 클릭하면 푸시 스트림 주소가 생성됩니다.
>- 실제 작업 수요에 따라 푸시 스트림 주소를 생성하기 전에 대응하는 [기능 템플릿](https://intl.cloud.tencent.com/document/product/267/31069) 생성을 설정하여 푸시 스트림 도메인에 연동할 수 있습니다. 부가 기능 가격은 [가격 리스트](https://intl.cloud.tencent.com/document/product/267/2819)를 참고하시기 바랍니다.

[](id:step3)
## 3단계: 라이브 방송 푸시 스트림

서비스 시나리오에 따라 생성한 푸시 스트림 주소를 해당 푸시 스트림 소프트웨어에 입력하십시오.
- PC용 푸시 스트림은 OBS 사용을 권장하며, 먼저 [OBS 플러그 인 설정](https://intl.cloud.tencent.com/document/product/267/42131)이 필요합니다. 플러그 인 설정 후 후속 작업은 [OBS 푸시 스트림](https://intl.cloud.tencent.com/document/product/267/31569)을 참고하십시오.
- Web에서의 푸시 스트림은 **보조 툴**>[**Web 푸시**](https://console.cloud.tencent.com/live/tools/webpush) 사용을 권장합니다. 푸시 스트림이 필요한 도메인을 선택하고 사용자 정의 스트림 이름 StreamName을 입력합니다. 주소 만료 시간을 선택하고 카메라를 켠 후 **푸시 스트림 시작**을 클릭합니다.    
- 모바일 푸시 스트림은 [Tencent Cloud 툴킷 App](https://intl.cloud.tencent.com/document/product/1071/38147)를 다운로드하여 설치하고, **MLVB**>**푸시 스트림 데모(카메라 푸시 스트림)** 열기 및 선택 후, 수동 입력 또는 QR 코드 스캔을 통해 주소 입력란에 푸시 스트림 주소를 입력하고, **푸시 스트림 시작**을 클릭합니다.

>? 
>- 맞춤화된 App에서 Tencent Cloud가 제공하는 [MLVB SDK](https://intl.cloud.tencent.com/document/product/1071)를 통합해 푸시 스트림 기능을 구현할 수 있습니다.
>- LEB Web 방안은 B-프레임 디코딩 및 재생을 지원하지 않습니다. 자세한 내용은 [B-프레임 정보](#b_frame)를 참고하시기 바랍니다.

[](id:step4)
## 4단계: 재생 주소 가져오기

1. 푸시 스트림 완료 후, [**스트림 관리**](https://console.cloud.tencent.com/live/streammanage)> **온라인 스트림**을 선택하여 푸시 스트림 주소 상태를 조회하고, **테스트**를 클릭해 온라인에서 재생 및 시청합니다.
2. **라이브 방송 툴박스**>[**주소 생성기**](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)를 선택하여 재생 주소를 가져옵니다. 해당 페이지에서 다음과 같이 설정합니다.
   1. 생성 유형을 선택합니다. 예: 재생 도메인.
   2. 도메인 관리에 이미 추가한 재생 도메인을 선택합니다.
   3. 푸시 스트림 주소와 동일한 StreamName을 입력합니다. 재생 주소 ` StreamName`은 반드시 푸시 스트림 주소 ` StreamName`과 일치해야 해당 스트림을 재생할 수 있습니다.
   4. 주소 만료 시간을 선택합니다. 예: `2021-05-25  23:59:59`.
   5. 실제 필요에 따라 바인딩할 트랜스 코딩 템플릿을 선택합니다. (트랜스 코딩 템플릿을 선택하면 트랜스 코딩된 라이브 방송 재생 주소가 생성됩니다. 원본 라이브 방송 스트림 재생은 주소 생성을 위해 트랜스 코딩 템플릿을 선택할 필요가 없습니다.)
   5. **주소 생성**을 클릭하여 재생 주소를 생성합니다. LEB URL 형식은 `webrtc://domain/path/stream_id`입니다.
![](https://main.qcloudimg.com/raw/5025e22cd8c4c555d7de3e0360e13d11.png)
3. 서비스 시나리오에 따라 다음의 방식으로 라이브 방송 스트림이 정상적으로 재생되는지 테스트할 수 있습니다.
   - **Web 라이브 방송 스트림 테스트**: [WebRTC Live Demo](https://tcplayer.vcube.tencent.com/webrtc-demo/index.html) 툴 사용을 통한 재생 체험을 권장합니다.
>?
>- WebRTC Live Demo는 다중 해상도 기능을 지원합니다. CSS 콘솔의**기능 설정**>[**라이브 방송 트랜스 코딩**](https://console.cloud.tencent.com/live/ config/transcode)에서 HD, SD 트랜스 코딩 템플릿을 설정할 수 있습니다. 트랜스 코딩 템플릿이 있는 WebRTC 스트림 주소를 Demo의 해당 열에 입력한 다음 재생을 테스트합니다(이 기능을 테스트할 필요가 없는 경우, Demo에 WebRTC 원본 스트림 하나만 입력하면 됩니다).
>- 라이브 방송 트랜스 코딩 운영 가이드 및 트랜스 코딩 과금 관련 내용은 [라이브 방송 트랜스 코딩](https://intl.cloud.tencent.com/document/product/267/31071) 문서를 참고하시기 바랍니다.
   - **모바일 라이브 방송 스트림 테스트**: [비디오 클라우드 툴킷](https://intl.cloud.tencent.com/document/product/1071/38147)을 다운로드하고, **LEB 재생** 열기 및 선택 후, 수동 입력 또는 QR 코드 스캔을 통해 **푸시 스트림 체험**에서 획득한 LEB 재생 주소 입력하고, 재생 버튼을 클릭하여 재생 및 시청합니다.
>? App에서 푸시 스트림을 진행해야 하는 경우 [MLVB SDK](https://intl.cloud.tencent.com/product/mlvb)를 통합하여 LEB 서비스와 함께 사용할 수 있습니다. 사용 중 문제가 발생하면 [FAQ](#que)을 참고하시기 바랍니다.

## 5단계: LEB 제품 액세스
-**모바일 솔루션**: B-프레임 디코딩 및 AAC 오디오 형식을 지원합니다. 현재 MLVB SDK에 통합되었으며, 연결 방법은 [LEB 풀 스트림](https://intl.cloud.tencent.com/document/product/1071/41875)을 참고하십시오.
-**Web 솔루션**: TCPlayerLite 플레이어에 통합되었습니다.

[](id:que)
## FAQ
[](id:play_url)
### 풀 스트림 URL 생성
LEB 풀 스트림 URL은 기본적으로 Tencent Cloud CSS 풀 스트림 URL과 동일하며 Tencent Cloud CSS 풀 스트림 URL 앞의 'rtmp'를 'webrtc'로 바꾸기만 하면 됩니다.

LEB 풀 스트림 URL 형식은 **`webrtc://domain/path/stream_id`**이며, [링크 도용 방지 계산](https://intl.cloud.tencent.com/document/product/267/31560)이 필요한 경우, 풀 스트림 URL 형식은 **`webrtc://domain/path/stream_id?txSecret=xxx&txTime=xxx`**입니다. Tencent Cloud CSS 풀 스트림 URL 생성은 [재생 주소 가져오기](#step4)를 참고하십시오.

>? 다른 해상도와 비트레이트의 스트림을 풀링해야 하는 경우 트랜스 코딩 스트림을 풀링할 수 있으며, 트랜스 코딩된 스트림의 URL 생성은 [라이브 방송 캡슐화 전환 및 트랜스 코딩](https://intl.cloud.tencent.com/document/product/267/31561)을 참고하시기 바랍니다.

[](id:b_frame)
### B-프레임 관련
LEB Web 방안은 **B-프레임 디코딩 및 재생을 지원하지 않습니다**. 원본 스트림에 B-프레임이 있는 경우 백그라운드에서 B-프레임을 제거하기 위해 자동으로 트랜스 코딩을 진행하지만, 이로 인해 트랜스 코딩 딜레이가 추가 발생하고, ** 트랜스 코딩 비용이 발생합니다**. B 프레임이 포함된 스트림은 최대한 푸시하지 않는 것을 권장합니다. 사용자는 푸시 스트림 소프트웨어(예: OBS)의 비디오 인코딩 매개변수를 조정하여 B 프레임을 제거할 수 있습니다. OBS를 사용하여 푸시 스트림하는 경우 설정을 통해 B-프레임을 비활성화할 수 있습니다. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/b28d5919589364e6a1f78d62e0b58c47.png)

[](id:a_transcoding)
### 오디오 트랜스 코딩 관련
Web 브라우저 풀 스트림은 표준 WebRTC 프로토콜만 지원하며, AAC 오디오 형식은 지원하지 않으므로 푸시 스트림의 AAC 오디오 형식을 OPUS 오디오 형식으로 변환하여 재생해야 합니다. 이로 인해 [오디오 트랜스 코딩](https://intl.cloud.tencent.com/document/product/267/39604) 요금이 발생할 수 있습니다.
