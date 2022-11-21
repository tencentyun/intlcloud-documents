## Overview
As more and more streaming media transfer protocols emerge, the Tencent Media IO (TMIO) SDK integrates, optimizes, and extends mainstream protocols to help you easily develop stable and available media applications, freeing you from laborious development and debugging of various protocols.
The TMIO SDK encapsulates and optimizes the SRT protocol, and it will continue to be extended to optimize more mainstream streaming media protocols in the future.

### Strengths
- Multi-platform support
  It supports Android, iOS, Linux, macOS, and Windows.
- Flexible integration methods
   - It offers non-intrusive proxy modes as described in [Selecting the proxy mode](#choose).
   - Based on the simple API design, it can be quickly integrated to replace the existing transfer protocol as instructed in [Internal integration](#internal).
- Simple API design with high compatibility and flexibility
   - Easy-to-use APIs are offered.
   - It allows you to select an appropriate mode and policy based on your business requirements and scenarios.
   - It can be extended to customize and optimize other protocols.
- SRT-based customization and optimization of transfer protocols
   - It delivers a high random packet loss prevention rate.
   - It can transfer data at a low latency based on UDT.
   - It implements a retransmission mechanism based on ARQ and a timeout policy.
   - It optimizes multi-linkage transfer to support various transfer modes, including broadcasting, primary/secondary, and aggregation.

### Feature description
- **SRT-based streaming media transfer**
- **Low-latency, secure, and reliable transfer design based on UDT**
- **Multi-linkage transfer with the new linkage aggregation feature**
The multi-linkage transfer feature enables you to configure multiple linkages to transfer data. In the current era where 4G/5G networks are widely used, mobile devices can transfer data over both Wi-Fi and the data network, so the linkage stability can be guaranteed even if only one linkage is available when a network is disconnected suddenly.
<table>
<thead><tr><th>Feature Mode</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Broadcasting mode</td>
<td>In this mode, you can configure multiple linkages to send redundant data, which ensures the data integrity and linkage reliability.</td>
</tr><tr>
<td>Primary/Secondary mode</td>
<td>In this mode, only one linkage is active at a time based on the linkage stability and reliability, and the optimal linkage is selected in real time for data transfer. This not only guarantees the linkage stability and reliability but also reduces the bandwidth usage of redundant data.</td>
</tr><tr>
<td>Aggregation mode</td>
<td>In scenarios requiring a high bitrate and bandwidth, if the bandwidth of a single linkage cannot meet the requirements, this mode can split data and send the data over multiple linkages and then recombine the data at the receiver end, so as to increase the available bandwidth.</td>
</tr>
</tbody></table>

## Integration Method
Taking the RTMP over SRT protocol as an example:

[](id:choose)
### Selecting the proxy mode
#### Integration in `TmioProxy` mode
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
The `TmioProxyListener` listener API is as detailed below:
<dx-tabs>
::: The callback for `Tmio` configuration
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
::: The callback for `TmioProxy` startup
```c++
/*
void onStart(const char *local_addr, uint16_t local_port); 
*/
void onStart(const char *addr, uint16_t port) override {
		LOGFI("ip %s, port %" PRIu16, addr, port);
}
```
If this callback is received, the remote server is connected successfully, the local TCP port is bound successfully, and the stream can be pushed.
:::
::: The callback for an error message
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
You can identify a local or remote I/O error based on `ErrorType`. Local I/O errors are usually triggered by RTMP stream push actively, for example, when stream push is stopped, and can be ignored generally. However, remote I/O errors should not be ignored generally.
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
<td>The remote server URL</td>
</tr>
<tr>
<td>config</td>
<td>The configuration parameter, which takes effect only when the SRT bonding feature is enabled. For its specific definition, see the definition of the `SrtFeatureConfig` structure in <code>tmio.h</code>.</td>
</tr>
</tbody></table>

  - The sample code for a single linkage:
```C++
 proxy_->start(local_url, remote_url, NULL);
```
  - The sample code for multi-linkage bonding:
```C++
tmio::SrtFeatureConfig option;
option_.protocol = tmio::Protocol::SRT;
option_.trans_mode = tmio::SrtTransMode::SRT_TRANS_BACKUP;
/*-----------------------------------------------------------*/
{
	// You can add multiple linkages as needed.
	option_.addAvailableNet(net_name, local_addr, remote_url, 0, weight, -1);
}
/*-----------------------------------------------------------*/

 proxy_->start(local_url, remote_url, &option_);
```
3. **Stop**:
```c++
/*
void stop();
*/
proxy_.stop();
```

[](id:internal)
### Internal integration
#### Internal integration in the TMIO SDK
![](https://qcloudimg.tencent-cloud.cn/raw/8071536afd22d5df2a9d471ab3dce357.jpg)

#### Integration process
1. **Create a `Tmio` instance and configure the parameters** as follows:
```C++
tmio_ = tmio::TmioFactory::createUnique(tmio::Protocol::SRT);
tmio::SrtPreset::mpegTsLossless(tmio_.get());
tmio_->setIntOption(tmio::srt_options::CONNECT_TIMEOUT, 4000);
tmio_->setBoolOption(tmio::base_options::THREAD_SAFE_CHECK, true);
```
  - **Create a `Tmio` instance**: You can use `TmioFactory` to create it.
  - **Configure parameters**: Select different APIs to configure the parameters:
	<ul>
	<li><strong>Parameter</strong>: See <code>tmio-option.h</code>.</li>
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
2. **Start connection** as follows:

```C++
/**
 * open the stream specified by url
 *
 * @param config protocol dependent
 */
virtual std::error_code open(const std::string &url,
							  void *config = nullptr) = 0;
```
  - A single linkage (`config` can be `NULL`)
```C++
// A single linkage by default
auto err = tmio->open(TMIO_SRT_URL);
if (err) {
	LOGE("open failed, %d, %s", err.value(), err.message().c_str());
}
```
  - Multi-linkage bonding (currently, only the SRT protocol is supported)
		- To set `config` for the SRT bonding feature, see the definition of the `SrtFeatureConfig` structure in the `tmio.h` file.
```C++
tmio::SrtFeatureConfig option_;
option_.protocol = tmio::Protocol::SRT;
option_.trans_mode = tmio::SrtTransMode::SRT_TRANS_BACKUP;
option_.addAvailableNet(net_name, local_addr, remote_url, 0, weight, -1);
```
```C++
// Multi-linkage bonding
auto err = tmio_->open(TMIO_SRT_URL, &option_);
if (err) {
	LOGE("open failed, %d, %s", err.value(), err.message().c_str());
}
```
  - The multi-linkage bonding `open` API can be used to add new linkages to the group for data transfer.
3. **Send the data**:

```C++
int ret = tmio_->send(buf.data(), datalen, err);
if (ret < 0) {
		LOGE("send failed, %d, %s", err.value(), err.message().c_str());
		break;
}
```
4. **Receive the data**:

	- If the protocol requires interaction such as RTMP, you need to enable a data receiving API to read the data and complete the protocol interaction. Here, two APIs are provided:
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
5. **Shut down the `Tmio` instance**:
```C++
tmio_->close();
```
6. **More**:
This API is used to get the current linkage status (the application can adjust the stream push policy based on the status).
```C++
tmio::PerfStats stats_;
tmio_->control(tmio::ControlCmd::GET_STATS, &stats_);
```

## FAQs
### Can all devices use the multi-linkage bonding feature?
Only devices with multiple available network interfaces can use multi-linkage bonding, and Android devices can use this feature only if the Android version is 6.0 or later and the API level is 23 or above.

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
		Log.d(TAG, "The 4G/5G channel is enabled.");
		super.onAvailable(network);
	}
}
```