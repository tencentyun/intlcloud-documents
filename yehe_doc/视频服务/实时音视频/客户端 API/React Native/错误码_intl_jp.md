## エラーコードリスト
### 基本的なエラーコード

| 記号 | 値 | 意味 |
|---|---|---|
|ERR_NULL|0|エラーなし|

### 入室関連のエラーコード

TRTCCloud.enterRoom() 入室に失敗したときにこのタイプのエラーコードがトリガーされます。コールバック関数TRTCCloudDelegate.onEnterRoom()、TRTCCloudDelegate.OnError()によって、関連通知をキャプチャできます。

| 記号 | 値 | 意味 |
|---|---|---|
|ERR_ROOM_ENTER_FAIL|-3301|入室の失敗|
|ERR_ENTER_ROOM_PARAM_NULL|-3316|入室パラメータが空です。TRTCCloud.enterRoom():インターフェースの呼び出しが有効なparamで渡されるかどうか確認してください|
|ERR_SDK_APPID_INVALID|-3317|入室パラメータsdkAppIdエラー|
|ERR_ROOM_ID_INVALID|-3318|入室パラメータroomIdエラー|
|ERR_USER_ID_INVALID|-3319|入室パラメータuserIDが正しくありません|
|ERR_USER_SIG_INVALID|-3320|入室パラメータuserSigが正しくありません|
|ERR_ROOM_REQUEST_ENTER_ROOM_TIMEOUT|-3308|入室リクエストがタイムアウトしました。ネットワークをご確認ください|
|ERR_SERVER_INFO_SERVICE_SUSPENDED|-100013|サービスをご利用いただけません。パッケージの残りの分数が0より大きいかどうか、Tencent Cloudアカウントの支払いが遅延していないかどうかご確認ください|


### 退室関連のエラーコード

TRTCCloud.exitRoom() 入室に失敗したときにこのタイプのエラーコードがトリガーされます。コールバック関数TRTCCloudDelegate.onEnterRoom()、TRTCCloudDelegate.OnError()によって、関連通知をキャプチャできます。

| 記号 | 値 | 意味 |
|---|---|---|
|ERR_ROOM_REQUEST_QUIT_ROOM_TIMEOUT|-3325|退室リクエストのタイムアウト|


### デバイス（カメラ、マイク、スピーカー）関連のエラーコード

コールバック関数TRTCCloudDelegate.OnError()によって、関連通知をキャプチャできます。

| 記号 | 値 | 意味 |
|---|---|---|
|ERR_CAMERA_START_FAIL|-1301|カメラの起動に失敗しました。例えば、WindowsまたはMacデバイスの場合、カメラのコンフィギュレーター（ドライバー）に異常があります。デバイスを無効にしてから再度有効にするか、マシンを再起動するか、またはコンフィギュレーターを更新してください|
|ERR_CAMERA_NOT_AUTHORIZED|-1314|カメラデバイスの権限が承認されていません。通常はモバイルデバイスに表示されます。ユーザーから権限承認を拒否されている可能性があります|
|ERR_CAMERA_SET_PARAM_FAIL|-1315|カメラパラメータ設定エラー（パラメータがサポートされていないか、その他）|
|ERR_CAMERA_OCCUPY|-1316|カメラが使用中なので、他のカメラの起動を試みることができます|
|ERR_MIC_START_FAIL|-1302|マイクの起動に失敗しました。例えば、WindowsまたはMacデバイスの場合、マイクのコンフィギュレーター（ドライバー）に異常があります。デバイスを無効にしてから再度有効にするか、マシンを再起動するか、またはコンフィギュレーターを更新してください|
|ERR_MIC_NOT_AUTHORIZED|-1317マイクデバイスの権限が承認されていません。通常はモバイルデバイスに表示されます。ユーザーから権限承認を拒否されている可能性があります|
|ERR_MIC_SET_PARAM_FAIL|-1318|マイクパラメータの設定に失敗しました|
|ERR_MIC_OCCUPY|-1319|マイクが使用中です。例えば、モバイルデバイスが通話中の場合、マイクの起動は失敗します|
|ERR_MIC_STOP_FAIL|-1320|マイクの停止に失敗しました|
|ERR_SPEAKER_START_FAIL|-1321|スピーカーの起動に失敗しました。例えば、WindowsまたはMacデバイスの場合、スピーカーのコンフィギュレーター（ドライバー）に異常があります。デバイスを無効にしてから再度有効にするか、マシンを再起動するか、またはコンフィギュレーターを更新してください|
|ERR_SPEAKER_SET_PARAM_FAIL|-1322|スピーカーパラメータの設定に失敗しました|
|ERR_SPEAKER_STOP_FAIL|-1323|スピーカーの停止に失敗しました|


