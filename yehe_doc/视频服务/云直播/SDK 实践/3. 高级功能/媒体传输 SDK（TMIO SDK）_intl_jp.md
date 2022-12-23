## 概要説明
ストリームメディアプロトコルが日々多様化している中、TMIO SDK (Tencent Media IO SDK)は主流のプロトコルを統合、最適化、拡張していることで、複数のプロトコルを開発、デバッグする煩雑な作業からユーザを解放し、安定して動作できるメディアアプリケーションを開発することに協力します。
TMIO SDKでは、ストリームメディアプロトコルSRT向けのカプセル化と最適化がすでに実装されています。他の主流的なプロトコルに対しても引き続き最適化や拡張を行っていきます。

### 機能メリット
- 複数のOSに対応。
  Android、iOS、Linux、Mac、Windows
- 導入方法を柔軟に選択可能。
   - ソースコード侵入なしのプロキシモード。詳しくは、[導入概要](#choose)をご参照ください。
   - APIの設計が簡単なため、既存の転送プロトコルの代替えとして迅速に導入可能。詳しくは、[導入概要](#internal)をご参照ください。
- APIインターフェースの設計が簡単で、互換性と柔軟性が良い。
   - 簡単で使いやすいインターフェースの設計。
   - 運用シーンに応じて、適切なモードとポリシーを選択可能。
   - 他のプロトコルのカスタマイズと最適化を拡張可能。
- SRTをベースにして転送プロトコルをカスタマイズまたは最適化可能。
   - ランダムパケットドロップ対策。
   - UDTベースの低遅延転送。
   - ARQとタイムアウトポリシーをベースにした再転送メカニズム。
   - マルチリンク転送最適化。ブロードキャスト、マスター／スレーブ、集約など多様な転送に対応。

### 機能説明
- **SRTベースのストリームメディア転送機能**。
- **UDTベースの低遅延、安全安心な転送設計**。
- **マルチリンク転送機能。既存機能をリンク集約機能まで拡張**：
マルチリンク転送機能を使用し、複数のリンクを設定してデータ転送を実装できます。特に4G/5Gネットワークが普及している今、モバイル端末デバイスはデータ転送にWi-Fiとモバイルデータネットワークのどちらかに使用することもできます。そのうちの一方が切断されても、1つのリンクさえ使用できれば、通信の安定さを確保できます。
<table>
<thead><tr><th>機能モード</th><th>の説明</th></tr></thead>
<tbody><tr>
<td>ブロードキャストモード</td>
<td>複数の接続を設定することで冗長送信を実装し、データの完全性と接続の信頼性を確保できます。</td>
</tr><tr>
<td>マスター／スレーブ</td>
<td>リンクの安定性と信頼性を参考にして、同一時間に1つのリンクだけがアクティブになっており、リアルタイムで質の良いリンクを選択してデータを転送します。リンクの安定性と信頼性を確保した上で、冗長なデータによって無駄な帯域幅の消費を減らすことができます。</td>
</tr><tr>
<td>集約モード</td>
<td>高いビットレートと帯域幅を要求するシーンでは、単一リンクの帯域幅がニーズを満たせない場合、集約モードを使用すれば、データを複数のリンクに分割して転送すると同時に、受信側で受信したデータを組み立てます。これにより、帯域幅が増えます。</td>
</tr>
</tbody></table>

### 導入方法
以下ではRTMP over SRTプロトコルを例として説明します。

[](id:choose)
### プロキシモードの選択
#### Tmio Proxyモードで導入
![](https://qcloudimg.tencent-cloud.cn/raw/4b7d4a5180a9450c2d815161bf060cb2.jpeg)

#### 操作手順
1. **Tmio Proxyの作成**：

```c++
std::unique_ptr<tmio::TmioProxy> proxy_ = tmio::TmioProxy::createUnique();
```
2. **リスナーの設定**：

```c++
void setListener(TmioProxyListener *listener);
```
TmioProxyListener リスナーインターフェースは以下のとおりです：
<dx-tabs>
::: Tmio 設定のコールバック
ユーザはこのコールバックの中でTmioのパラメータを設定できます。**`tmio-preset.h` を使用して提供できる補助メソッドを簡単に設定できます**。

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
::: TmioProxy 起動のコールバック
```c++
/*
void onStart(const char *local_addr, uint16_t local_port); 
*/
void onStart(const char *addr, uint16_t port) override {
		LOGFI("ip %s, port %" PRIu16, addr, port);
}
```
このコールバックを受信すると、正常にリモートサーバーに接続し、TCPローカルポートと正常にバインドしており、プルを起動できます。
:::
::: エラーメッセージのコールバック
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
ユーザはErrorTypeでローカルIOエラーかリモートIOエラーを区別できます。ローカルIOは通常RTMPプッシュが自発的に発生させます。プッシュを終了すれば、ローカルIOエラーを無視してよいです。しかし、一般的には、リモートIOエラーを無視してはなりません。
:::
</dx-tabs>

3. **プロキシの起動**：
```c++
std::error_code start(const std::string &local_url, const std::string &remote_url, void * config=nullptr)
```
  - インターフェースパラメータ
<table>
<thead>
<tr>
<th>パラメータ</th>
<th>説明</th>
</tr>
</thead>
<tbody><tr>
<td>local_url</td>
<td>TCP Schemeのみをサポートします。フォーマットは<code>tcp://${ip}:${port}</code>です。portは0で構いません。0の場合、ランダムにポートにバインドし、onStart()コールバックで正常にバインドしたポート番号をアプリケーションに返します。0ポートを使用すれば、ポート占有や権限なしによるバインド失敗を回避できます</td>
</tr>
<tr>
<td>remote_url</td>
<td>リモートサーバーURL</td>
</tr>
<tr>
<td>config</td>
<td>設定パラメータ。現在、このパラメータは、SRT bonding機能が有効になっている場合のみ使用され、<code>tmio.h</code>配下のSrtFeatureConfig構造体に基づいて定義してください</td>
</tr>
</tbody></table>

  - シングルリンク（ソースコード例）
```C++
 proxy_->start(local_url, remote_url, NULL);
```
  - マルチリンクバインド（ソースコード例）
```C++
tmio::SrtFeatureConfig option;
option_.protocol = tmio::Protocol::SRT;
option_.trans_mode = tmio::SrtTransMode::SRT_TRANS_BACKUP;
/*-----------------------------------------------------------*/
{
	//作成するリンク数に応じて複数のリンクを追加できます
	option_.addAvailableNet(net_name, local_addr, remote_url, 0, weight, -1);
}
/*-----------------------------------------------------------*/

 proxy_->start(local_url, remote_url, &option_);
```
3. **停止**：
```c++
/*
void stop();
*/
proxy_.stop();
```

[](id:internal)
### 内部統合
#### Tmio SDKの内部に導入方法を統合します
![](https://qcloudimg.tencent-cloud.cn/raw/4b7d4a5180a9450c2d815161bf060cb2.jpeg)

#### 導入プロセス
1. **Tmio&設定パラメータの作成**（ソースコード例）：
```C++
tmio_ = tmio::TmioFactory::createUnique(tmio::Protocol::SRT);
tmio::SrtPreset::mpegTsLossless(tmio_.get());
tmio_->setIntOption(tmio::srt_options::CONNECT_TIMEOUT, 4000);
tmio_->setBoolOption(tmio::base_options::THREAD_SAFE_CHECK, true);
```

  - **Tmioの作成**：`TmioFactory`で作成します。
  - **パラメータの設定**：パラメータによってインターフェースを選択し設定を実装します：
	<ul>
	<li><strong>パラメータ名</strong>：詳しくは、<code>tmio-option.h</code>をご参照ください。</li>
	<li><strong>簡単な設定</strong>：詳しくは、<code>tmio-preset.h</code>をご参照ください。
	</ul>

```C++
//パラメータのプロパティによって適切な設定を選択します
bool setBoolOption(const std::string &optname, bool value);
bool setIntOption(const std::string &optname, int64_t value);
bool setDoubleOption(const std::string &optname, double value);
bool setStrOption(const std::string &optname, const std::string &value);
...
```
2. **接続開始**（ソースコード例）：

```C++
/**
 * open the stream specified by url
 *
 * @param config protocol dependent
 */
virtual std::error_code open(const std::string &url,
							  void *config = nullptr) = 0;
```
  - シングルリンク（configにNULLを指定して構わない）
```C++
//デフォルトではシングルリンクとします
auto err = tmio->open(TMIO_SRT_URL);
if (err) {
	LOGE("open failed, %d, %s", err.value(), err.message().c_str());
}
```
  - マルチリンクバインド（現在SRTプロトコルのみ対応）
	- configを設定する時、SRT bondingの設定パラメータは`tmio.h`ファイル中のSrtFeatureConfigを参考にして定義します。
```C++
tmio::SrtFeatureConfig option_;
option_.protocol = tmio::Protocol::SRT;
option_.trans_mode = tmio::SrtTransMode::SRT_TRANS_BACKUP;
option_.addAvailableNet(net_name, local_addr, remote_url, 0, weight, -1);
```
```C++
//マルチリンクをバインドします
auto err = tmio_->open(TMIO_SRT_URL, &option_);
if (err) {
	LOGE("open failed, %d, %s", err.value(), err.message().c_str());
}
```
  -  マルチリンクbonding openインターフェースは、groupグループに新しいリンクを追加することにも使用できます。
3. **データの送信**：

```C++
int ret = tmio_->send(buf.data(), datalen, err);
if (ret < 0) {
		LOGE("send failed, %d, %s", err.value(), err.message().c_str());
		break;
}
```
4. **データの受信**：

	- インタラクションを必要とするプロトコル（RTMPなど）の場合、受信インータ―フェースを有効にしデータを読み取りプロトコル間のインタラクションを行う必要があります。以下では、2つのインターフェースの呼出しを提供します。

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
  - 上位のアプリケーションを繰り返して読み取ります
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
  - コールバックを読み取ります
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
5. **Tmioの停止**：

```C++
tmio_->close();
```
6. **その他**：
現在のリンク状態を取得します（アプリケーションは状態に応じてプルポリシーを調整します）。
```C++
tmio::PerfStats stats_;
tmio_->control(tmio::ControlCmd::GET_STATS, &stats_);
```

## よくあるご質問
### すべてのデバイスでマルチリンクバインド機能を使用できますか？
マルチリンク機能を使用する前提は、デバイスに複数の使用可能なネットワークインターフェースがあることです。なお、OSがAndroidのデバイスの場合、6.0（api level >=23）以降のバージョンも要求しています。

### Android系の携帯電話がWi-Fiに接続している場合、どのように4G/5Gモバイルネットワークを有効にしますか？
Android系の携帯電話がWi-Fiに接続していれば、4G/5Gモバイルネットワークをそのまま使用できます。4G/5Gモバイルネットワークを使用するには、4G/5Gモバイルネットワークを使用する権限を申請する必要があります。ソースコードは以下のとおりです：
```java
ConnectivityManager connectivityManager = (ConnectivityManager) context.getSystemService(Context.CONNECTIVITY_SERVICE);
NetworkRequest request = new NetworkRequest.Builder().addTransportType(NetworkCapabilities.TRANSPORT_CELLULAR)
										   .addCapability(NetworkCapabilities.NET_CAPABILITY_INTERNET)
										   .build();

ConnectivityManager.NetworkCallback networkCallback = new ConnectivityManager.NetworkCallback(){
	@Override
	public void onAvailable(@NonNull Network network) {
		Log.d(TAG, "4/5gチャネルが有効になっています。");
		super.onAvailable(network);
	}
}
```