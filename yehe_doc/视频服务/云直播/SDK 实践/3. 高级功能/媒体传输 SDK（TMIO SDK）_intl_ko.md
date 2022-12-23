## 개요
점점 더 많은 스트리밍 미디어 전송 프로토콜이 등장함에 따라 TMIO SDK(Tencent Media IO SDK)는 주요 프로토콜을 통합, 최적화 및 확장하여 안정적이고 사용 가능한 미디어 애플리케이션을 쉽게 개발할 수 있도록 지원하여 다양한 프로토콜의 힘든 개발 및 디버깅에서 자유로울 수 있게 합니다.
TMIO SDK는 SRT 프로토콜을 캡슐화하고 최적화하며 향후 더 많은 주요 스트리밍 미디어 프로토콜을 최적화하도록 계속 확장될 것입니다.

### 강점
- 멀티 플랫폼 지원
  Android, iOS, Linux, Mac 및 windows를 지원합니다.
- 유연한 통합 방법
   - [프록시 모드 선택](#choose)에 설명된 대로 비간섭 프록시 모드를 제공합니다.
   - 간단한 API 설계를 기반으로 신속하게 통합하여 기존 전송 프로토콜을 대체할 수 있습니다. [내부 통합](#internal)을 참고하십시오.
- API 설계가 간단하고 호환성과 유연성이 높습니다.
   - 사용하기 쉬운 API가 제공됩니다.
   - 비즈니스 요구 사항 및 시나리오에 따라 적절한 모드와 정책을 선택할 수 있습니다.
   - 다른 프로토콜을 사용자 지정하고 최적화하도록 확장할 수 있습니다.
- 전송 프로토콜의 SRT를 기반으로 맞춤화 및 최적화합니다.
   - 높은 랜덤 패킷 손실 방지율을 제공합니다.
   - UDT를 기반으로 데이터를 저지연 전송할 수 있습니다.
   - ARQ 및 타임아웃 정책에 기반한 재전송 메커니즘을 구현합니다.
   - 다중 연결 전송을 최적화하여 방송, 프라이머리/세컨더리 및 취합을 포함한 다양한 전송 모드를 지원합니다.

### 기능 소개
- **SRT 기반 스트리밍 미디어 전송**.
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
<th>설명</th>
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
<td>SRT bonding 기능이 활성화된 경우에만 적용되는 구성 매개변수입니다. 구체적인 정의는 <code>tmio.h</code>의 SrtFeatureConfig 구조 정의를 참고하십시오.</td>
</tr>
</tbody></table>

  - 단일 연결(예시 코드)
```C++
 proxy_->start(local_url, remote_url, NULL);
```
  - 다중 연결 bonding(예시 코드)
```C++
tmio::SrtFeatureConfig option;
option_.protocol = tmio::Protocol::SRT;
option_.trans_mode = tmio::SrtTransMode::SRT_TRANS_BACKUP;
/*-----------------------------------------------------------*/
{
	// 필요에 따라 여러 연결을 추가할 수 있습니다
	option_.addAvailableNet(net_name, local_addr, remote_url, 0, weight, -1);
}
/*-----------------------------------------------------------*/

 proxy_->start(local_url, remote_url, &option_);
```
3. **중지**:
```c++
/*
void stop();
*/
proxy_.stop();
```

[](id:internal)
### 내부 통합
#### Tmio SDK의 내부 통합
![](https://qcloudimg.tencent-cloud.cn/raw/ffad74f4bebbc9cea6eb780a937dc0b9.jpeg)

#### 통합 프로세스
1. **Tmio 인스턴스 생성&매개변수 구성**(예시 코드):

```C++
tmio_ = tmio::TmioFactory::createUnique(tmio::Protocol::SRT);
tmio::SrtPreset::mpegTsLossless(tmio_.get());
tmio_->setIntOption(tmio::srt_options::CONNECT_TIMEOUT, 4000);
tmio_->setBoolOption(tmio::base_options::THREAD_SAFE_CHECK, true);
```

  - **Tmio 생성**: `TmioFactory`를 사용하여 만들 수 있습니다.
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
	 - SRT bonding 기능에 대한 config를 설정하려면 `tmio.h` 파일의 SrtFeatureConfig 구조 정의를 참고하십시오.
```C++
tmio::SrtFeatureConfig option_;
option_.protocol = tmio::Protocol::SRT;
option_.trans_mode = tmio::SrtTransMode::SRT_TRANS_BACKUP;
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

## FAQ
### 모든 장치에서 다중 연결 bonding 기능을 사용할 수 있습니까?
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
		Log.d(TAG, "4/5g 채널이 활성화 되었습니다.");
		super.onAvailable(network);
	}
}
```