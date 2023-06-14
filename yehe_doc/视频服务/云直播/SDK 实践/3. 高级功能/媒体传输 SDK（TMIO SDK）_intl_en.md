## Overview
As more and more streaming protocols emerge, it has become a challenge to build an application that supports all protocols. For this, we have developed the Tencent Media IO (TMIO) SDK, which is optimized for mainstream protocols on the market, to help you build stable and highly available media applications with ease.
The TMIO SDK supports mainstream protocols including SRT and QUIC, as well as Tencent’s proprietary protocol, Elastic Transmission Control (ETC). More will be added in the future.

### Strengths
- **Multi-platform support**: The SDK comes in editions for Android, iOS, Linux, macOS, and Windows.
- **Different integration methods**:
   - You can use the non-intrusive [proxy mode](#choose) to use the SDK, with no code changes required.
   - The simple API design also allows you to quickly [integrate](#internal) the SDK into your application, replacing your existing protocols.
- **Simple API design with high compatibility and flexibility**:
   - Easy-to-use APIs are offered.
   - You can choose different modes and policies based on your business scenario.
   - The SDK can be extended to support other protocols.
- **Multi-protocol support and optimization**:
   - The SDK supports emerging streaming protocols including SRT and QUIC, as well as Tencent’s proprietary ETC protocol.
   - It can meet many requirements in different business scenarios.
   - It delivers low-latency, secure, and reliable transfer based on UDP.
   - It supports multi-connection acceleration, which guarantees transfer stability and smoothness.

### Test (TMIO SRT)
- **The TMIO SDK supports the SRT protocol, which can improve upstream stability and downstream smoothness under poor network conditions or in long-distance transfer scenarios.**
  In the test below, with RTMP streaming, playback begins to stutter when packet loss reaches 10%, but for SRT streaming, stability and low latency are guaranteed even with a packet loss of 30%.
  
  <video width="500px" height="auto" src="https://qcloudimg.tencent-cloud.cn/raw/8d165df8dec666b05a013a3def596e0b.mp4" controls  muted></video>


### Features

- **SRT-based streaming media transfer**
  - **High tolerance for random packet loss**
  - **A retransmission mechanism based on ARQ and a timeout policy**
  - **Low-latency, secure, and reliable transfer based on UDT**
  - **Multi-connection transfer and the aggregation transfer mode**:
  You can configure multiple connections to transfer data. For example, mobile devices can transfer data over both Wi-Fi and the 4G/5G data network, so even if one of the connections is disconnected, data transfer will not be affected. This improves transfer reliability.

    <table>
    <thead><tr><th>Transfer Mode</th><th>Description</th></tr></thead>
    <tbody><tr>
    <td>Broadcasting mode</td>
    <td>You can send redundant data over multiple internet connections to ensure data integrity and transfer reliability.</td>
    </tr><tr>
    <td>Primary/Backup mode</td>
    <td>In this mode, only one connection is active at a time. The connection is selected in real time based on stability and reliability. This also reduces bandwidth usage because no redundant data is sent.</td>
    </tr><tr>
    <td>Aggregation mode</td>
    <td>In scenarios requiring a high bitrate and bandwidth, the bandwidth of a single internet connection may be unable to meet the requirements. This mode can split data, send them over multiple connections, and then combine them at the receiver end.</td>
    </tr>
    </tbody></table>

- **QUIC-based media transfer**
  - **Adaptive congestion control algorithm**
  - **Smooth network switch**
  - **Support for the next-generation HTTP/3**
  - **Less redundant data sent when bandwidth is limited or network is unstable**
- **Proprietary streaming protocol ETC**
  - **Innovative, lightweight, and cross-platform**
  - **Support for IoT devices (peer-to-peer communication)**
  - **Quick startup, low latency, and efficient bandwidth utilization**
  - **Quick and accurate detection of internet connection changes to ensure that the optimal transfer policy is always used**
  - **Fair and stable usage of bandwidth when used together with mainstream streaming protocols**


## Integration Directions
The directions below use the RTMP over SRT protocol as an example.

[](id:choose)
### Using the proxy mode
#### Workflow
![](https://qcloudimg.tencent-cloud.cn/raw/4b7d4a5180a9450c2d815161bf060cb2.jpeg)

#### Directions
1. **Create a `TmioProxy` instance**:
```c++
std::unique_ptr<tmio::TmioProxy> proxy_ = tmio::TmioProxy::createUnique();
```
2. **Set the listener**:
```c++
void setListener(TmioProxyListener *listener);
```
Below are the callbacks of `TmioProxyListener`:
<dx-tabs>
::: TMIO configuration callback
You can configure `Tmio` parameters in this callback. **For simple configuration, you can use the auxiliary methods provided in `tmio-preset.h`.**
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
::: TMIO proxy startup callback
```c++
/*
void onStart(const char *local_addr, uint16_t local_port); 
*/
void onStart(const char *addr, uint16_t port) override {
		LOGFI("ip %s, port %" PRIu16, addr, port);
}
```
This callback indicates that the remote server is connected successfully, and the local TCP port is bound successfully. You can start pushing streams.
:::
::: Error callback
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
You can use `ErrorType` to determine whether an error is a local or remote I/O error. A local I/O error is usually because RTMP streaming is stopped by the streamer. Therefore, if streaming has ended, you can ignore such errors. However, a remote I/O error usually needs to be handled.
:::
</dx-tabs>
3. **Start the proxy**:
```c++
std::error_code start(const std::string &local_url, const std::string &remote_url, void * config=nullptr)
```

  - API parameters

<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>local_url</td>
<td>It supports only the TCP scheme in the format of <code>tcp://${ip}:${port}</code>. `port` can be `0`, which indicates to bind a random port. After the binding succeeds, the bound port will be returned to the application through the `onStart()` callback. Using port `0` can avoid binding failures due to issues such as port occupancy and no permissions.</td>
</tr>
<tr>
<td>remote_url</td>
<td>The remote server URL.</td>
</tr>
<tr>
<td>config</td>
<td>The configuration parameter. This parameter is valid if SRT connection bonding or QUIC H3 is enabled. For details, see the definition of the `SrtFeatureConfig` structure in <code>tmio.h</code>.</td>
</tr>
</tbody></table>

  - The sample code for a single connection:

```C++
 proxy_->start(local_url, remote_url, NULL);
```
  - The sample code for multi-connection bonding:
```C++
tmio::TmioFeatureConfig option;
option_.protocol = tmio::Protocol::SRT;
option_.trans_mode = static_cast<int>(tmio::SrtTransMode::SRT_TRANS_BACKUP);
/*-----------------------------------------------------------*/
{
	// You can add multiple connections as needed.
	option_.addAvailableNet(net_name, local_addr, remote_url, 0, weight, -1);
}
/*-----------------------------------------------------------*/

 proxy_->start(local_url, remote_url, &option_);
```
1. **Stop the proxy**:
```c++
/*
void stop();
*/
proxy_.stop();
```

[](id:internal)
### Integrating the TMIO SDK into your application
#### Workflow
![](https://qcloudimg.tencent-cloud.cn/raw/8071536afd22d5df2a9d471ab3dce357.jpg)

## Directions
1. **Create a `Tmio` instance and configure the parameters**:
```C++
tmio_ = tmio::TmioFactory::createUnique(tmio::Protocol::SRT);
tmio::SrtPreset::mpegTsLossless(tmio_.get());
tmio_->setIntOption(tmio::srt_options::CONNECT_TIMEOUT, 4000);
tmio_->setBoolOption(tmio::base_options::THREAD_SAFE_CHECK, true);
```

- **Create a `Tmio` instance**: You can use `TmioFactory` to create it.
- **Configure parameters**: Select different APIs to configure the parameters:
<ul>
<li><strong>Parameters</strong>: See <code>tmio-option.h</code>.</li>
<li><strong>Simple configuration</strong>: See <code>tmio-preset.h</code>.
</ul>

```C++
// Select an appropriate configuration based on different parameter attributes
bool setBoolOption(const std::string &optname, bool value);
bool setIntOption(const std::string &optname, int64_t value);
bool setDoubleOption(const std::string &optname, double value);
bool setStrOption(const std::string &optname, const std::string &value);
...
```

2. **Start connection**:
```C++
/**
 * open the stream specified by url
 *
 * @param config protocol dependent
 */
virtual std::error_code open(const std::string &url,
							  void *config = nullptr) = 0;
```
  - A single connection (`config` can be `NULL`)
```C++
// A single connection by default
auto err = tmio->open(TMIO_SRT_URL);
if (err) {
	LOGE("open failed, %d, %s", err.value(), err.message().c_str());
}
```

 - Multi-connection bonding (currently, only the SRT protocol is supported)
	- For how to set `config` for the SRT bonding feature, see the definition of the `TmioFeatureConfig` structure in the `tmio.h` file.
```C++
tmio::TmioFeatureConfig option_;
option_.protocol = tmio::Protocol::SRT;
option_.trans_mode = static_cast<int>(tmio::SrtTransMode::SRT_TRANS_BACKUP);
option_.addAvailableNet(net_name, local_addr, remote_url, 0, weight, -1);
```
```C++
// Multi-connection bonding
auto err = tmio_->open(TMIO_SRT_URL, &option_);
if (err) {
	LOGE("open failed, %d, %s", err.value(), err.message().c_str());
}
```
  - With multi-connection bonding, you can use the `open` API to add new transfer connections to the group.
3. **Send data**:

```C++
int ret = tmio_->send(buf.data(), datalen, err);
if (ret < 0) {
		LOGE("send failed, %d, %s", err.value(), err.message().c_str());
		break;
}
```

4. **Receive data**:
	- For protocols that involve interactions, such as RTMP, you need to call an API to read the data. We offer two APIs for this:
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
  - Loop read of the upper-layer application:
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
  - Read through callback:
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

5. **Terminate the `Tmio` instance**:
```C++
tmio_->close();
```

6. **More**:
Get the current connection status (your application can adjust its stream push policy based on the status):
```C++
tmio::PerfStats stats_;
tmio_->control(tmio::ControlCmd::GET_STATS, &stats_);
```

## API and Demo Updates
To get the latest updates on the APIs and demos of the SDK, visit [this GitHub page](https://github.com/tencentyun/tmio/blob/master/README_en.md).


## FAQs
### Is SRT multi-connection bonding supported for all devices?
Only devices with multiple available network interfaces can use multi-connection bonding, and Android devices can use this feature only if the Android version is 6.0 or later and the API level is 23 or above.

### How do I enable the 4G/5G data network on an Android phone connected to Wi-Fi?
An Android phone connected to Wi-Fi cannot transfer data directly over the 4G/5G network. To enable the data network, apply for the data network permission as follows:
```java
ConnectivityManager connectivityManager = (ConnectivityManager) context.getSystemService(Context.CONNECTIVITY_SERVICE);
NetworkRequest request = new NetworkRequest.Builder().addTransportType(NetworkCapabilities.TRANSPORT_CELLULAR)
										   .addCapability(NetworkCapabilities.NET_CAPABILITY_INTERNET)
										   .build();

ConnectivityManager.NetworkCallback networkCallback = new ConnectivityManager.NetworkCallback(){
	@Override
	public void onAvailable(@NonNull Network network) {
                Log.d(TAG, "The mobile data network has been enabled");
		super.onAvailable(network);
	}
}
```
