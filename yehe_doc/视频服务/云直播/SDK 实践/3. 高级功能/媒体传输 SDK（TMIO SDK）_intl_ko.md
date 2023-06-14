## 개요
점점 더 많은 스트리밍 미디어 전송 프로토콜이 등장함에 따라 TMIO SDK(Tencent Media IO SDK)는 주요 프로토콜을 통합, 최적화 및 확장하여 안정적이고 사용 가능한 미디어 애플리케이션을 쉽게 개발할 수 있도록 지원하여 다양한 프로토콜의 힘든 개발 및 디버깅에서 자유로울 수 있게 합니다.
TMIO SDK는 SRT 및 QUIC 등 주류 스트리밍 미디어 프로토콜을 최적화 및 확장했으며, 자체 개발 전송 제어 프로토콜 ETC(Elastic Transmission Control)를 추가했습니다. 향후 더 많은 주류 스트리밍 미디어 프로토콜을 최적화하도록 계속 확장될 것입니다.

### 강점
- **멀티 플랫폼 지원**: Android, iOS, Linux, Mac 및 windows 지원.
- **유연한 통합 방법**:
   - [프록시 모드 선택](#choose)에 설명된 대로 비간섭 프록시 모드 제공.
   - 간단한 API 설계를 기반으로 신속하게 통합하여 기존 전송 프로토콜 대체 가능. [내부 통합](#internal)을 참고하십시오.
- **API 설계가 간단하고 호환성과 유연성이 높음**.
   - 사용하기 쉬운 API 제공.
   - 비즈니스 요구 사항 및 시나리오에 따라 적절한 모드와 정책 선택 가능.
   - 다른 프로토콜을 사용자 지정, 최적화, 확장 가능.
- **다양한 전송 프로토콜 확장, 최적화 및 통합**:
   - SRT, QUIC 등 차세대 주요 전송 프로토콜 및 자체 개발 전송 제어 프로토콜 ETC 지원
   - 다양한 비즈니스 시나리오에 적용 가능한 다양한 수요 옵션
   - UDP 기반의 저지연, 안전하고 안정적인 전송 설계
   - 보다 안정적이고 원활한 전송을 보장하는 다중 연결 가속 이점

### 효과 표시(TMIO SRT 예시)
- **TMIO는 업스트림 안정성과 다운스트림 원활성을 향상시키기 위해 약한 네트워크 및 장거리 전송 시나리오에서 사용할 수 있는 SRT 프로토콜 지원.**
  다음 테스트 시나리오에서, RTMP 스트리밍은 10% 패킷 손실률에서 이미 랙이 발생하였으나, SRT 스트리밍은 10%에서는 물론 30% 패킷 손실률에서도 안정적이고 낮은 딜레이 상태를 유지합니다.
  
  <video width="500px" height="auto" src="https://qcloudimg.tencent-cloud.cn/raw/8d165df8dec666b05a013a3def596e0b.mp4" controls  muted></video>


### 기능 소개

- **SRT 기반 스트리밍 미디어 전송**
  - **높은 랜덤 패킷 손실 방지율 제공**.
  - **ARQ 및 타임아웃 정책에 기반한 재전송 메커니즘 구현**
  - **UDT 기반의 저지연, 안전하고 안정적인 전송 설계**.
  - **새로운 연결 취합 기능을 통한 다중 연결 전송**:
  다중 연결 전송 기능을 사용하면 여러 연결을 구성하여 데이터를 전송할 수 있습니다. 4G/5G 네트워크가 널리 사용되는 현 시대에 모바일 기기는 Wi-Fi와 데이터 네트워크 모두를 통해 데이터를 전송할 수 있으므로 갑자기 네트워크 연결이 끊어졌을 때 하나의 연결만 가능하더라도 연결 안정성을 보장할 수 있습니다.

    <table>
    <thead><tr><th>기능 모드</th><th>설명</th></tr></thead>
    <tbody><tr>
    <td>방송 모드</td>
    <td>이 모드에서는 데이터 무결성과 연결 안정성을 보장하는 중복 데이터를 전송하도록 여러 링크를 구성할 수 있습니다.</td>
    </tr><tr>
    <td>프라이머리/세컨더리 모드</td>
    <td>이 모드에서는 연결 안정성과 신뢰도에 따라 한 번에 하나의 링크만 활성화되며 실시간으로 최적의 연결을 선택하여 데이터를 전송합니다. 이는 연결 안정성과 신뢰성을 보장할 뿐만 아니라 중복 데이터의 대역폭 사용을 줄입니다.</td>
    </tr><tr>
    <td>취합 모드</td>
    <td>높은 비트 레이트와 대역폭이 필요한 시나리오에서 단일 연결의 대역폭이 요구 사항을 충족할 수 없는 경우 이 모드는 데이터를 분할하고 여러 연결을 통해 데이터를 보낸 다음 수신기 끝에서 데이터를 재결합하여 사용 가능한 대역폭을 늘릴 수 있습니다.</td>
    </tr>
    </tbody></table>

- **QUIC 기반 스트리밍 미디어 전송**
  - **어댑티브 혼잡 방지 알고리즘**
  - **네트워크 연결 마이그레이션 지원, 매끄럽고 감지 불가**
  - **차세대 HTTP3 기본 전송 프로토콜 지원**
  - **대역폭 제한 및 지터 환경에서는 중복 데이터 전송을 줄이고 대역폭 비용을 절약하여, 이점이 큼**
- **자체 개발 전송 제어 프로토콜 ETC**
  - **순수 자체 개발, 경량, 크로스 플랫폼**
  - **엔드 투 엔드 통신에 적합한 IoT 장치 지원**
  - **빠른 실행, 낮은 딜레이 시간 및 높은 대역폭 사용률**
  - **빠르고 정확하게 링크 상태 변화를 감지하고 적시에 최상의 전송 정책으로 조정**
  - **주요 전송 프로토콜과 공존할 경우, 대역폭을 보다 공정하고 안정적으로 사용할 수 있음**


## 통합 방법
RTMP over SRT 프로토콜을 예로 듭니다.

[](id:choose)
### 프록시 모드 선택
#### Tmio Proxy 모드에서 통합
![](https://qcloudimg.tencent-cloud.cn/raw/4b7d4a5180a9450c2d815161bf060cb2.jpeg)

#### 작업 순서
1. **Tmio Proxy 인스턴스 생성**:
```c++
std::unique_ptr<tmio::TmioProxy> proxy_ = tmio::TmioProxy::createUnique();
```
2. **리스너 설정**:
```c++
void setListener(TmioProxyListener *listener);
```
TmioProxyListener 리스너 API는 아래와 같습니다.
<dx-tabs>
::: Tmio 구성에 대한 콜백
이 콜백에서 Tmio 매개변수를 구성할 수 있습니다. **간단한 구성을 위해 `tmio-preset.h`에서 제공하는 보조 방법을 사용할 수 있습니다**.
```c++
/*
void onTmioConfig(Tmio *tmio);
*/
void onTmioConfig(tmio::Tmio *tmio) override {
		auto protocol = tmio->getProtocol();
		if (protocol == tmio::Protocol::SRT) {
				tmio::SrtPreset::rtmp(tmio);
		} else if (protocol == tmio::Protocol::RIST) {
				tmio->setIntOption(tmio::base_options::RECV_SEND_FLAGS,
													 tmio::base_options::FLAG_SEND);
		}
}
```
:::
::: TmioProxy 시작에 대한 콜백
```c++
/*
void onStart(const char *local_addr, uint16_t local_port); 
*/
void onStart(const char *addr, uint16_t port) override {
		LOGFI("ip %s, port %" PRIu16, addr, port);
}
```
이 콜백을 수신하면 원격 서버가 성공적으로 연결되고 로컬 TCP 포트가 성공적으로 바인딩되며 스트림을 푸시할 수 있습니다.
:::
::: 오류 메시지에 대한 콜백
```c++
/*
void onError(ErrorType type, const std::error_code &err);
*/
void onError(tmio::TmioProxyListener::ErrorType type,
						const std::error_code &err) override {
		LOGFE("error type %s, %s, %d", tmio::TmioProxyListener::errorType(type),
					err.message().c_str(), err.value());
}
```
ErrorType을 기반으로 로컬 또는 원격 IO 오류를 식별할 수 있습니다. 로컬 IO 오류는 일반적으로 스트림 푸시가 중지된 경우와 같이 RTMP 스트림 푸시에 의해 활발하게 트리거되며 일반적으로 무시할 수 있습니다. 그러나 일반적으로 원격 IO 오류를 무시해서는 안 됩니다.
:::
</dx-tabs>
3. **프록시 시작**:
```c++
std::error_code start(const std::string &local_url, const std::string &remote_url, void * config=nullptr)
```

  - API 매개변수

<table>
<thead>
<tr>
<th>매개변수</th>
<th>비고</th>
</tr>
</thead>
<tbody><tr>
<td>local_url</td>
<td>TCP Scheme만 지원합니다. 형식은 <code>tcp://${ip}:${port}</code>입니다. port는 0일 수 있으며 이는 임의의 포트를 바인딩함을 나타냅니다. 바인딩이 성공하면 onStart() 콜백을 통해 바인딩된 포트가 애플리케이션으로 반환됩니다. 포트 0을 사용하면 포트 점유 및 권한 없음과 같은 문제로 인한 바인딩 실패를 방지할 수 있습니다.</td>
</tr>
<tr>
<td>remote_url</td>
<td>원격 서버 URL</td>
</tr>
<tr>
<td>config</td>
<td>SRT bonding 기능 및 QUIC H3 프로토콜이 활성화된 경우에만 적용되는 구성 매개변수입니다. 구체적인 정의는 <code>tmio.h</code>의 TmioFeatureConfig 구조 정의를 참고하십시오.</td>
</tr>
</tbody></table>

  - 단일 연결(예시 코드)

```C++
 proxy_->start(local_url, remote_url, NULL);
```
  - 다중 연결 bonding(예시 코드)
```C++
tmio::TmioFeatureConfig option;
option_.protocol = tmio::Protocol::SRT;
option_.trans_mode = static_cast<int>(tmio::SrtTransMode::SRT_TRANS_BACKUP);
/*-----------------------------------------------------------*/
{
	//필요에 따라 여러 연결을 추가할 수 있습니다
	option_.addAvailableNet(net_name, local_addr, remote_url, 0, weight, -1);
}
/*-----------------------------------------------------------*/

 proxy_->start(local_url, remote_url, &option_);
```
1. **중지**:
```c++
/*
void stop();
*/
proxy_.stop();
```

[](id:internal)
### 내부 통합
#### Tmio SDK의 내부 통합
![](https://qcloudimg.tencent-cloud.cn/raw/8071536afd22d5df2a9d471ab3dce357.jpg)

#### 통합 프로세스
1. **Tmio 인스턴스 생성&매개변수 구성**(예시 코드):
```C++
tmio_ = tmio::TmioFactory::createUnique(tmio::Protocol::SRT);
tmio::SrtPreset::mpegTsLossless(tmio_.get());
tmio_->setIntOption(tmio::srt_options::CONNECT_TIMEOUT, 4000);
tmio_->setBoolOption(tmio::base_options::THREAD_SAFE_CHECK, true);
```

- **Tmio 생성**: `TmioFactory`를 사용하여 생성할 수 있습니다.
- **매개변수 구성**: 다른 API를 선택하여 매개변수를 구성합니다.
<ul>
<li><strong>매개변수</strong>: <code>tmio-option.h</code>를 참고하십시오.</li>
<li><strong>간단한 구성</strong>: <code>tmio-preset.h</code>를 참고하십시오.
</ul>

```C++
//다양한 매개변수 속성을 기반으로 적절한 구성 선택
bool setBoolOption(const std::string &optname, bool value);
bool setIntOption(const std::string &optname, int64_t value);
bool setDoubleOption(const std::string &optname, double value);
bool setStrOption(const std::string &optname, const std::string &value);
...
```

2. **연결 시작**(예시 코드):
```C++
/**
 * open the stream specified by url
 *
 * @param config protocol dependent
 */
virtual std::error_code open(const std::string &url,
							  void *config = nullptr) = 0;
```
  - 단일 연결(config는 NULL일 수 있음)
```C++
//기본적으로 단일 링크
auto err = tmio->open(TMIO_SRT_URL);
if (err) {
	LOGE("open failed, %d, %s", err.value(), err.message().c_str());
}
```

 - 다중 연결 bonding(현재 SRT 프로토콜만 지원)
	- SRT bonding 기능에 대한 config를 설정하려면 `tmio.h` 파일의 TmioFeatureConfig 구조 정의를 참고하십시오.
```C++
tmio::TmioFeatureConfig option_;
option_.protocol = tmio::Protocol::SRT;
option_.trans_mode = static_cast<int>(tmio::SrtTransMode::SRT_TRANS_BACKUP);
option_.addAvailableNet(net_name, local_addr, remote_url, 0, weight, -1);
```
```C++
//다중 연결 bonding
auto err = tmio_->open(TMIO_SRT_URL, &option_);
if (err) {
	LOGE("open failed, %d, %s", err.value(), err.message().c_str());
}
```
  -  다중 연결 bonding open API를 사용하여 데이터 전송을 위해 group에 새 연결을 추가할 수 있습니다.
3. **데이터 전송**:

```C++
int ret = tmio_->send(buf.data(), datalen, err);
if (ret < 0) {
		LOGE("send failed, %d, %s", err.value(), err.message().c_str());
		break;
}
```

4. **데이터 수신**:
	- 프로토콜에 RTMP와 같은 인터랙션이 필요한 경우 데이터 수신 API를 활성화하여 데이터를 읽고 프로토콜 인터랙션을 완료해야 합니다. 여기에 두 가지 API가 제공됩니다.
```c++
/**
* receive data
*
* @param err return error details
* @return number of bytes which were received, or < 0 to indicate error
*/
virtual int recv(uint8_t *buf, int len, std::error_code &err) = 0;

using RecvCallback = std::function<bool(const uint8_t *buf, int len, const std::error_code &err)>;
/**
* receive data in event loop
*
* recvLoop() block current thread, receive data in a loop and pass the data to recvCallback
* @param recvCallback return true to continue the receive loop, false for break
*/
virtual void recvLoop(const RecvCallback &recvCallback) = 0;
```
  - 상위 레이어 애플리케이션의 루프 읽기
```C++
while (true) {
	ret = tmio_->recv(buf.data(), buf.size(), err);
	if (ret < 0) {
		LOGE("recv error: %d, %s", err.value(), err.message().c_str());
		break;
	}
	...
}
```
  - 콜백을 통해 읽기
```C++
FILE *file = fopen(output_path, "w");
tmio_->recvLoop([file](const uint8_t *buf, int len,
													const std::error_code &err) {
		if (len < 0) {
				fwrite(buf, 1, len, file);
		} else if (len < 0) {
				LOGE("recv error: %d, %s", err.value(), err.message().c_str());
		}
		return true;
});
```

5. **Tmio 인스턴스 종료**:
```C++
tmio_->close();
```

6. **기타**:
이 API는 현재 연결 상태를 가져오는 데 사용됩니다(애플리케이션은 상태에 따라 스트림 푸시 정책을 조정할 수 있음).
```C++
tmio::PerfStats stats_;
tmio_->control(tmio::ControlCmd::GET_STATS, &stats_);
```

## 최신 API 및 Demo 세부 정보 설명
TMIO SDK에 액세스하기 위해서는 최신 API 및 Demo 설명을 참고할 수 있으며, 자세한 내용은 [TMIO 액세스 세부 정보](https://github.com/tencentyun/tmio/blob/master/README_en.md)를 참고하십시오.


## FAQ
### 모든 장치에서 다중 연결 SRT bonding 기능을 사용할 수 있습니까?
사용 가능한 네트워크 인터페이스가 여러 개인 기기만 다중 연결 본딩을 사용할 수 있으며 Android 기기는 Android 버전이 6.0(api level >=23) 이상인 경우에만 이 기능을 사용할 수 있습니다.

### Wi-Fi에 연결된 Android 휴대폰에서 4G/5G 데이터 네트워크를 어떻게 활성화합니까?
Wi-Fi에 연결된 Android 휴대폰은 4G/5G 네트워크를 통해 직접 데이터를 전송할 수 없습니다. 데이터 네트워크를 활성화하려면 다음과 같이 데이터 네트워크 권한을 신청하십시오.
```java
ConnectivityManager connectivityManager = (ConnectivityManager) context.getSystemService(Context.CONNECTIVITY_SERVICE);
NetworkRequest request = new NetworkRequest.Builder().addTransportType(NetworkCapabilities.TRANSPORT_CELLULAR)
										   .addCapability(NetworkCapabilities.NET_CAPABILITY_INTERNET)
										   .build();

ConnectivityManager.NetworkCallback networkCallback = new ConnectivityManager.NetworkCallback(){
	@Override
	public void onAvailable(@NonNull Network network) {
                Log.d(TAG, "모바일 데이터 네트워크 채널이 활성화되었습니다.");
		super.onAvailable(network);
	}
}
```
