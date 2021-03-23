## 솔루션 배경
CSS는 해외 푸시 스트림 및 재생 스케쥴링에 기본적으로 도메인 DNS 리졸브 스케쥴링을 사용하며, 이는 가장 많이 사용되고 간편한 액세스 방식입니다. 해외 네트워크 환경은 매우 복잡하여 도메인 리졸브에 오류가 발생하거나 네트워크 간 트래픽이 발생하는 문제가 보편적으로 존재합니다. 해당 문제를 해결하기 위해 CSS에 해외 라이브 방송 스케쥴링을 최적화하는 HttpDNS 솔루션 사용을 권장합니다.

통신사 LocalDNS의 발신 게이트웨이는 권한 있는 DNS 타깃 IP 주소에 따라 NAT를 진행하거나, 리졸브 요청을 다른 DNS 서버에 전달합니다. 이에 따라 권한 있는 DNS가 정확하게 통신사 LocalDNS IP를 식별할 수 없어 도메인 리졸브 오류 및 네트워크 간 트래픽이 발생하는 등의 문제가 나타납니다.
Tencent Cloud HttpDNS는 세계적으로 앞서가는 DNS 클러스터 기술을 보유하고 있으며, 여러 통신사 및 사용자 정의 회선에 최적화된 스케쥴링을 지원합니다. 자세한 내용은 [모바일 HttpDNS 리졸브]를 참조하십시오.


>?본 문서에서는 무료 HttpDNS를 예시로 HttpDNS 스케쥴링 솔루션을 Tencent Cloud 해외 라이브 방송에 적용하는 방법을 소개합니다. 무료 버전 HttpDNS 인터페이스에 대한 자세한 내용은 [문서]를 참조하십시오. 

## HttpDNS를 사용한 업스트림 푸시 스트림 스케쥴링

### 1. 업스트림 액세스 포인트 IP 요청
`http://119.29.29.29/d?dn=$push_domain.&ip=$ip`에서 HTTP Get 요청의 매개변수 의미는 다음과 같습니다.
- push_domain은 푸시 스트림 도메인을 의미합니다.
- IP 필드는 요청 측의 외부 네트워크 발신 게이트웨이 IP입니다. 해당 IP는 최종적으로 스케쥴링된 액세스 포인트 IP의 소재지 및 통신사를 의미합니다.


### 2. 업스트림 푸시 스트림 URL 조합
server_ip는 **업스트림 액세스 포인트 IP 요청**으로 획득한 IP이며, 푸시 스트림 URL 조합은 다음과 같습니다.
`rtmp://server_ip/live/streamname?txTime=xxx&txSecret=xxx&txHost=domain`, 여기서 가장 중요한 점은 기존의 푸시 스트림 매개변수에 비즈니스 푸시 스트림 도메인을 대표하는 필드인 txHost가 추가되었다는 것입니다.

## HttpDNS를 사용한 다운스트림 재생 스케쥴링

### 1. 다운스트림 액세스 포인트 IP 요청
`http://119.29.29.29/d?dn=$domain.&ip=$ip`에서 HTTP Get 요청의 매개변수 의미는 다음과 같습니다.
- domain은 재생 도메인을 의미합니다.
- IP 필드는 요청 측의 외부 네트워크 발신 게이트웨이 IP입니다. 해당 IP는 최종적으로 스케쥴링된 액세스 포인트 IP의 소재지 및 통신사를 의미합니다.


### 2. 다운스트림 재생 URL 조합
- HTTP: FLV 및 HLS 재생 프로토콜을 포함하고 있으며, server_ip는 **다운스트림 액세스 포인트 IP 요청**으로 획득한 IP, play_domain은 재생 도메인을 의미합니다. HTTP 재생 URL 조합은 다음과 같습니다.

```
http://server_ip/play_domain/live/streamname.flv?xxxxxxxxxx
http://server_ip/play_domain/live/ streamname.m3u8?xxxxxxxxxx
http://server_ip/play_domain/live/ streamname -123.ts?xxxxxxxxxx
```

- HTTP: FLV 및 HLS 재생 프로토콜을 포함하고 있으며, server_ip는 **다운스트림 액세스 포인트 IP 요청**으로 획득한 IP, play_domain은 재생 도메인을 의미합니다. HTTPS 조합 규칙은 플레이어 로직을 따르며 **TCP에 연결 구축을 요청하는 타깃 IP가 HttpDNS로 스케쥴링되는 server_ip**입니다. 재생 URL 요청 시에는 일반적인 재생 요청이 필요합니다.

```java
https://play_domain/live/ streamname.flv?xxxxxxxxxx
https://play_domain/live/ streamname.m3u8?xxxxxxxxxx
https://play_domain/live/ streamname -123.ts?xxxxxxxxxx
```

- RTMP: server_ip는 **다운스트림 액세스 포인트 IP 요청**으로 획득한 IP, play_domain은 재생 도메인을 의미합니다. RTMP 재생 URL 조합은 다음과 같습니다.

```
rtmp://server_ip/play_domain/live/ streamname?xxxxxxxxxx
```

>!위 내용은 CSS 해외 스케쥴링 플랫폼 기반의 솔루션으로, 중국 내 사용에 완벽히 응용할 수 없습니다. 중국 내에서 HttpDNS를 통한 CSS 스케쥴링 최적화가 필요한 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 문의하시기 바랍니다.
