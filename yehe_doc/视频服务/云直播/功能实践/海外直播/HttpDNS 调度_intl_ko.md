## 솔루션 배경
CSS는 기본적으로 DNS 확인을 기반으로 글로벌 푸시 및 재생 트래픽을 라우팅합니다. 이는 가장 일반적이고 가장 간단한 액세스 방법입니다. 그러나 중국 본토 내 네트워크 환경의 복잡성으로 인해 DNS 확인 오류 및 네트워크 간 트래픽 발생은 일반적인 현상입니다. 라이브 스트리밍을 위한 트래픽 라우팅을 최적화하려면 Tencent Cloud의 HTTPDNS를 사용하는 것이 좋습니다.

ISP의 LocalDNS 송신은 권한 있는 DNS 대상 IP 주소를 기반으로 NAT를 수행하거나 리졸브 요청을 다른 DNS 서버로 전달합니다. 이것은 권한 있는 DNS 서버가 ISP의 LocalDNS의 IP 주소를 올바르게 식별하기 어렵게 하여 확인 오류와 네트워크 간 트래픽을 발생시킵니다. Tencent Cloud의 HTTPDNS 서비스는 최고의 DNS 클러스터 기술을 기반으로 하며 다중 ISP 라우팅 및 사용자 지정 경로를 지원합니다.

>?  본문은 HTTPDNS를 사용하여 글로벌 라이브 스트리밍을 위해 트래픽 라우팅을 최적화하는 방법을 보여줍니다. 사용되는 HTTPDNS API에 대한 자세한 내용은 [Querying with HTTP Request Methods](https://intl.cloud.tencent.com/document/product/1130/44468)를 참고하십시오.

## 준비 사항
1. HTTPDNS 서비스를 활성화하려면 Tencent Cloud HTTPDNS 콘솔의 [Activating HTTPDNS](https://intl.cloud.tencent.com/document/product/1130/44461)를 참고하십시오.
2. [개발 구성 페이지](https://console.cloud.tencent.com/httpdns/configure)로 이동하여 인증 정보(인증 ID, DES 키)를 확인합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/ad5bf89eb5cfe81d4d9b7d19176c622a.png)

## HTTPDNS를 사용하여 푸시 트래픽 라우팅

### 푸시 IP 주소 요청

HTTPDNS 에서 푸시 IP 주소를 요청하려면 `http://119.29.29.98/d?dn={$push_domain DES 암호화 문자열}&ip={$ip DES 암호화 문자열}&id=$id` 형식의 HTTP Get 요청을 사용합니다.

- push_domain은 DES 알고리즘을 사용하여 암호화해야 하는 푸시 도메인을 나타냅니다. 키는 [HTTPDNS 개발 설정 페이지](https://console.cloud.tencent.com/httpdns/configure)에서 확인할 수 있습니다. 자세한 내용은 [AES/DES Encryption/Decryption](https://intl.cloud.tencent.com/document/product/1130/44470)을 참고하십시오.
- ip 필드는 요청자의 공개 송신 IP 주소를 나타냅니다. 이 필드는 트래픽이 라우팅되는 IP 주소의 리전 및 ISP를 결정합니다. 또한 DES 알고리즘을 사용하여 암호화해야 합니다.
- id 필드는 사용자를 고유하게 식별하는 권한 부여 ID를 나타냅니다.

### IP 주소 복호화

HTTPDNS를 통해 얻은 데이터는 DES로 암호화됩니다. 암호를 해독하여 IP 주소(server_ip)를 가져옵니다. 자세한 내용은 [AES/DES Encryption/Decryption](https://intl.cloud.tencent.com/document/product/1130/44470)을 참고하십시오.

### 푸시 URL 스플라이싱

여기서 server_ip는 **이전 단계에서 얻은 푸시 IP 주소**입니다. 푸시 URL의 형식은 `rtmp://server_ip/live/streamname?txTime=xxx&txSecret=xxx&txHost=domain` 입니다. txHost(중요)는 푸시에 사용하는 도메인입니다.

## HTTPDNS를 사용하여 재생 트래픽 라우팅

### 재생 IP 주소 요청

HTTPDNS 에서 재생 IP 주소를 요청하려면 `http://119.29.29.98/d?dn={$domain DES 암호화 문자열}&ip={$ip DES 암호화 문자열}&id=$id` 형식의 HTTP Get 요청을 사용합니다.

| 필드 | 의미 |
|---------|---------|
| push_domain | 재생 도메인, 이 필드의 값은 DES 알고리즘을 사용하여 암호화되어야 합니다. [HTTPDNS 개발 구성 페이지](https://console.cloud.tencent.com/httpdns/configure)에서 키를 볼 수 있습니다. 자세한 내용은 [AES/DES Encryption/Decryption](https://intl.cloud.tencent.com/document/product/1130/44470)을 참고하십시오. |
| ip | 요청자의 공중망 송신 IP 주소입니다. 이 필드는 트래픽이 라우팅되는 IP 주소의 리전 및 ISP를 결정합니다. 또한 DES 알고리즘을 사용하여 암호화해야 합니다. |
| id | 각 사용자를 고유하게 식별하는 권한 부여 ID입니다. |

### IP 주소 복호화

HTTPDNS를 통해 얻은 데이터는 DES로 암호화됩니다. 암호를 해독하여 IP 주소(server_ip)를 가져옵니다. 자세한 내용은 [AES/DES Encryption/Decryption](https://intl.cloud.tencent.com/document/product/1130/44470)을 참고하십시오.

### 재생 URL 스플라이싱
- **HTTP**: FLV 및 HLS 재생 프로토콜을 포함하고 있으며, server_ip는 **다운스트림 액세스 포인트 IP 요청**으로 획득한 IP, play_domain은 재생 도메인을 의미합니다. HTTP 재생 URL 조합은 다음과 같습니다.
```
http://server_ip/play_domain/live/streamname.flv?xxxxxxxxxx
http://server_ip/play_domain/live/ streamname.m3u8?xxxxxxxxxx
http://server_ip/play_domain/live/ streamname -123.ts?xxxxxxxxxx
```
- **HTTP**: FLV 및 HLS 재생 프로토콜을 포함하고 있으며, server_ip는 **다운스트림 액세스 포인트 IP 요청**으로 획득한 IP, play_domain은 재생 도메인을 의미합니다. HTTPS 연결 규칙은 플레이어에 따라 다릅니다. **TCP 연결의 대상 IP 주소는 HTTPDNS에서 할당한 server_ip**여야 하며, URL은 일반 재생 요청이어야 합니다. 형식은 다음과 같습니다.
```
https://server_ip/play_domain/live/ streamname.flv?xxxxxxxxxx
https://server_ip/play_domain/live/ streamname.m3u8?xxxxxxxxxx
https://server_ip/play_domain/live/ streamname -123.ts?xxxxxxxxxx
```
- **RTMP**: RTMP 재생 URL의 형식은 다음과 같습니다(server_ip는 **이전 단계에서 얻은 재생 IP 주소**이고 play_domain은 재생 도메인임).
```
rtmp://server_ip/play_domain/live/ streamname?xxxxxxxxxx
```

>? HTTPDNS 요청 오류가 발생할 가능성은 적습니다. 요청 시간이 초과되었거나 반환된 결과가 IP 주소가 아니거나 비어 있는 경우 LocalDNS 서버에서 확인을 수행하십시오.