### 画面共有関連のエラーコード

コールバック関数TRTCCloudDelegate.OnError()によって、関連通知をキャプチャできます。

| 記号 | 値 | 意味 |
|---|---|---|
|ERR_SCREEN_CAPTURE_START_FAIL|-1308|画面録画の開始に失敗しました。モバイルデバイスに表示されるときは、ユーザーから権限承認を拒否されている可能性があります。WindowsまたはMacシステムのデバイスに表示される場合は、画面録画インターフェースのパラメータが要件を満たしているかご確認ください|
|ERR_SCREEN_CAPTURE_UNSURPORT|-1309|画面録画に失敗しました。Androidプラットフォームでは5.0以降のシステム、iOSプラットフォームでは11.0以降のシステムが必要です|
|ERR_SERVER_CENTER_NO_PRIVILEDGE_PUSH_SUB_VIDEO|-102015|サブチャネルのアップストリームの権限がありません|
|ERR_SERVER_CENTER_ANOTHER_USER_PUSH_SUB_VIDEO|-102016|他のユーザーがサブチャネルのアップストリームを行っています|
|ERR_SCREEN_CAPTURE_STOPPED|-7001|画面録画がシステムによって停止されました|


### コーデック関連のエラーコード

コールバック関数TRTCCloudDelegate.OnError()によって、関連通知をキャプチャできます。

| 記号 | 値 | 意味 |
|---|---|---|
|ERR_VIDEO_ENCODE_FAIL|-1303|ビデオフレームのエンコードに失敗しました。例えば、iOSデバイスを他のアプリケーションに切り替えると、システムによってハードウェアエンコーダが解放される場合があります。切り替えて元に戻すと、ハードウェアエンコーダが再起動する前にスローされる場合があります|
|ERR_UNSUPPORTED_RESOLUTION|-1305|サポートされていないビデオ解像度|
|ERR_AUDIO_ENCODE_FAIL|-1304|オーディオフレームのエンコードに失敗しました。例えば、渡されたカスタムオーディオデータを、SDKで処理することはできません|
|ERR_UNSUPPORTED_SAMPLERATE|-1306|サポートされていないオーディオサンプルレート|


### ユーザー定義キャプチャ関連のエラーコード

コールバック関数TRTCCloudDelegate.OnError()によって、関連通知をキャプチャできます。

| 記号 | 値 | 意味 |
|---|---|---|
|ERR_PIXEL_FORMAT_UNSUPPORTED|-1327|設定されたpixel formatはサポートされていません|
|ERR_BUFFER_TYPE_UNSUPPORTED|-1328|設定されたbuffer typeはサポートされていません|


### CDNバインディングおよびミクスストリーミング関連のエラーコード

コールバック関数TRTCCloudDelegate.onStartPublishing()、TRTCCloudDelegate.onSetMixTranscodingConfig()によって関連通知をキャプチャできます。

