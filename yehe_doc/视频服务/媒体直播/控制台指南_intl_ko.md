## 개요

Tencent Cloud StreamLive는 Tencent Cloud가 새롭게 선보이는 고품질의 스트림 처리 플랫폼입니다. 방송 수준의 실시간 온라인 스트림 미디어 처리 서비스 제공이 가능합니다. Tencent Cloud의 독자적인 고성능 비디오 인코딩 및 압축 알고리즘을 채택하여, 더욱 개선된 시청 경험을 보장하면서도 전송 트래픽은 절약하는 데 주력하고 있습니다.

StreamLive 콘솔은 Channel 차원의 관리를 통해 사용자가 고품질의 비디오 스트림을 생성하여 여러 유형의 디바이스에 배포할 수 있도록 합니다.

## 콘솔 개요

StreamLive 콘솔은 Channel 차원에서 관리합니다. 크게 보안 그룹(Security Groups), 채널 입력(Input), 채널 관리(Channel) 세 가지 모듈로 구성되어 있습니다. 보안 그룹은 입력 소스에 대한 보안 검증을 관리하고, 채널 입력은 채널 입력 소스의 프로토콜 및 입력 방식에 대한 설정을 담당합니다. 채널은 StreamLive 핵심 모듈로써 기존 설정에 따라 입력 스트림에 대해 트랜스 코딩, 리먹싱 등의 비디오 처리 작업을 수행한 뒤 이를 지정된 타깃 리전 또는 CAS로 출력합니다.

