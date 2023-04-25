## 概要説明
ストリームメディアプロトコルが日々多様化している中、TMIO SDK (Tencent Media IO SDK)は主流のプロトコルを統合、最適化、拡張していることで、複数のプロトコルを開発、デバッグする煩雑な作業からユーザを解放し、安定して動作できるメディアアプリケーションを開発することに協力します。
TMIO SDKは現在、SRTやQUICなどの主流のメディアプロトコルを最適化、拡張し、同時に自社開発の伝送制御プロトコルETC（正式名称：Elastic Transmission Control）を追加し、今後も他の主流のプロトコルの最適化および拡張機能を追加し続けます。

### 機能メリット
- **マルチプラットフォームのサポート**：Android、iOS、Linux、Mac、およびWindowsを含みます。
- **アクセス方法の柔軟な選択**：
   - ソースコード侵入なしのプロキシモード。詳しくは、[導入概要](#choose)をご参照ください。
   - APIの設計が簡単なため、既存の転送プロトコルの代替えとして迅速に導入可能。詳しくは、[導入概要](#internal)をご参照ください。
- **APIインターフェースの設計が簡単で、互換性と柔軟性が良い**。
   - 簡単で使いやすいインターフェースの設計。
   - 運用シーンに応じて、適切なモードとポリシーを選択可能。
   - 他のプロトコルのカスタマイズと最適化を拡張可能。
- **複数の伝送プロトコルを統合し、拡張および最適化します**：
   - SRT、QUICなどの新世代の主流伝送プロトコルと自社開発の伝送制御プロトコルETCサポート。
   - さまざまなサービスケースに適用可能なさまざまなニーズの選択。
   - UDTベースの低遅延、安全で信頼できる伝送設計に基づきます。
   - マルチリンクアクセラレーションの利点により、より安定したスムーズな伝送が保証されます。

### 効果の表示（TMIO SRTを例に）
- **TMIOはSRTプロトコルをサポートし、弱いネットワークや長距離伝送のシナリオで使用して、アップリンクの安定性とダウンリンクのスムーズさを向上させることができます。**
  次のテストシナリオでは、パケットロス率が10%の場合にRTMPプッシュにラグが発生し、パケットロス率が10%または30%の場合でも、SRTプッシュは安定性と低遅延を維持できます。
  
  <video width="500px" height="auto" src="https://qcloudimg.tencent-cloud.cn/raw/8d165df8dec666b05a013a3def596e0b.mp4" controls  muted></video>


### 機能の説明

- **SRTベースのストリームメディア転送機能**。
  - **ランダムなパケットロスに対する強い耐性**。
  - **ARQとタイムアウトポリシーをベースにした再転送メカニズム**。
  - **UDTベースの低遅延、安全安心な転送設計**。
  - **マルチリンク転送機能。既存機能をリンク集約機能まで拡張**：
  マルチリンク転送機能を使用し、複数のリンクを設定してデータ転送を実装できます。特に4G/5Gネットワークが普及している今、モバイル端末デバイスはデータ転送にWi-Fiとモバイルデータネットワークのどちらかに使用することもできます。そのうちの一方が切断されても、1つのリンクさえ使用できれば、通信の安定性を確保できます。

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

- **QUICによるストリーミングメディア伝送機能**
  - **自己適応な輻輳制御アルゴリズム**
  - **ネットワーク接続の移行をサポートし、スムーズで感知無し**
  - **次世代のHTTP3基本伝送プロトコルをサポート**
  - **帯域幅とジッターが制限されている環境では、冗長データの送信が少なくなり、帯域幅のコストが節約され、メリットが明らかになる**
- **自社開発の伝送制御プロトコルETC**
  - **完全自社開発、軽量、クロスプラットフォーム**
  - **IoTデバイスをサポートし、エンドツーエンドの通信に適する**
  - **高速起動、低遅延、高帯域幅使用率**
  - **リンクステータスの変化を迅速かつ正確に認識し、最適な伝送ポリシーに合わせて調整する**
  - **主流の伝送プロトコルと共存すると、帯域幅をより公平かつ安定的に使用できる**


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
このコールバックを受信すると、正常にリモートサーバーに接続し、TCPローカルポートと正常に関連付けており、プルを起動できます。
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
<td>TCP Schemeのみをサポートします。フォーマットは<code>tcp://${ip}:${port}</code>です。portは0で構いません。0の場合、ランダムにポートに関連付け、onStart()コールバックで正常に関連付けたポート番号をアプリケーションに返します。0ポートを使用すれば、ポート占有や権限なしによる関連付け失敗を回避できます</td>
</tr>
<tr>
<td>remote_url</td>
<td>リモートサーバーURL</td>
</tr>
<tr>
<td>config</td>
<td>設定パラメータ。このパラメータは、SRT bonding機能およびQUIC H3プロトコルが有効になっている場合に使用され、具体的には<code>tmio.h</code>配下のTmioFeatureConfig構造体に基づいて定義してください</td>
</tr>
</tbody></table>

  - シングルリンク（ソースコード例）

```C++
 proxy_->start(local_url, remote_url, NULL);
```
  - bonding マルチリンク（ソースコード例）
```C++
tmio::TmioFeatureConfig option;
option_.protocol = tmio::Protocol::SRT;
option_.trans_mode = static_cast<int>(tmio::SrtTransMode::SRT_TRANS_BACKUP);
/*-----------------------------------------------------------*/
{
	//作成するリンク数に応じて複数のリンクを追加できます
	option_.addAvailableNet(net_name, local_addr, remote_url, 0, weight, -1);
}
/*-----------------------------------------------------------*/

 proxy_->start(local_url, remote_url, &option_);
```
1. **停止**：
```c++
/*
void stop();
*/
proxy_.stop();
```

[](id:internal)
### 内部統合
#### Tmio SDKの内部に導入方法を統合します
![](https://qcloudimg.tencent-cloud.cn/raw/8071536afd22d5df2a9d471ab3dce357.jpg)

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

 - bonding マルチリンク（現在SRTプロトコルのみ対応）
	- configを設定する時、SRT bondingの設定パラメータは`tmio.h`ファイル構造のTmioFeatureConfigを参考にして定義します。
```C++
tmio::TmioFeatureConfig option_;
option_.protocol = tmio::Protocol::SRT;
option_.trans_mode = static_cast<int>(tmio::SrtTransMode::SRT_TRANS_BACKUP);
option_.addAvailableNet(net_name, local_addr, remote_url, 0, weight, -1);
```
```C++
//bonding マルチリンク
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

## 最新のAPIインターフェースおよびDemoの詳細な説明
TMIO SDKへのアクセスは、最新のAPIインターフェースおよびDemoの説明を参照することができます。詳細については、[TMIOアクセスの詳細](https://github.com/tencentyun/tmio)をご参照ください。


## よくあるご質問
### すべてのデバイスでSRT bonding機能を使用できますか？
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
                Log.d(TAG, 「モバイルデータインターネットチャネルはオンです.");
		super.onAvailable(network);
	}
}
```