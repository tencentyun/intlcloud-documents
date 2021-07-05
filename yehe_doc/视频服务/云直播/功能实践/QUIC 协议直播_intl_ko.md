QUIC(Quick UDP Internet Connection)은 Google이 개발한 UDP 프로토콜 기반의 차세대 고품질 전송 프로토콜입니다. IETF는 2018년부터 QUIC 프로토콜을 HTTP/3.0 네트워크 프로토콜 규범으로 정하고 보급하기 시작하였습니다. QUIC 프로토콜은 TCP 프로토콜에 비해 약한 네트워크 및 패킷 손실률이 높은 시나리오에서의 데이터 전송에 더욱 적합합니다.

Tencent Video Cloud는 현재 QUIC 프로토콜을 사용한 [라이브 방송 푸시 스트림](#push)과 [라이브 방송 풀 스트림](#play)을 지원합니다.

## 프로토콜 버전 지원

현재 CSS에서 지원되는 QUIC 프로토콜 버전: 39, 41, 42, 43, 44.

> ! 43 버전 사용을 권장합니다.

## 주의 사항

QUIC 풀 스트림 기능을 사용하시려면 Tencent Cloud에 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 풀 스트림 도메인에 해당하는 QUIC 프로토콜 풀 스트림 기능을 활성화하십시오.


## 라이브 방송 푸시 스트림

[](id:push)

### 액세스 방법
라이브 방송 푸시 스트림은 RTMP over QUIC 프로토콜을 지원하며, 푸시 스트림을 위해 UDP 1935를 사용해야 합니다. 푸시 스트림 주소는 RTMP over TCP 프로토콜과 동일하며, CSS 콘솔의 [[주소 생성기](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)] 중, [푸시 스트림 주소 생성](https://intl.cloud.tencent.com/document/product/267/31084)에서 생성할 수 있습니다.

![](https://main.qcloudimg.com/raw/31d20b09de1c8d3c9748872e59f9a828.png)


푸시 스트림 액세스 방식은 다음과 같은 두 가지가 있습니다.

- **Tencent Cloud [MLVB SDK](https://intl.cloud.tencent.com/document/product/1071/38150) 사용**: 사용 방법은 RTMP over TCP 방식과 동일하며, SDK는 기본적으로 QUIC 프로토콜을 사용하여 Tencent Cloud에 액세스합니다.
- **자체 QUIC 프로토콜 클라이언트 사용**: LVB가 생성한 푸시 스트림 주소를 통해 QUIC 프로토콜 푸시 스트림을 시작할 수 있습니다. RTMP over QUIC의 푸시 스트림 주소와 RTMP over TCP의 푸시 스트림 주소는 동일하며 QUIC 프로토콜 푸시 스트림은 Tencent Cloud의 QUIC 스트림 서버에 직접 액세스합니다.

[](id:pushtest)


## 라이브 방송 풀 스트림

[](id:play)

### 풀 스트림 액세스

라이브 방송 풀 스트림은 HTTP over QUIC 프로토콜을 지원하며, 풀 스트림을 위해 UDP 443 포트를 사용해야 합니다. 풀 스트림 주소는 HTTP FLV 프로토콜과 동일하며, CSS 콘솔의 [[주소 생성기](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)] 중, [풀 스트림 주소 생성](https://intl.cloud.tencent.com/document/product/267/31084)을 통해서도 생성할 수 있습니다.
![](https://main.qcloudimg.com/raw/e4727db59f2e195abdd9382456212d14.png)

[](id:playtest)

### 풀 스트림 테스트

Tencent Cloud [TCPlayerDemo](https://imgcache.qq.com/open/qcloud/video/vcplayer/demo/tcplayer-test.html) 툴을 사용하여 검사할 수 있으며, 구체적인 방법은 다음과 같습니다.
> ? Chrome 브라우저는 QUIC 프로토콜 요청을 지원합니다. Tencent Cloud TCPlayerDemo를 Chrome 브라우저와 결합하여 사용하면 QUIC 프로토콜을 사용하여 재생되었는지 여부를 검증할 수 있습니다.

1. Chrome의 QUIC 스위치를 켭니다.
   Chrome 브라우저 주소창에 `chrome://flags/#enable-quic `를 입력하고 스위치를 Enabled로 설정한 뒤, Chrome 브라우저를 재시작합니다.
   ![](https://main.qcloudimg.com/raw/b5aee3532ef918518206b607cc2d8f53.png) 
2. TCPlayerDemo를 실행합니다. HTTPS 재생 주소 입력 시 FLV와 HLS의 풀 스트림 주소 사용을 권장하며, RTMP의 주소는 Flash 재생만 지원합니다. 연결 생성을 클릭하고 ![](https://main.qcloudimg.com/raw/5886ad8b68619d7ba99268e0a4e24f2c.png)를 클릭해 재생을 시작합니다.
![](https://main.qcloudimg.com/raw/a2e4d83ca259b97b4376875215015a22.png)
3. Chrome의 개발자 툴에서 [Network] 탭을 선택하면 요청한 protocol이 `http/2+quic/46`임을 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/e1e61b7ae544881b898ccd7aa116e8a4.png)

> ? 
> - 브라우저 버전에 따라 QIUC 버전 넘버가 조금씩 다를 수 있습니다.
> - Protocol 필드가 기본적으로 표시되지 않는 경우, 디스플레이에서 마우스 오른쪽 버튼을 클릭하고 Protocal을 선택하면 표시됩니다.
> ![](https://main.qcloudimg.com/raw/ee21e41e7f61e87dccb2f2509ff7678d.png)