![](https://main.qcloudimg.com/raw/e76d930fd73f010632e9e4571a8351d9.png)

## 전제 조건

[Tencent Cloud StreamLive 콘솔](https://console.cloud.tencent.com/mdl/security)에 로그인합니다.

## 작업 순서

### 1.   리전 선택

Tencent Cloud StreamLive는 현재 인도 뭄바이, 태국 방콕, 한국 서울 세 개의 가용존을 제공하고 있으며 이 중에서 사용자의 소재 리전을 선택할 수 있습니다. 일본 도쿄 등의 리전은 현재 배포 및 런칭 준비 중입니다. 기타 다른 가용존에 대한 배포를 요청하려면 [고객센터](https://intl.cloud.tencent.com/contact-sales)로 문의하시기 바랍니다.

![](https://main.qcloudimg.com/raw/c9da8ddd469f557487c5b6d943ef69af.png)

### 2.   보안 그룹 생성

보안 그룹은 입력 소스 IPV4 주소의 유효성을 확인하는 용도로 사용되며, 보안 그룹 설정을 통해 StreamLive 채널을 보다 안전하게 입력할 수 있습니다.

[Security Group Management] 메뉴를 선택하고 [Create Security Group]을 클릭하여 보안 그룹을 생성합니다. Name을 입력한 뒤, CIDR 포맷의 문자열을 새로운 입력 보안 그룹에 추가하고 쉼표 또는 줄 바꿈 부호로 구분해 줍니다. 입력 후 [Confirm]을 클릭해 생성을 완료합니다.

![](https://main.qcloudimg.com/raw/e5c7365ba3724802b2013b3c25cdc07b.png)

>?
>- 보안 그룹의 상태에는 idle과 occupied가 있습니다. 
>- idle은 현재 보안 그룹이 연결되어 있지 않으며 편집이나 삭제가 가능한 상태임을 나타냅니다.
>- occupied는 현재 보안 그룹이 channel-input과 연결되어 있음을 나타내며, 이 경우 보안 그룹을 편집할 수는 있으나 삭제할 수는 없습니다.
>- 콘솔은 기본적으로 최대 5개의 보안 그룹을 생성할 수 있도록 설정되어 있습니다. 더 많은 보안 그룹을 생성해야 하는 경우, [티켓 제출](https://console.cloud.tencent.com/workorder)을 통해 Tencent Cloud 고객 지원팀에 문의하시기 바랍니다.

### 3.   입력 생성

[Input Management] 메뉴를 선택하고 [Create Input]를 클릭하여 채널 입력을 생성합니다.

채널 입력은 StreamLive의 미디어 스트림 입력 터널로, 일반적으로 하나의 보안 그룹과 하나의 StreamLive 채널과 연결됩니다. 채널 입력은 현재 RTP, RTP-FEC, RTMP, UDP, HLS, HTTP-MP4 등의 프로토콜 입력을 지원하며, PULL과 PUSH 두 가지 입력 방식을 제공하고 있습니다.

모든 채널은 하나의 보안 그룹 및 하나의 채널에 연결할 수 있으며, 채널과 연결된 입력 상태는 attached로 표시됩니다.

![](https://main.qcloudimg.com/raw/eed9a73cc25fc646b1f601ac545ccc0e.png)

>?
>- 콘솔은 기본적으로 최대 5개의 input을 지원합니다.
>- 입력된 미디어 소스는 현재 최소 1개의 비디오 데이터 채널을 포함해야 합니다.
>- MPEG-TS 멀티 터널을 사용하면 최대 8개 터널의 동시 전송이 가능합니다.

### 4.   StreamLive 채널 생성

1. [Channel Management] 메뉴를 선택하고 [Create Channel]을 클릭하여 채널 입력을 생성합니다.

2. 사용자 정의 채널 이름. 사용자가 생성한 채널을 식별하는 데 사용됩니다. [Next Step]을 클릭하여 다음 단계로 넘어갑니다.

![](https://main.qcloudimg.com/raw/824d8ad80106fb65f69df5dffae7bd0b.png)

3. 입력 소스 추가. 생성한 채널 입력 중 1개 또는 다중 선택하여 StreamLive 채널에 입력 소스로 추가합니다. **정상적인 상황에서****,** **기본적으로 처음의 입력이 입력 소스로 사용됩니다**. 다른 입력 소스는 액티브/스탠바이 재해 복구(Failover) 또는 시간 계획(Plan)에서 사용될 수 있습니다. 하나의 채널에 최대 5개의 입력 소스를 바인딩할 수 있으며, 그 중 PUSH 입력은 최대 2개입니다.

![](https://main.qcloudimg.com/raw/72974873310b8f07ea0acc09ce3c3f64.png)

다른 유형의 입력 소스는 [settings]를 클릭하여 연 후 아래의 설정을 진행하십시오.

a.    [오디오 셀렉터] 사용자의 RTP_PUSH / RTP-FEC_PUSH / UDP_PUSH 입력 소스에 여러 개의 오디오 스트림이 있는 경우에는 MEPGTS에 캡슐화된 오디오 PID를 바탕으로 셀렉터를 생성하여, 차후 출력 설정 페이지에서 여러 오디오 언어를 구성할 수 있도록 지원합니다.

![](https://main.qcloudimg.com/raw/8ea9e3a78e57242e446f4ab2f4cd6850.png)

>!
>- 여기에서 PID는 반드시 입력 오디오 스트림의 PID와 동일해야 하며, 상이할 경우 트랜스 코딩 작업이 실패할 수 있습니다.
>- 처음 입력(첫 행의 입력)만이 오디오 셀렉터 설정을 진행할 수 있으며, 다른 상황에서 해당 설정은 유효하지 않습니다. Plan의 입력 전환으로 인해 해당 입력 소스가 사용된 경우, 시스템은 기본적으로 같은 종류의 오디오 트랙을 선택하여 트랜스 코딩을 진행합니다.
>- 입력 소스가 액티브/스탠바이 재해 복구를 설정한 경우, 스탠바이 스트림은 자동으로 액티브 스트림과 일치하는 오디오 셀렉터를 유지하여 액티브/스탠바이 전환 시 오디오 트랜스 코딩 가용성을 보장합니다.

b.    [풀 스트림 설정] 사용자는 MP4_PULL / HLS_PULL 입력 소스에 풀 스트림 푸시의 소스 동작을 설정할 수 있습니다. 두 가지 모드가 있으며 LOOP는 순환하여 풀 스트림하고, ONCE는 풀 스트림이 한 번 종료된 후 자동으로 입력 스트림이 끊어집니다.

![](https://main.qcloudimg.com/raw/a721d60a7263dddeab3927b3331cfaa2.png)

c.    [액티브/스탠바이 재해 복구 설정] 사용자는 RTMP_PUSH / RTP_PUSH 입력 소스에 액티브/스탠바이 재해 복구를 설정하여 액티브 스트림에 이상이 생긴 경우 자동으로 스탠바이 스트림으로 전환되어 입력할 수 있습니다. 액티브/스탠바이 재해 복구 활성화를 선택한 후, 한 개의 입력 소스를 선택하여 현재 입력 소스의 스탠바이 스트림으로 사용할 수 있습니다. 동시에 장애 검증 시간(액티브 스트림에 이상이 생긴 후에 액티브/스탠바이 재해 복구를 재활성화할 때까지의 기본 대기 시간은 3000ms)과 입력 스트림 설정(액티브 스트림 복구 후 액티브 스트림 입력으로 재전환 여부로서 PRIMARY_PREFERRED는 액티브 스트림 우선, EQUAL_PREFERRED은 액티브/스탠바이의 우선순위 같음)을 지정할 수 있습니다.

![](https://main.qcloudimg.com/raw/588efa49ee40b158793421c6ced77319.png)

![](https://main.qcloudimg.com/raw/ebc0d3305a94534edaf97d09ecf18f9c.png)

>?
>- 최대 한 쌍의 액티브/스탠바이 스트림을 설정할 수 있으며, 액티브 스트림과 스탠바이 스트림의 입력 소스 유형과 터널 수는 같아야 합니다.
>- 액티브/스탠바이 관계 확인 후, 스탠바이 스트림의 액티브/스탠바이 재해 복구 ON/OFF가 OFF로 자동 잠금됩니다. 즉, 스탠바이 스트림을 추가할 수 없습니다. 액티브/스탠바이 관계 조정이 필요한 경우(예를 들어, 액티브/스탠바이 교환) 현재의 액티브/스탠바이 관계를 해제/변경 후 다시 설정해야 합니다.
>- 액티브/스탠바이 재해 복구 설정 후, 액티브 스트림과 스탠바이 스트림 입력명 옆에 'Primary'와 'Backup'을 표시하는 필드가 나타납니다.
>- 스탠바이 스트림은 자동으로 액티브 스트림 아래로 순서가 조정됩니다.

 

위의 설정 외에, 입력 시 아래의 작업도 진행할 수 있습니다.

- [details]를 클릭하여 주소 입력 등 입력 소스의 기본 정보를 조회합니다.
- [Set as First]를 클릭하여 최상위 항목을 입력하고, 이를 기본 입력으로 설정합니다. 주의사항: 스탠바이 스트림은 최상위 항목이 될 수 없습니다.
- [delete]를 클릭하여 입력 소스를 삭제합니다.

[Next Step]을 클릭하여 다음 단계로 넘어갑니다.


4. 출력 그룹을 설정합니다.

a.     여러 출력 그룹 설정. StreamLive는 단일 채널의 여러 Output Group에 대한 출력을 지원합니다. 우측 상단의 플러스를 클릭하여 여러 Output Group을 추가합니다.

![](https://main.qcloudimg.com/raw/e6af7ba8a52e288e0d02dc3bea54871e.png)

b.     출력 그룹의 이름 및 유형. 현재 Output Group의 이름과 유형을 설정합니다. 현재 StreamLive는 HLS/DASH 포맷의 출력을 지원하며, HLS 파일을 출력해 Tencent Cloud COS로의 보관(자세한 작업 방식은 제6절 참조)을 지원합니다. 또한 Tencent Cloud StreamPackage와 함께 사용하여 HLS/DASH 포맷의 라이브 방송 스트림을 그대로 동일 계정의 StreamPackage에서 출력할 수 있도록 지원(자세한 작업 방식은 제7절 참조)함으로써, 사용자가 자체 원본 서버를 구축하여 대규모 라이브 방송을 안정적으로 배포할 수 있도록 해줍니다.

>?
>- Tencent Cloud COS에 관한 자세한 내용은 다음을 참조하십시오.[COS 세부정보](https://intl.cloud.tencent.com/document/product/436/6222)
>- Tencent Cloud StreamPackage에 대한 자세한 내용은 다음을 참조하십시오.[StreamPackage 세부정보](https://intl.cloud.tencent.com/document/product/1063/37495)

![](https://main.qcloudimg.com/raw/6b87cbe42011cc98c045af99369348a3.png)

c.     CDN 푸시 주소 설정. HLS 또는 DASH 프로토콜 유형을 선택하여 출력하는 경우, 여기에 CDN의 푸시 스트림 주소를 입력할 수 있습니다. 푸시 스트림 주소를 인증해야 하는 경우에는 인증 정보를 입력할 수 있습니다.

![](https://main.qcloudimg.com/raw/8fb39dfab5a32ea34444b9a6f1e4edab.png)

d.     Segment 설정. Manifest 파일에서 Segment 길이와 Segment 수를 설정합니다. 태그 파일에 utc 시간을 삽입해야 하는 경우, Pdt 스위치를 켜고 utc 시간 삽입 간격을 설정할 수 있습니다.

![](https://main.qcloudimg.com/raw/36b16a1dda37c530d7b8f497688a93d9.png)

e.     DRM 설정. Tencent Cloud StreamLive는 사용자 정의 DRM을 지원하므로 실제 필요에 따라 선택할 수 있습니다.

![](https://main.qcloudimg.com/raw/fbb528cc453be167497d4d7eca823d43.png)

>? Output Group Setting의 Output Group Type에서 HLS/HLS_ARCHIVE/HLS_StreamPackage를 선택하고 DRM을 활성화하면 기본적으로 Fairplay 암호화가 사용됩니다. Output Group Setting의 Output Group Type에서 DASH/DASH_StreamPackage를 선택하고 DRM을 활성화하면 기본적으로 Widevine 암호화가 사용됩니다.
>- Fairplay 키 설정. 출력 유형을 HLS/HLS_ARCHIVE/HLS_StreamPackage로 선택한 경우에는 Fairplay 암호화 방식이 적용되며, Fairplay의 ContentId(KeyId), Key, Iv를 입력해야 합니다. 그중 Key와 Iv는 32비트의 16진수 문자열입니다.
![](https://main.qcloudimg.com/raw/e172623be22b4397d9f4964d90e8eb03.png)
>- Widevine 키 설정. 출력 유형을 DASH/DASH_StreamPackage로 선택한 경우에는 Widevine 암호화 방식이 적용되며, Widevine의 ContentId 및 Track을 설정해야 합니다. 그중 Track 유형은 SD/HD/UHD1/UHD2/AUDIO로 나뉩니다.
>- All Track을 선택하면 5가지 Track 유형의 KeyId와 Key가 동일하게 설정됩니다.
![](https://main.qcloudimg.com/raw/06b22ae97702570f7bdfac4161219ece.png)
>-  Select Track를 선택하는 경우 각 Track 유형의 KeyId와 Key를 사용자 정의 설정할 수 있습니다.
![](https://main.qcloudimg.com/raw/9c9e6b56980d6c87aea64c2b3b426ad5.png)

f.     오디오 설정. StreamLive는 단일 출력 유닛의 여러 오디오 트랜스 코딩 설정을 지원합니다. 여기에서 오디오 이름, 오디오 트랜스 코딩 포맷, 오디오 비트 레이트, 해당 오디오 언어를 포함한 오디오 템플릿을 구성할 수 있으며, 오디오 셀렉터와 연결되지 않은 경우, Input 입력 스트림에서 기본 스트림을 선택해 트랜스 코딩하여 출력할 수 있습니다. 현재 지원되는 오디오 트랜스 코딩 비트 레이트 범위는 6000-1024000Bit입니다. 언어 코드는 ISO639 표준을 따르며 3자리 언어 코드를 입력해야 합니다.

![](https://main.qcloudimg.com/raw/c092adee1a2aeca7f9e98f18659b4aef.png)

g.     비디오 설정. StreamLive는 비디오 템플릿 이름, 인코더 유형 선택(현재 H264 지원), 비디오 트랜스 코딩 비트 레이트(지원 범위 50000-40000000Bit), 해상도, 프레임 레이트 설정 등을 포함한 비디오 템플릿 구성을 지원합니다. 'Top Speed Codec Transcoding'은 Tencent Cloud 비디오 팀에서 개발한 고성능의 비디오 트랜스 코딩 서비스로, 해당 기능을 활성화하면 AI 알고리즘 기능을 통해 실시간으로 비즈니스 시나리오에 최적화된 동적 인코딩 매개변수를 컴퓨팅하여 낮은 비트 레이트의 고품질 트랜스 코딩 서비스를 구현합니다. 'Bitrate compression ratio'는 비디오 비트 레이트의 압축 비율입니다.

![](https://main.qcloudimg.com/raw/92242c0a054e342a1071794db28600de.png)

>? 더욱 우수한 성능의 스마트 비디오 압축 알고리즘이 탑재된 코덱이 필요한 경우, ‘초고속 고화질’ 트랜스 코딩을 선택할 수 있습니다. 해당 기능을 활성화하면 AI 알고리즘이 비즈니스 시나리오에 따라 실시간으로 최적의 동적 인코딩 매개변수를 컴퓨팅하여 낮은 비트 레이트의 고품질 트랜스 코딩 서비스를 구현합니다.

h.     출력 조합. Outputs를 설정하여 생성된 오디오 트랜스 코딩 템플릿과 비디오 트랜스 코딩 템플릿을 조합 및 연결합니다. 또한 HLS 또는 DASH의 파일 태그에서 Scte35 관련 정보의 전송을 지원합니다.

![](https://main.qcloudimg.com/raw/9e2db2401085804c20ea520364f43c3a.png)

i.      하단의 [Done]을 클릭하여 설정을 저장합니다.

![](https://main.qcloudimg.com/raw/1874e5ebae643cddbe8f41c00bc92731.png)

j.      채널 설정이 모두 완료되었습니다. [Start]를 클릭하여 실행합니다.

![](https://main.qcloudimg.com/raw/ec0fe249551d5db6d80697a1c5d47d36.png)

## 5.   StreamLive를 통해 Tencent Cloud COS로 보관

StreamLive는 HLS 파일을 Tencent Cloud COS로 출력하여 보관하도록 지원합니다. 이를 위해 우선 COS에 버킷을 생성하고 StreamLive에 버킷 액세스 권한을 부여해야 합니다.

1. COS 서비스 활성화 및 COS 버킷 생성

COS로 출력하여 보관하는 작업을 시작하기 전에 먼저 [Tencent Cloud COS 서비스 활성화 ](https://console.cloud.tencent.com/cos5)여부를 확인하십시오. COS 서비스를 활성화한 뒤, [COS 버킷 콘솔](https://console.cloud.tencent.com/cos5)에서 [버킷 리스트]를 선택하고 [버킷 생성]을 클릭하여 근처 리전에 COS 버킷을 생성합니다.

![](https://main.qcloudimg.com/raw/258a128f8e010886f7bea5b6dac83c72.png)

2. 출력 유형을 HLS_ARCHIVE로 선택합니다. StreamLive 콘솔로 돌아와서 출력 설정 시, 출력 유형을 HLS_ARCHIVE로 선택합니다.

![](https://main.qcloudimg.com/raw/5e782e85e27d4f860d9921cc86f1165f.png)

3. StreamLive에 COS 버킷 액세스 권한을 부여합니다. StreamLive에 COS 버킷 액세스 권한을 부여하지 않았기 때문에 COS 타깃 필드가 회색으로 설정되어 있고 입력이 제한되어 있습니다. [click here]을 클릭하면 권한 부여 알림창이 나타납니다. [Authorize Now]를 클릭하여 권한 추가 인터페이스로 이동합니다. [Grant]를 클릭하여 권한 부여를 완료합니다.

![](https://main.qcloudimg.com/raw/5327f143f1fc7482c68225e8abad3c82.png)

![](https://main.qcloudimg.com/raw/3b3a91b1e9053f9ac0b6c9bc2955e12c.png)

권한 부여 완료 후 StreamLive 인터페이스로 돌아와 [Authorization completed]를 선택하면 COS Destination 필드를 입력할 수 있습니다.

![](https://main.qcloudimg.com/raw/ee8f5a51ec6fb2642e570a9c67f91865.png)

![](https://main.qcloudimg.com/raw/41fc5c9c4a18d04b54f6585241231688.png)

4. COS 보관 주소를 입력합니다. 생성한 COS 버킷을 바탕으로 COS 보관 주소를 입력할 수 있으며 포맷은 다음과 같습니다. http://<BucketName-APPID>.cos.<Region>.myqcloud.com/path

5. 설정을 저장하고 제출합니다. 이어서 [4-4]절의 나머지 channel 설정을 완료하고 저장합니다.

## 6.   StreamLive를 통해 Tencent Cloud StreamPackage로 출력

StreamLive는 Tencent Cloud StreamPackage와 함께 사용하여 HLS/DASH 포맷의 라이브 방송 스트림을 그대로 동일 계정의 StreamPackage에서 출력할 수 있도록 지원함으로써, 사용자가 손쉽게 자체 원본 서버를 구축하고 비디오 배포 및 재생할 수 있도록 해줍니다.

1. StreamPackage 활성화

StreamPackage로 출력하기 전에 먼저 [StreamPackage 서비스 활성화 ](https://console.cloud.tencent.com/mdp/channel)및 Channel 생성을 완료하십시오.

2. StreamPackage의 Channel을 생성하십시오.

좌측 상단의 [Create Channel]을 클릭하여 채널을 생성하고 채널 이름과 StreamLive 출력 유형과 동일한 프로토콜을 입력합니다. 예시: StreamLive의 출력 유형을 HLS_StreamPackage로 선택한 경우, 여기에서도 HLS를 선택합니다.

>! StreamLive과 StreamPackage은 같은 Region에 있어야 합니다.

![](https://main.qcloudimg.com/raw/ca0ae9e483499e4489a8db47b7bb290b.png)

3. Endpoint 생성

Channel이 생성되면 Channel의 상세 내용 페이지로 들어가 Endpoint 노드를 생성할 수 있으며, 실제 비즈니스 요구사항에 따라 IP 블랙리스트/화이트리스트 또는 인증 기능 활성화 여부도 선택할 수 있습니다.

![](https://main.qcloudimg.com/raw/da2c4f2cefcbb73aa5ba68f75579937c.png)

4. Endpoint 주소 및 Channel ID 획득

생성된 Endpoint의 URL이 재생/원본 서버 주소가 됩니다.

![](https://main.qcloudimg.com/raw/30594049a37593a5d8827990bd9a13a1.png)

>?  Channel ID는 StreamLive 출력을 입력하는 데 사용됩니다.
> ![](https://main.qcloudimg.com/raw/c66b1bb5f1c9f570225310e66f8e0a66.png)

5. 출력 유형을 HLS_STREAMPACKAGE 또는 DASH_STREAMPACKAGE로 선택합니다.

StreamLive 콘솔로 돌아가 출력 설정 시, 출력 유형을 HLS_STREAMPACKAGE 또는 DASH_STREAMPACKAGE(사용자의 실제 비즈니스 니즈 및 방금 생성한 StreamPackage의 Channel 유형에 따라 결정)로 선택합니다. StreamPackage의 Channel ID를 입력합니다.

![](https://main.qcloudimg.com/raw/486e54380f8bbecd2430c01ad8265c86.png)

6. 설정을 저장하고 제출합니다. 이어서 [4-4]절의 나머지 Channel 설정을 완료하고 저장합니다.

## 7.   채널 가져오기/내보내기, 복제, 편집 및 삭제

StreamLive는 채널 구성 파일 가져오기/내보내기 및 채널 복제 기능을 통해 신속한 채널 생성을 지원합니다.

1. 채널 내보내기

StreamLive의 [Channel Management] 인터페이스에 생성한 채널 및 상태가 표시되며, 우측의 [Export] 버튼을 클릭하면 채널 구성 json 파일을 빠르게 내보낼 수 있습니다.

![](https://main.qcloudimg.com/raw/764c7eea7b0ea222364a5b4dad88eb41.png)

![](https://main.qcloudimg.com/raw/e67829bbee59c2148ba68ae1e652f8da.png)

2. 채널 가져오기

[Channel Management] 인터페이스에서 [Create Channel] 버튼을 클릭한 뒤, [Import Configuration]을 선택하고, 수정된 채널 구성 json 파일을 선택해 저장합니다.

json 파일을 제출하면 채널 편집 상태로 전환되며, 기존의 구성 프로세스에 따라 채널을 저장 및 제출합니다.

![](https://main.qcloudimg.com/raw/1fe8fdf4c50c5be5a6fe1dc820f5469f.png)

>?
>- 채널 가져오기는 실제로는 매우 빠르게 진행되는 입력 프로세스로, 사용자가 가져온 json 파일을 기반으로 [Basic Information], [Output Group Setting] 두 부분의 내용을 빠르게 자동으로 입력해주며, [Input Setting] 부분은 무시하기 때문에 Input을 다시 선택해야 합니다. 따라서 이와 같은 방법으로 빠르게 Channel을 생성해야 하는 경우, 사전에 새로운 input을 생성해 놓을 수 있습니다.
>- 채널 편집 시 새로운 구성 파일을 가져오는 경우, 기존 채널 구성 정보는 덮어씁니다.

3. 채널 복제

채널 복제는 빠르고 특수한 채널 내보내기/가져오기 작업으로, [Channel Management] 인터페이스에서 [Operation]의 [Clone]을 클릭하면 복제 채널의 구성 상태로 전환됩니다.

이때, 채널은 자동으로 복제된 채널의 기본 정보([Input Setting] 부분 제외)를 입력하고, 기존 구성 프로세스에 따라 채널을 저장 및 제출합니다.

![](https://main.qcloudimg.com/raw/92bf580af5c4f013363915688744f1f6.png)

4. 채널 편집 및 삭제

[RUNNING] 중인 채널은 편집/삭제가 불가능하며, 먼저 [Stop] 후 편집/삭제를 진행해야 합니다.

![](https://main.qcloudimg.com/raw/57923bc62f83d99ee10df572bebbb6e3.png)

## 8.   채널 품질 모니터링

[Channel Management] 인터페이스에서 채널 이름을 클릭해 채널 상세 내용 페이지로 들어갑니다. 채널 상세 정보 페이지에는 해당 채널의 정보, 입력, 출력, Alerts, Health 등 상세 정보가 표시됩니다.

![](https://main.qcloudimg.com/raw/c97468a3a9fbeb51e9c15ae552d53efd.png)

특정 채널의 파이프에서 문제가 발생하거나 잠재적인 문제가 발견된 경우, StreamLive는 해당 채널에 대한 알람을 생성합니다. Set time은 알람 이벤트 발생 시간이고 Cleared time는 알람 해제 시간입니다. 경고 기록이 SET일 경우 Set time, State 필드가 빨간색으로 표시되고, 경고 기록이 삭제되면 상태가 CLEARED로 바뀌고 빨간색 표시가 사라지는 등의 방식으로 알람 기록 상태가 업데이트됩니다. 알람에는 문제가 발생한 파이프, 알람 유형 및 상세 정보가 명확히 기록됩니다. 최근 5일 이내의 데이터만 조회할 수 있으며 조회 기간은 24시간 미만입니다.

삭제 전:

![](https://main.qcloudimg.com/raw/a76c4bb27dd86c6e2d06f2dd6ccbb42e.png)

삭제 후:

![](https://main.qcloudimg.com/raw/4a986687ccdf97ce0e222aac2b936fb6.png)

Heath는 사용자가 현재 채널이 정상적으로 운영되고 있는지 확인할 수 있도록 채널 입력(대역폭, 입력 비디오 프레임 레이트 및 입력 오디오 프레임 레이트) 및 출력(대역폭) 정보와 해당 그래프를 제공합니다. 최근 5일 이내의 데이터만 조회할 수 있으며 조회 기간은 24시간 미만입니다.

![](https://main.qcloudimg.com/raw/e49e312b0d134d0d9fb1c8dccbcee00b.png)

![](https://main.qcloudimg.com/raw/de84757254338b428e55695b4b3a2170.png)

 

## 9.   시간 계획 설정

StreamLive 채널 시간 계획을 설정하여, 푸시 스트리밍 과정에서 정해진 시간에 특정 이벤트 설정을 트리거할 수 있습니다(예: 15:00:00 입력 소스를 input2로 전환).

[Channel Management] 인터페이스에서 채널 이름을 클릭해 채널 상세 내용 페이지로 들어갑니다. [Plan]을 선택하고 [Add]를 클릭하여 이벤트를 추가하십시오.

1. 두 가지 트리거 시간이 있는 모드는 다음을 선택할 수 있습니다. Fixed Time은 날짜와 시간을 수동으로 설정해야 하며, 이벤트가 설정한 시간에 실행됩니다. Immediate는 현재 설정 시간이 트리거 시간이 되어 이벤트를 즉시 실행합니다.

2. 이벤트 유형은 현재 '입력 전환' 기능만 지원하며, 사용자는 타깃 입력 소스를 선택할 수 있습니다.

[create]를 클릭하여 시간-이벤트 생성을 완료하십시오.

![](https://main.qcloudimg.com/raw/b45ec0b7275bc1c4363bd683652dd541.png)

![](https://main.qcloudimg.com/raw/cb4c8a9d4f289072476364297346fb4d.png)

>!
>- 작성하는 시간은 사용자 소재지의 시간이며 과거의 시간으로 작성할 수 없습니다.
>- 전환된 MP4_PULL (또는 HLS_PULL) 입력 소스의 스트림 설정이 ONCE인 경우, 풀 스트림 한 번 이후 입력 스트림이 자동으로 끊기며 이어지는 이벤트는 트리거되지 않습니다.

 

생성한 모든 이벤트는 '트리거 시간' 순서에 따라 차례대로 정렬됩니다. 이벤트는 조회, 삭제 및 추가할 수 있습니다.

>! 생성된 이벤트는 편집 작업을 지원하지 않습니다.

 