| 記号 | 値 | 意味 |
|---|---|---|
|ERR_PUBLISH_CDN_STREAM_REQUEST_TIME_OUT|-3321|バイパス転送リクエストのタイムアウト|
|ERR_CLOUD_MIX_TRANSCODING_REQUEST_TIME_OUT|-3322|クラウドミクスストリーミングリクエストのタイムアウト|
|ERR_PUBLISH_CDN_STREAM_SERVER_FAILED|-3323|バイパス転送リターンパケットの異常|
|ERR_CLOUD_MIX_TRANSCODING_SERVER_FAILED|-3324|クラウドミクスストリーミング・リターンパケットの異常|
|ERR_ROOM_REQUEST_START_PUBLISHING_TIMEOUT|-3333|Tencent CloudへのライブCDNのプッシュ開始シグナリングのタイムアウト|
|ERR_ROOM_REQUEST_START_PUBLISHING_ERROR|-3334||Tencent CloudへのライブCDNのプッシュ開始シグナリングの異常|
|ERR_ROOM_REQUEST_STOP_PUBLISHING_TIMEOUT|-3335|Tencent CloudへのライブCDNのプッシュ停止シグナリングのタイムアウト|
|ERR_ROOM_REQUEST_STOP_PUBLISHING_ERROR|-3336|Tencent CloudへのライブCDNのプッシュ停止シグナリングの異常|


### ルーム間マイク接続関連のエラーコード

TRTCCloud.ConnectOtherRoom() ルーム間マイク接続に失敗したときにこのタイプのエラーコードがトリガーされます。コールバック関数TRTCCloudDelegate.onConnectOtherRoom()によって、関連通知をキャプチャできます。

| 記号 | 値 | 意味 |
|---|---|---|
|ERR_ROOM_REQUEST_CONN_ROOM_TIMEOUT|-3326|マイク接続リクエストのタイムアウト|
|ERR_ROOM_REQUEST_DISCONN_ROOM_TIMEOUT|-3327|マイク接続からの退出リクエストのタイムアウト|
|ERR_ROOM_REQUEST_CONN_ROOM_INVALID_PARAM|-3328|無効なパラメータ|
|ERR_CONNECT_OTHER_ROOM_AS_AUDIENCE|-3330|現在のロールは視聴者であり、ルーム間マイク接続をリクエストまたは切断することはできません。まずキャスターにswitchRole()する必要があります|
|ERR_SERVER_CENTER_CONN_ROOM_NOT_SUPPORT|-102031|ルーム間マイク接続はサポートされていません|
|ERR_SERVER_CENTER_CONN_ROOM_REACH_MAX_NUM|-102032|ルーム間マイク接続の上限に達しました|
|ERR_SERVER_CENTER_CONN_ROOM_REACH_MAX_RETRY_TIMES|-102033|ルーム間マイク接続の再試行回数の上限に達しました|
|ERR_SERVER_CENTER_CONN_ROOM_REQ_TIMEOUT|-102034|ルーム間マイク接続リクエストのタイムアウト|
|ERR_SERVER_CENTER_CONN_ROOM_REQ|-102035|ルーム間マイク接続リクエストの形式エラー|
|ERR_SERVER_CENTER_CONN_ROOM_NO_SIG|-102036|ルーム間マイク接続に署名がありません|
|ERR_SERVER_CENTER_CONN_ROOM_DECRYPT_SIG|-102037|ルーム間マイク接続の署名復号に失敗しました|
|ERR_SERVER_CENTER_CONN_ROOM_NO_KEY|-102038|ルーム間マイク接続の署名復号キーが見つかりませんでした|
|ERR_SERVER_CENTER_CONN_ROOM_PARSE_SIG|-102039|ルーム間マイク接続の署名解析エラー|
|ERR_SERVER_CENTER_CONN_ROOM_INVALID_SIG_TIME|-102040|ルーム間マイク接続の署名タイムスタンプエラー|
|ERR_SERVER_CENTER_CONN_ROOM_SIG_GROUPID|-102041|ルーム間マイク接続の署名が一致しません|
|ERR_SERVER_CENTER_CONN_ROOM_NOT_CONNED|-102042|このルームはマイク接続がありません|
|ERR_SERVER_CENTER_CONN_ROOM_USER_NOT_CONNED|-102043|このユーザーはマイク接続を開始していません|
|ERR_SERVER_CENTER_CONN_ROOM_FAILED|-102044|ルーム間マイク接続に失敗しました|
|ERR_SERVER_CENTER_CONN_ROOM_CANCEL_FAILED|-102045|ルーム間マイク接続の取り消しに失敗しました|
|ERR_SERVER_CENTER_CONN_ROOM_CONNED_ROOM_NOT_EXIST|-102046|マイク接続されたルームが存在しません|
|ERR_SERVER_CENTER_CONN_ROOM_CONNED_REACH_MAX_ROOM|-102047|マイク接続されたルームがマイク接続の上限に達しました|
|ERR_SERVER_CENTER_CONN_ROOM_CONNED_USER_NOT_EXIST|-102048|マイク接続されたユーザーが存在しません|
|ERR_SERVER_CENTER_CONN_ROOM_CONNED_USER_DELETED|-102049|マイク接続されたユーザーが削除されました|
|ERR_SERVER_CENTER_CONN_ROOM_CONNED_USER_FULL|-102050|マイク接続されたユーザーがリソースの上限に達しました|
|ERR_SERVER_CENTER_CONN_ROOM_INVALID_SEQ|-102051|マイク接続リクエストの番号が乱れています|


