## データ構造と関数の説明
### class ToaFetcher
TOAの取得と解放を管理するためのプリンシパルクラスです。

### InitUpToaFetcher
#### 関数の説明
この関数は、TOA fetcherを初期化するために使用されます。

bool InitUpToaFetcher(char *ncard_ip_str, char *svr_ip_str, u_short svr_port[], u_short svr_port_num, u_short cache_secs=TIMER_CACHE_SECS)

#### インプットパラメータの説明
ncard_ip_strは、ネットワークインターフェイスのIPアドレス文字列、例えば、「10.75.132.39」を識別するために使用されます。このネットワークカードは、次の図に示すように、クライアントと通信するネットワークカードです。
![](https://main.qcloudimg.com/raw/b9af3663b55b043d5891dfc2baa42877.png)
vr_ip_str：TCPストリームをフィルタリングするためのサーバのIPアドレス文字列であり、たとえば、「10.75.132.39」です。
svr_port：TCPストリームをフィルタリングするためのサーバのポートリストであり、最大3つ、少なくとも1つのポートを記入できます。
svr_port_num：サーバのポート数です。
cache_secs：キャッシュ時間（秒単位、デフォルトは15秒）であり、詳細については、toa_fetcher.h：TIMER_CACHE_SECSを参照してください。キャッシュ時間が切れると、TOAは保存されません。

#### 戻り値
TRUE：TOA取得バイパススレッドの作成に成功したことを示します。
FALSE：TOA取得バイパススレッドの作成に失敗したことを示します。

### FetchToaValue
#### 関数の説明
この関数は、TOA値を取得するために使用され、tcp-synパケット交換後、1ms以内にTOAを取得できます。通常、スリーウェイハンドシェイクに1ms以上要します。

bool FetchToaValue(u_long fake_client_ip_addr, u_short fake_client_port, u_long &real_client_ip_addr, u_short &real_client_port)

#### インプットパラメータの説明
fake_client_ip_addr：クライアントのダミーIPアドレスであり、ネットワークバイトオーダーにより記憶され、サーバのaccept関数によって返されたピアアドレスから取得されます。
fake_client_port：クライアントのダミーポート番号であり、ネットワークバイトオーダーにより記憶され、サーバのaccept関数によって返されたピアアドレスから取得されます。
real_client_ip_addr：クライアントの実IPアドレスであり、ネットワークバイトオーダーにより記憶され、TOAから取得されます。
real_client_port：クライアントの実ポート番号であり、ネットワークバイトオーダーにより記憶され、TOAから取得されます。

#### 戻り値
TRUE：TOA取得に成功しました。
FALSE：TOAが取得されていません。通常、キャッシュ時間を超えるとTOAはクリアされます。


### StopToaFetcher
#### 関数の説明
この関数はTOA fetcherを停止するために使用されます。

void StopToaFetcher()

#### インプットパラメータの説明
無し。
#### 戻り値
無し。

### GetFetcherStatus
#### 関数の説明
この関数はFetcher状態を取得するために使用されます。

int GetFetcherStatus()

#### インプットパラメータの説明
無し。
#### 戻り値
0：初期状態を示します。インスタンスが作成された後、初期状態はこの状態で、Fetcherの初期化過程では、状態は変更されませんが、途中でエラーが発生すると、-1に戻り、成功すると、1に戻ります。
-1：異常状態を示します。
1：正常動作中を示します。

### FetchThreadHandler
#### 関数の説明
この関数は、TOAバイパススレッドハンドルを取得するために使用されます。

HANDLE FetchThreadHandler()

 #### インプットパラメータの説明
無し。
#### 戻り値
TOAバイパススレッドハンドルであり、ToaFetcherインスタンスが破棄されると、ハンドルはアクティブに閉じられます。

### FetchErrorInfo
#### 関数の説明
この関数はエラーコードを取得するために使用されます。

bool FetchErrorInfo(int* err_code_ptr, char* err_msg_ptr)

#### インプットパラメータの説明
err_code_ptr：エラーコードに指向する整数型ポインタであり、エラーコードを返すために使用されます。
err_msg_ptr：文字列バッファに指向する文字ポインタであり、少なくとも50バイトで、エラーメッセージを返すために使用されます。

#### 戻り値
TRUE：取得に成功しました。
FALSE：取得異常が発生しました。

## エラーコード
| エラーコード | エラーメッセージ | 説明 |
|---------|---------|---------|
| 0	       | Ok	| 正常 |
| -1001	|Exceed max server port number |	最大ポート数を超えています。CreateToaFetecherThread：svr_port_numを確認してください。 |
| -1002	| Invalid IP address	| 不正なIPv4アドレスです。|
| -1003	| No suitable network interface | 適切なネットワークインターフェイスが見つかりません。|
| -1004	| System Error: find dev error | システムエラー：devが見つかりませんでした。lib開発者に連絡してください。|
| -1005	| System Error: start timer error | システムエラー：タイマー起動エラー。lib開発者に連絡してください。|
| -1006	| System Error: compile filter error | システムエラー：フィルタルールのコンパイルエラー。lib開発者に連絡してください。|
| -1007	| System Error: set filter error | システムエラー：フィルタルールの設定エラー。lib開発者に連絡してください。|
| -1008	| System Error: open pcap error | システムエラー：devオープンエラー。lib開発者に連絡してください。|
| -1009	| System Error: start pcap error | システムエラー：リスナー起動エラー。lib開発者に連絡してください。|
| -1010	| System Error: begin thread error | システムエラー：スレッド起動エラー。lib開発者に連絡してください。|
| -1999	| Unknown error | 未知のエラー。lib開発者に連絡してください。|


## 例
ToaFetcherを初期化します。
```
char ncard_ip_str[] = "1.1.1.1";
char svr_ip_str[] = "1.1.1.1";
u_short svr_port_list[3] = {1111, 2222, 3333};
ToaFetcher inst = ToaFetcher();
inst.InitUpToaFetecher((char*)ncard_ip_str, (char*)svr_ip_str, svr_port_list, 3);
```

TOAを取得します。
```
void GetToa(SOCKADDR_IN client_addr, ToaFetcher * toa_fetcher_ptr)
{
	u_long fake_client_ip_addr = 0;
	u_short fake_client_port = 0;
	u_long real_client_ip_addr = 0;
	u_short real_client_port = 0;
	memcpy(&fake_client_ip_addr, &client_addr.sin_addr, 4);
	memcpy(&fake_client_port, &client_addr.sin_port, 2);
	bool ret = toa_fetcher_ptr->FetchToaValue(fake_client_ip_addr, fake_client_port, real_client_ip_addr, real_client_port);
	if(ret == FALSE){
		printf("No toa found\n");
	}else{
    	//fpp: カスタムプリント関数
		fpp("real_client_ip_addr", &real_client_ip_addr, 4);	
　　fpp("real_client_port", &real_client_port, 2);
	}
}
```













