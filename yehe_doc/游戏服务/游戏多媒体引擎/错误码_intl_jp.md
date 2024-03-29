開発者のデバッグ作業、及びGMEのAPI製品へのアクセスを容易にするために、ここで、Gaming Multimedia Engine開発に適用されるエラーコードドキュメンテーションを説明します。

## 一般的なエラー

| エラーコード名                    | エラーコード値 | 原因と解決策                                               |
| ----------------------------- | -------- | ------------------------------------------------------------ |
| AV_ERR_3DVOICE_ERR_NOT_INITED | 7003     | インターフェースInitSpatializerを呼び出してください                             |
| AV_ERR_NET_REQUEST_FALLED     | 7004     | ネットワーク要求に失敗しました。通常ネットワークの状態が不安定からです。[リアルタイムボイスルームの問題](https://intl.cloud.tencent.com/document/product/607/35611)を参照してトラブルシューティングしてください |
|AV_ERR_CHARGE_OVERDUE         | 7005     | アカウントの支払い延滞による失敗しました、Tencent Cloudのコンソールで支払い延滞があるかどうかを確認してください           |
| AV_ERR_AUTH_FIALD             | 7006     | 認証は失敗しました。下記の原因があります。1.appidは存在していないか、或いはエラーが発生しています。2.authbuff 認証エラーが発生しています。3.認証は期限切れになっています。 |
| AV_ERR_IN_OTHER_ROOM          | 7007     | 他のルームに入っています                                               |
| AV_ERR_NO_PERMISSION          | 7009     | アクションを実行しようとしているときに権限がありません                               |
| AV_ERR_FILE_CANNOT_ACCESS     | 7010     | ファイルにアクセスできません                                                 |
| AV_ERR_FILE_DAMAGED           | 7011     | ファイルが破損しています                                                   |
| AV_ERR_SERVICE_NOT_OPENED     | 7012     | この機能はコンソールで有効になっていません。コンソールで有効にしてください                     |
| AV_ERR_USER_CANCELED          | 7013     | ユーザーはこの操作を自らキャンセルしました。例えば、ルームに入らずに退室操作を実行しました             |
|AV_ERR_LOAD_LIB_FAILED       |7014|ライブラリファイルが正しくロードされていません。ライブラリファイルがあるか確認してください|k
|AV_ERR_SDK_NOT_FULL_UPDATE       |7015|SDKをアップグレードするとき、すべてのファイルがアップグレードされていないため、一致しないモジュールがあります。SDKを完全にアップグレードしてください|
|AV_ERR_3DVOICE_ERR_FILE_DAMAGED       |7002|3Dサウンドエフェクトファイルは成功にロードされていません|

## リアルタイム音声のクライアントエラー

<table>
<thead>
<tr>
<th>エラーコード名</th>
<th>エラーコードの値</th>
<th>意味</th>
<th>原因</th>
<th>解決策&nbsp;&nbsp;&nbsp;&nbsp;</th>
</tr>
</thead>
<tbody><tr>
<td>AV_ERR_REPEATED<br>_OPERATION</td>
<td>1001</td>
<td>繰り返した操作</td>
<td>このエラーは、ある操作を実行しているが再び同じ操作を実行する場合に発生します。操作のタイプは、AVContextクラス、ルームクラス、デバイスクラス、メンバクラスなどがあります。AVContextタイプの操作：StartContext/StopContext。ルームタイプの操作：EnterRoom/ExitRoom。デバイスタイプの操作：デバイスをオン/オフします。</td>
<td>次の操作に進むには、前の操作が完了するまで待つ必要があります。</td>
</tr>
<tr>
<td>AV_ERR_EXCLUSIVE<br>_OPERATION</td>
<td>1002</td>
<td>相互排他操作</td>
<td>このエラーは、ある操作を実行しているが再び同じタイプの操作を実行する場合に発生します。</td>
<td>次の操作に進むには、前の操作が完了するまで待つ必要があります。</td>
</tr>
<tr>
<td>AV_ERR_HAS_IN<br>_THE_STATE</td>
<td>1003</td>
<td>繰り返した操作</td>
<td>このエラーは、オブジェクトがある状態にあるがその状態にする操作を行った場合に発生します。例えば、すでにルームに入っているが、部屋に参加する操作をした場合にエラーが発生します。</td>
<td>すでに所望の状態にあるので、その操作は成功したと考え、成功したものとして扱うことができます。</td>
</tr>
<tr>
<td>AV_ERR_INVALID<br>_ARGUMENT</td>
<td>1004</td>
<td>エラーパラメータ</td>
<td>このエラーは、SDKインターフェースの呼び出しに間違ったパラメータが渡された場合に発生します。このエラーは、ルームに参加するときに、渡されたルームのタイプは、AVRoom::ROOM_TYPE_PAIRまたはAVRoom::ROOM_TYPE_MULTIでなければ、発生します。</td>
<td>APIドキュメントを詳細に読み、各インターフェースの各パラメータの有効な数値範囲を取得し、入力パラメータの正確性を確保し、必要な予防処理を行ってください。</td>
</tr>
<tr>
<td>AV_ERR_TIMEOUT</td>
<td>1005</td>
<td>操作タイムアウト</td>
<td>特定の操作を行い、規定の時間内に操作結果が返されない場合、このエラーが発生します。ほとんどの状況において、シグナリング伝送に関連し、かつネットワークに問題がある状況でこのエラーが発生しやすいです。ルーム参加操作を実行した時に、30s後にルーム参加操作完了の結果が返されない場合、このエラーが発生します。</td>
<td>ネットワークに問題があるか、パブリックネットワークに接続できるかを確認した上、リトライします。</td>
</tr>
<tr>
<td>AV_ERR_NOT<br>_IMPLEMENTED</td>
<td>1006</td>
<td>未実装</td>
<td>このエラーは、機能がサポートされていないSDKインターフェースを呼び出すときに発生します。</td>
<td>この機能はサポートされていませんので、別の解決策を検討してください。</td>
</tr>
<tr>
<td>AV_ERR_NOT_IN<br>_MAIN_THREAD</td>
<td>1007</td>
<td>メインスレッドにありません</td>
<td>SDKの外部向けインターフェースはメインスレッドで実行する必要があります。このエラーは、業務側がSDKインターフェースを呼び出すときメインスレッドで呼び出さない場合に発生します。</td>
<td>SDKインターフェースがメインスレッドで呼び出されるように業務側のロジックを変更してください。</td>
</tr>
<tr>
<td>AV_ERR_RESOURCE<br>_IS_OCCUPIED</td>
<td>1008</td>
<td>リソースが使用されています</td>
<td>このエラーは、すでに使用されているカメラやスクリーンなどのリソースを使用する場合に発生します。</td>
<td>リソースの使用が競合しないよう、SDK関連機能を適切なタイミングで使用するには、具体的にどのリソースが使用されているのか、そのリソースがなぜ使用されているのかを確認してください。</td>
</tr>
<tr>
<td>AV_ERR_CONTEXT<br>_NOT_EXIST</td>
<td>1101</td>
<td>AVContextステータスの問題</td>
<td>このエラーは、AVContextオブジェクトがCONTEXT_STATE_STARTEDステータスではなく、このステータスが必要であるインターフェースを呼び出す場合に発生します。</td>
<td>業務側のロジックを変更して、SDKインターフェースを呼び出すタイミングの正確性を確保してください。</td>
</tr>
<tr>
<td>AV_ERR_CONTEXT<br>_NOT_STOPPED</td>
<td>1102</td>
<td>AVContextステータスの問題</td>
<td>このエラーは、AVContextオブジェクトがCONTEXT_STATE_STOPPEDステータスではなく、このステータスが必要であるインターフェースを呼び出す場合に発生します。そのステータスでないまま、AVContext::DestroyContextを呼び出す場合にこのエラーが発生します。</td>
<td>業務側のロジックを変更して、SDKインターフェースを呼び出すのタイミングの正確性を確保してください。</td>
</tr>
<tr>
<td>AV_ERR_ROOM<br>_NOT_EXIST</td>
<td>1201</td>
<td>AVRoomステータスの問題</td>
<td>このエラーは、AVRoomオブジェクトがROOM_STATE_ENTEREDステータスではなく、このステータスが必要であるインターフェースを呼び出す場合に発生します。</td>
<td>業務側のロジックを変更して、SDKインターフェースを呼び出すのタイミングの正確性を確保してください。</td>
</tr>
<tr>
<td>AV_ERR_ROOM<br>_NOT_EXITED</td>
<td>1202</td>
<td>AVRoomステータスの問題</td>
<td>このエラーは、AVRoomオブジェクトがROOM_STATE_EXITEDステータスではなく、このステータスが必要であるインターフェースを呼び出す場合に発生します。そのステータスでないまま、AVContext::StopContextを呼び出す場合にこのエラーが発生します。</td>
<td>業務側のロジックを変更して、SDKインターフェースを呼び出すのタイミングの正確性を確保してください。</td>
</tr>
<tr>
<td>AV_ERR_DEVICE<br>_NOT_EXIST</td>
<td>1301</td>
<td>デバイスが存在しません</td>
<td>このエラーは、デバイスが存在しないか、デバイスの初期化が完了していないままデバイスを使用する場合に発生します。</td>
<td>デバイスが本当に存在すること、デバイスIDが正しく入力されていること、デバイスが正常に初期化された後にデバイスを使用することを確認してください。</td>
</tr>
<tr>
<td>AV_ERR_ENDPOINT<br>_NOT_EXIST</td>
<td>1401</td>
<td>AVEndpointオブジェクトが存在しません</td>
<td>このエラーは、メンバーが音声ファイルまたはビデオファイルを送信していないがAVEndpointオブジェクトを取得する場合に発生することがあります。</td>
<td>業務側のロジックを変更して、SDKインターフェースを呼び出すのタイミングの正確性を確保してください。</td>
</tr>
<tr>
<td>AV_ERR_ENDPOINT<br>_HAS_NOT_VIDEO</td>
<td>1402</td>
<td>メンバーがビデオを送信していません</td>
<td>このエラーは、メンバーがビデオを送信していないが、メンバーのビデオ送信が必要である操作を行った場合に発生することがあります。メンバがビデオを送信していないが、そのメンバの画面をリクエストする場合にこのエラーが発生します。</td>
<td>業務側のロジックを変更して、SDKインターフェースを呼び出すのタイミングの正確性を確保してください。</td>
</tr>
<tr>
<td>AV_ERR_TINYID_TO<br>_OPENID_FAILED</td>
<td>1501</td>
<td>tinyidからidentifierへの変換に失敗しました</td>
<td>メンバ情報更新のシグナリングを受信したときにtinyidをidentifierに変換する必要がありますが、IMSDKライブラリに関連するロジックやネットワークに問題がある場合などにこのエラーが発生します。</td>
<td>ネットワークに問題がないか、ログを使用してIMSDKに関連するロジックに問題がないかを確認してください。</td>
</tr>
<tr>
<td>AV_ERR_OPENID_TO<br>_TINYID_FAILED</td>
<td>1502</td>
<td>identifierからtinyidへの変換に失敗しました</td>
<td>StartContextインターフェースを呼び出すときにidentifierをtinyidに変換する必要がありますが、IMSDKライブラリに関連するロジックやネットワークに問題があり、ログイン状態にない場合などにこのエラーが発生します。</td>
<td>ネットワークに問題がないか、ログを使用してIMSDKに関連するロジックに問題がないか、IMSDKのログインインターフェースが正常に呼び出されたか確認してください。</td>
</tr>
<tr>
<td>AV_ERR_DEVICE<br>_TEST_NOT_EXIST</td>
<td>1601</td>
<td>AVDeviceTestステータスの問題</td>
<td>このエラーは、AVDeviceTestオブジェクトがDEVICE_TEST_STATE_STARTEDステータスではなく、このステータスが必要であるインターフェースを呼び出す場合に発生します。</td>
<td>業務側のロジックを変更して、SDKインターフェースを呼び出すのタイミングの正確性を確保してください。</td>
</tr>
<tr>
<td>AV_ERR_DEVICE<br>_TEST_NOT_STOPPED</td>
<td>1602</td>
<td>AVDeviceTestステータスの問題</td>
<td>このエラーは、AVDeviceTestオブジェクトがDEVICE_TEST_STATE_STOPPEDステータスではなく、このステータスが必要であるインターフェースを呼び出す場合に発生します。そのステータスでないまま、AVContext::StopContextを呼び出す場合にこのエラーが発生します。</td>
<td>業務側のロジックを変更して、SDKインターフェースを呼び出すのタイミングの正確性を確保してください。</td>
</tr>
<tr>
<td>AV_ERR_INVITET<br>_FAILED</td>
<td>1801</td>
<td>招待の送信に失敗しました。</td>
<td>招待を送信するときに発生した失敗です。</td>
<td>招待モジュールはDEMOに使用されているだけで、招待機能の呼び出しはサポートされていません。業務側でこれらのエラーコードを処理する必要はありません。</td>
</tr>
<tr>
<td>AV_ERR_ACCEPTT<br>_FAILED</td>
<td>1802</td>
<td>招待の受け入れに失敗しました</td>
<td>招待を受け入れるときに発生した失敗です。</td>
<td>招待モジュールはDEMOに使用されているだけで、招待機能の呼び出しはサポートされていません。業務側でこれらのエラーコードを処理する必要はありません。</td>
</tr>
<tr>
<td>AV_ERR_REFUSE<br>_FAILED</td>
<td>1803</td>
<td>招待の拒否に失敗しました</td>
<td>招待を拒否するときに発生した失敗です。</td>
<td>招待モジュールはDEMOに使用されているだけで、招待機能の呼び出しはサポートされていません。業務側でこれらのエラーコードを処理する必要はありません。</td>
</tr>
<tr>
<td>QAV_ERR_NOT_TRY<br>_NEW_ROOM</td>
<td>2001</td>
<td>新しいルームに入ろうとはしない場合、元のルームにとどまることになります。</td>
<td>新しいルームへの切り替えに失敗しましたが、元のルームにいます。</td>
<td>現在のルームで正常に使用できます。</td>
</tr>
<tr>
<td>QAV_ERR_TRY_NEW<br>_ROOM_FAILED</td>
<td>2002</td>
<td>新しいルームに入ろうとしたが失敗し、元のルームが閉鎖されます。</td>
<td>新しいルームへの切り替えに失敗し、元の部屋からも退出しました。</td>
<td>ルームから退出してもう一度参加します。</td>
</tr>
</tbody></table>

## リアルタイム音声サーバー側のエラー

<table>
<thead>
<tr>
<th width="30%">エラーコード名</th>
<th width="11%">エラーコードの値</th>
<th width="15%">意味</th>
<th width="22%">原因</th>
<th width="22%">解決策</th>
</tr>
</thead>
<tbody><tr>
<td>AV_ERR_SERVER_FAILED</td>
<td>10001</td>
<td>一般的なエラー</td>
<td>具体的な原因は、ログを分析してバックグラウンドからクライアントへ返された実際のエラーコードを確認すればわかります。</td>
<td>AppID、UIN、AuthBuffer（ドキュメントを参照）など、ルーム参加APIのパラメータを表示して、その適切性を確認してください。コンソール上の関連パラメータがローカルのものと一致しているかどうかを確認してください。コンソールが料金滞納になっていないか確認してください。開発者テスト用デバイスのネットワーク環境が、開発者プライベートネットワーク環境にあるかパブリックネットワーク環境にあるかを確認してください。</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_INVALID_ARGUMENT</td>
<td>10002</td>
<td>エラーパラメータ</td>
<td>SDKインターフェースが呼び出されたとき、またはSDKが内部でバックグラウンドにシグナリングを送信したときに、誤ったパラメータが渡されました。</td>
<td>SDKインターフェースが呼び出されるときに渡されるパラメータが正しいことを確認してください。ログを分析し、バックグラウンドからクライアントに返された本当のエラーコードを取得し、解決してもらうようにバックグラウンドのスタッフに連絡します。</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_NO_PERMISSION</td>
<td>10003</td>
<td>権限がありません</td>
<td>機能を使用する権限がありません。このエラーは、ルームに入ったときに間違った署名を持っていたり、有効期限が切れていたりした場合に発生します。</td>
<td>適切な機能を使用する前に適切な権限パラメータを設定したことを確認してください。AppIDと権限キーが正しいことを確認してください。</td>
</tr>
<tr>
<td>AV_ERR_SERVER_TIMEOUT</td>
<td>10004</td>
<td>タイムアウト</td>
<td>このエラーは、ある操作が行われ、所定の時間内に操作結果が返されない場合に発生します。</td>
<td>ログを分析し、バックグラウンドからクライアントに返された本当のエラーコードを取得し、解決してもらうようにバックグラウンドのスタッフに連絡します。</td>
</tr>
<tr>
<td>AV_ERR_SERVER_ALLOC<br>_RESOURCE_FAILED</td>
<td>10005</td>
<td>ネットワークエラー</td>
<td>ある操作の実行中にネットワークエラーが発生しました</td>
<td>AppID、UIN、AuthBuffer（ドキュメントを参照）など、ルーム参加APIのパラメータを表示して、その適切性を確認します。適切な場合は、開発者テスト用デバイスのネットワーク環境が、開発者プライベートネットワーク環境にあるかパブリックネットワーク環境にあるかを確認してください。開発者プライベートネットワーク環境にある場合は、開発者にURL：openmsf.3g.qq.com:15000にアクセスできるかどうかの確認を依頼してください。上記のURLに正常にアクセス可能な場合は、URL：cloud.tim.qq.com:15000にアクセスできるかどうかの確認を依頼してください。</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_ID_NOT_IN_ROOM</td>
<td>10006</td>
<td>ルームにいません</td>
<td>このエラーは、部屋にいないときに何らかの操作を行った場合に発生します。</td>
<td>SDK関連機能が適切なタイミングで使用されるようにしてください。</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_NOT_IMPLEMENT</td>
<td>10007</td>
<td>未実装</td>
<td>このエラーは、機能がサポートされていないSDKインターフェースを呼び出すときに発生します。</td>
<td>この機能はサポートされていませんので、別の解決策を検討してください。</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_REPEATED_OPERATION</td>
<td>10008</td>
<td>繰り返した操作</td>
<td>このエラーは、ある操作を実行しているが再び同じタイプの操作を実行する場合に発生します。</td>
<td>次の操作に進むには、前の操作が完了するまで待つ必要があります。</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_ROOM_NOT_EXIST</td>
<td>10009</td>
<td>部屋は存在しません</td>
<td>このエラーは、部屋が存在しないときに何らかの操作を実行すると発生します。</td>
<td>SDK関連機能が適切なタイミングで使用されるようにしてください。</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_ENDPOINT_NOT_EXIST</td>
<td>10010</td>
<td>メンバーが存在しません</td>
<td>このエラーは、メンバーが存在しないときにそのメンバーに関連する操作を実行すると発生します。</td>
<td>ログを分析し、バックグラウンドからクライアントに返された本当のエラーコードを取得し、解決してもらうようにバックグラウンドのスタッフに連絡します。</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_INVALID_ABILITY</td>
<td>10011</td>
<td>エラー能力</td>
<td>具体的な原因は、ログを分析してバックグラウンドからクライアントへ返された実際のエラーコードを確認すればわかります。</td>
<td>ログを分析し、バックグラウンドからクライアントに返された本当のエラーコードを取得し、解決してもらうようにバックグラウンドのスタッフに連絡します。</td>
</tr>
</tbody></table>

## 音声から文字への変換エラー

| エラーコード名                                         | エラーコード値 | 意味               | 原因                                                       | 解決策                                                     |
| -------------------------------------------------- | -------- | ------------------ | ---------------------------------------------------------- | ------------------------------------------------------------ |
| QAVPTTERROR_RECORDER<br>\_PARAM_NULL                    | 4097     | 録音エラー           | パラメータは空です                                                   | コード内のインターフェースパラメータが正しいかをチェックしてください。                                 |
| QAVPTTERROR_RECORDER<br>\_INIT_ERROR                    | 4098     | 録音エラー           | 初期化エラー                                                 | デバイスが使用されているか、権限が正常であるか、初期化が正常であるかをチェックします。       |
| QAVPTTERROR_RECORDER<br>\_RECORDING_ERR                 | 4099     | 録音エラー           | レコーディング中です                                                 | 適切なタイミングでSDK録音機能を使用するようにしてください。                          |
| QAVPTTERROR_RECORDER<br>\_NODATA_ERR                    | 4100     | 録音エラー           | オーディオデータが収集されていません                                         | マイクデバイスに異常がないかを確認してください。                                     |
| QAVPTTERROR_RECORDER<br>\_OPENFILE_ERR                  | 4101     | 録音エラー           | 録音時に録音ファイルへのアクセスエラーが発生しました|                                   | ファイルが存在し、ファイルパスが有効であることを確保してください。                             |
| QAVPTTERROR_RECORDER<br>\_PERMISSION_MIC_ERR            | 4102     | 録音エラー           | マイク未認証エラー                                           | SDKを使用するにはマイクの権限が必要です。権限を追加するには、対応するエンジンまたはプラットフォームのSDKプロジェクト構成ドキュメントをご参照ください。|
| QAVPTTERROR_RECORDER<br>\_AUDIO_TOO_SHORT               | 4103     | 録音エラー           | 録音時間が短すぎます                                           | 正常に録音するには、録音時間の単位はミリ秒で、録音時間が1000秒以上である必要があります。|
| QAVPTTERROR_RECORDER<br>\_RECORD_NOT_START              | 4104     | 録音エラー           | 録音が開始されませんでした                                           | 録音開始インターフェースが呼び出されたかどうかを確認してください。                               |
| QAVPTTERROR_UPLOAD<br>\_FILE_ACCESSERROR                | 8193     | アップロードエラー           | ファイルをアップロードする時にファイルアクセスにエラーが発生しました                                   | ファイルが存在し、ファイルパスが有効であることを確保してください。                             |
| QAVPTTERROR_UPLOAD<br>\_SIGN_CHECK_FAIL                 | 8194     | アップロードエラー           | 署名検証失敗のエラーです                                           | 認証キーが正しいか、オフラインボイスが初期化されたかを確認してください。             |
| QAVPTTERROR_UPLOAD<br>\_COS_INTERNAL_FAIL               | 8195     | アップロードエラー           | ネットワークエラー                                                   | デバイスネットワークがパブリックネットワーク環境に正常にアクセスできるかを確認してください。[ネットワークをチェックする方法](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F)をご参照ください。|
| QAVPTTERROR_UPLOAD<br>\_GET_TOKEN_NETWORK_FAIL          | 8196     | アップロードエラー           | アップロードパラメータの取得中にネットワークが失敗しました                                 | 認証が正しいか、デバイスネットワークがパブリックネットワーク環境に正常にアクセスできるかを確認してください。[ネットワークをチェックする方法](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F)をご参照ください。|
| QAVPTTERROR_UPLOAD<br>\_SYSTEM_INNER_ERROR              | 8197     | アップロードエラー           | アップロードパラメータを取得するプロセスで、戻りパケットのデータが空です                             | 認証が正しいか、デバイスネットワークがパブリックネットワーク環境に正常にアクセスできるかを確認してください。[ネットワークをチェックする方法](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F)をご参照ください。|
| QAVPTTERROR_UPLOAD<br>\_RSP_DATA_DECODE_FAIL            | 8198     | アップロードエラー           | アップロードパラメータを取得するプロセスで、戻りパケットのアンパックができませんでした                            | 認証が正しいか、デバイスネットワークがパブリックネットワーク環境に正常にアクセスできるかを確認してください。[ネットワークをチェックする方法](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F)をご参照ください。|
| QAVPTTERROR_UPLOAD<br>\_APPINFO_UNSET                   | 8200     | アップロードエラー           | appinfoが設定されていません                                           | applyインターフェースが呼び出されたか、引き渡されたパラメータが空であるかどうかをチェックしてください。                |
| QAVPTTERROR_DOWNLOAD<br>\_FILE_ACCESSERROR              | 12289    | ダウンロードエラー           | ファイルをダウンロードする時にファイルアクセスエラーが発生しました                                   | ファイルパスが有効であるかをチェックしてください。                                       |
| QAVPTTERROR_DOWNLOAD<br>\_SIGN_CHECK_FAIL               | 12290    | ダウンロードエラー           | 署名検証失敗                                               | 認証キーが正しいか、オフラインボイスが初期化されたかをチェックしてください。             |
| QAVPTTERROR_DOWNLOAD<br>\_COS_INTERNAL_FAIL             | 12291    | ダウンロードエラー           | ネットワークエラー                                                   | サーバーが音声ファイルを取得できませんでした。インターフェースパラメータfileidが正しいかどうか、ネットワークが正常かどうかをチェックしてください。|
| QAVPTTERROR_DOWNLOAD<br>\_REMOTEFILE_ACCESSERROR        | 12292    | ダウンロードエラー           | サーバーファイルシステムエラー                                         | デバイスのネットワークがパブリックネットワーク環境に正常にアクセスできるか、このファイルがサーバー上にあるかどうかをチェックしてください。|
| QAVPTTERROR_DOWNLOAD<br>\_GET_SIGN_NETWORK_FAIL         | 12293    | ダウンロードエラー           | ダウンロードパラメータを取得するプロセスでHTTPネットワークが失敗しました                          | デバイスのネットワークがパブリックネットワーク環境に正常にアクセスできるかを確認してください。[ネットワークの確認方法](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F)をご参照ください。|
| QAVPTTERROR_DOWNLOAD<br>\_SYSTEM_INNER_ERROR            | 12294    | ダウンロードエラー           | ダウンロードパラメータを取得するプロセスで戻りパケットのデータが空です                           | デバイスのネットワークがパブリックネットワーク環境に正常にアクセスできるかを確認してください。[ネットワークの確認方法](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F)をご参照ください。|
| QAVPTTERROR_DOWNLOAD_GET<br>\_SIGN_RSP_DATA_DECODE_FAIL | 12295    | ダウンロードエラー           | ダウンロードパラメータを取得するプロセスで戻りパケットのアンパックができませんでした                           | デバイスのネットワークがパブリックネットワーク環境に正常にアクセスできるかを確認してください。[ネットワークの確認方法](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F)をご参照ください。|
| QAVPTTERROR_DOWNLOAD<br>\_APPINFO_UNSET                 | 12297    | ダウンロードエラー           | appinfoが設定されていません                                           | 認証キーが正しいか、オフラインボイスが初期化されたかをチェックしてください。             |
| QAVPTTERROR_PLAYER_INIT_ERR                        | 20481    | 再生エラー           | 初期化エラー                                                 | デバイスが使用されているか、権限が正常であるか、初期化が正常であるかをチェックしてください。       |
| QAVPTTERROR_PLAYER<br>\_PLAYING_ERR                     | 20482    | 再生エラー           | 再生中に中断して次のファイルを再生しようとしましたが失敗しました（通常は中断可能）| コードのロジックが正しいか確認してださい。                                       |
| QAVPTTERROR_PLAYER<br>\_PARAM_NULL                      | 20483    | 再生エラー           | パラメータが空です                                                   | コード内のインターフェースパラメータが正しいかをチェックしてください。                                 |
| QAVPTTERROR_PLAYER<br>\_OPENFILE_ERR                    | 20484    | 再生エラー           | 再生中にファイルアクセスエラーが発生しました                                       | ファイルが存在し、ファイルパスが有効であることを確保してください。                             |
| QAVPTTERROR_PLAYER<br>\_PLAYER_NOT_START_ERR            | 20485    | 再生エラー           | 再生が開始されていません                                                 | ファイルが存在し、ファイルパスが有効であることを確保してください。                             |
| QAVPTTERROR_S2T<br>\_INTERNAL_ERROR                     | 32769    | 音声から文字への変換エラー     | 内部エラー                                                   | このような状況が発生した場合は、Tencent Cloudの担当者に連絡し、[ダウンロードと使用に関する質問](https://intl.cloud.tencent.com/document/product/607/30256)を参照してログファイルを提供してください。|
| QAVPTTERROR_S2T<br>\_NETWORK_FAIL                       | 32770    | 音声から文字への変換エラー     | ネットワーク失敗                                                   | デバイスネットワークがパブリックネットワーク環境に正常にアクセスできるかを確認してください。[ネットワークの確認方法](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F)をご参照ください。|
| QAVPTTERROR_S2T<br>\_RSP_DATA_DECODE_FAIL               | 32772    | 音声から文字への変換エラー     | 戻りパケットのアンパックができませんでした                                               | このような状況が発生した場合は、Tencent Cloudの担当者に連絡し、[ダウンロードと使用に関する質問](https://intl.cloud.tencent.com/document/product/607/30256)を参照してログファイルを提供してください。|
| QAVPTTERROR_S2T<br>\_APPINFO_UNSET                      | 32774    | 音声から文字への変換エラー     | appinfoが設定されていません                                           | 認証キーが正しいか、オフラインボイスが初期化されたかをチェックしてください。             |
| QAVPTTERROR_STREAMIN<br>\_RECORD_SUC_REC_FAIL           | 32775    | ストリーミングボイスツーテキスト変換エラー | ストリーミングボイスのテキスト変換ができませんでしたが、録音が成功しました                         | ネットワークが正しく接続されているか、権限キーが正しいかを確認してください。                 |
| QAVPTTERROR_S2T<br>\_SIGN_CHECK_FAIL                    | 32776    | authbuffer検証失敗 | authbuffer検証に失敗しました                                        | authbufferが正しいか確認してください。                                   |
| QAVPTTERROR_STREAMIN<br>\_UPLOADANDRECORD_SUC_REC_FAIL  | 32777    | ストリーミングボイスツーテキスト変換エラー | ストリーミングボイスのテキスト変換ができませんでしたが、録音とアップロードが成功しました。         | コードにエラーがないか確認してください。                                         |
| QAVPTTERROR_S2T_PARAM_NULL                         | 32784    | ボイスツーテキスト変換エラー     | ボイスツーテキスト変換パラメータにエラーが発生しました                                         | コード内のインターフェースパラメータfileidが空でるかどうかをチェックしてください。                         |
| QAVPTTERROR_S2T<br>\_AUTO_SPEECH_REC_ERROR              | 32785    | ボイスツーテキスト変換エラー     | 音声からテキストへの翻訳にエラーが返されました                                     | このような状況が発生した場合は、Tencent Cloudの担当者に連絡し、[ダウンロードと使用に関する質問](https://intl.cloud.tencent.com/document/product/607/30256)を参照してログファイルを提供してください。|
| QAVPTTERROR_ERR<br>\_VOICE_STREAMIN_RUNING_ERROR        | 32786    | ストリーミングボイスツーテキスト変換エラー | ストリーミングボイスツーテキスト変換に失敗しました                                         | ストリーミングレコーディングステータスでは、ストリーミングレコーディングインターフェースの実行結果が返されるまで待ってください。         |
| QAVPTTERROR_ERR_VOICE<br>\_STREAMING_ASR_ERROR          | 50012    | ストリーミングボイスツーテキスト変換エラー | ASRリクエストのエラーです                                                | レコーディングファイル（UploadRecordedFile）を再アップロードし、テキスト変換インターフェース（SpeechToText）を呼び出してください。このような状況が発生した場合は、Tencent Cloudの担当者に連絡し、[ダウンロードと使用に関する質問](https://intl.cloud.tencent.com/document/product/607/30256)を参照してログファイルを提供してください。|