## アラートコード表

アラートコードを特に注意する必要はありません。必要に応じて、現在のユーザーに対応するプロンプ​​トを表示するかどうかを選択できます。

| 記号 | 値 | 意味 |
|---|---|---|
|WARNING_HW_ENCODER_START_FAIL|1103|ハードウェアエンコーディングの起動に問題が発生した場合、自動的にソフトウェアエンコーディングに切り替わります|
|WARNING_VIDEO_ENCODER_SW_TO_HW|1107|現在のCPU使用率が高すぎてソフトウェアエンコーディング要件を満たせないため、自動的にハードウェアエンコーディングに切り替わります|
|WARNING_INSUFFICIENT_CAPTURE_FPS|1108|カメラのキャプチャフレームレートが不足しています。美顔アルゴリズムを備えた一部のAndroidスマートフォンには表示されます|
|WARNING_SW_ENCODER_START_FAIL|1109|ソフトウェアエンコーディングの開始に失敗しました|
|WARNING_REDUCE_CAPTURE_RESOLUTION|1110|現在のフレームレートとパフォーマンスの最適解を満たすため、カメラのキャプチャ解像度が低下します。|
|WARNING_CAMERA_DEVICE_EMPTY|1111|使用可能なカメラデバイスが検出されません|
|WARNING_CAMERA_NOT_AUTHORIZED|1112|ユーザーは、現在のアプリケーションにカメラ使用権限を承認していません|
|WARNING_MICROPHONE_DEVICE_EMPTY|1201|使用可能なマイクデバイスが検出されません|
|WARNING_SPEAKER_DEVICE_EMPTY|1202|使用可能なスピーカーデバイスが検出されません|
|WARNING_MICROPHONE_NOT_AUTHORIZED|1203|ユーザーは、現在のアプリケーションにマイク使用権限を承認していません|
|WARNING_MICROPHONE_DEVICE_ABNORMAL|1204|オーディオキャプチャデバイスが利用できません（使用中であるなど）|
|WARNING_SPEAKER_DEVICE_ABNORMAL|1205|オーディオ再生デバイスが利用できません（使用中であるなど）|
|WARNING_VIDEO_FRAME_DECODE_FAIL|2101|現在のビデオフレームのデコードに失敗しました|
|WARNING_AUDIO_FRAME_DECODE_FAIL|2102|現在のオーディオフレームのデコードに失敗しました|
|WARNING_VIDEO_PLAY_LAG|2105|現在、ビデオ再生時にラグが発生しています|
|WARNING_HW_DECODER_START_FAIL|2106|ハードウェアデコードの開始に失敗しました。ソフトウェアデコードを使用してください|
|WARNING_VIDEO_DECODER_HW_TO_SW|2108|現在のストリームの最初のIフレームのハードウェアデコードが失敗しました。SDKは自動的にソフトウェアデコードに切り替えます|
|WARNING_SW_DECODER_START_FAIL|2109|ソフトウェアデコーダの起動に失敗しました|
|WARNING_VIDEO_RENDER_FAIL|2110|ビデオレンダリングに失敗しました|
|WARNING_START_CAPTURE_IGNORED|4000|キャプチャ中のため、キャプチャの開始は無視されます|
|WARNING_AUDIO_RECORDING_WRITE_FAIL|7001|オーディオ記録のファイルへの書き込みに失敗しました|
|WARNING_ROOM_DISCONNECT|5101|ネットワーク接続が切断されました|
|WARNING_IGNORE_UPSTREAM_FOR_AUDIENCE|6001|現在、視聴者ロールです。アップストリームのオーディオビデオデータを無視します|
|WARNING_NET_BUSY|1101|ネットワーク状態の不良：アップストリーム帯域幅が小さすぎて、データのアップロード時に問題が生じます|
|WARNING_RTMP_SERVER_RECONNECT|1102|CSSプッシュのときにネットワークが切断しましたが、自動再接続が開始されました（自動再接続は連続3回を超えて失敗すると、それ以上は行われません）|
|WARNING_LIVE_STREAM_SERVER_RECONNECT|2103|ライブストリーミングのプルのときにネットワークが切断しましたが、自動再接続が開始されました（自動再接続は連続3回を超えて失敗すると、それ以上は行われません）|
|WARNING_RECV_DATA_LAG|2104|不安定なネットワークパケット：ダウンストリーム帯域幅が不足しているか、キャスター側からのストリーミングが不均一であることが原因と思われます|
|WARNING_RTMP_DNS_FAIL|3001|ライブストリーミング、DNS解決に失敗しました|
|WARNING_RTMP_SEVER_CONN_FAIL|3002|ライブストリーミング、サーバーの接続に失敗しました|
|WARNING_RTMP_SHAKE_FAIL|3003|ライブストリーミング、RTMPサーバーとのハンドシェイクに失敗しました|
|WARNING_RTMP_SERVER_BREAK_CONNECT|3004|ライブストリーミング、サーバーが自動的に切断しました|
|WARNING_RTMP_READ_WRITE_FAIL|3005|ライブストリーミング、RTMPの読み取り/書き込みに失敗し、接続が切断されます|
|WARNING_RTMP_WRITE_FAIL|3006|ライブストリーミング、RTMP書き込みエラー（SDK内部エラーコードは外部にスローされません）|
|WARNING_RTMP_READ_FAIL|3007|ライブストリーミング、RTMP読み取りエラー（SDK内部エラーコードは外部にスローされません）|
|WARNING_RTMP_NO_DATA|3008|ライブストリーミング、30秒以上データが送信されない場合、自動的に接続が切断されます|
|WARNING_PLAY_LIVE_STREAM_INFO_CONNECT_FAIL|3009|ライブストリーミング、connectサーバー呼び出しに失敗しました（SDK内部エラーコードは外部にスローされません）|
|WARNING_NO_STEAM_SOURCE_FAIL|3010|ライブストリーミング、接続に失敗しました。このストリームアドレスにビデオはありません。（SDK内部エラーコードは外部にスローされません）|
|WARNING_ROOM_RECONNECT|5102|ネットワークが切断され、自動再接続が開始されました|
|WARNING_ROOM_NET_BUSY|5103|ネットワーク状態の不良：アップストリーム帯域幅が小さすぎて、データのアップロード時に問題が生じます|
    
