GME開発者がTencent Cloud GME製品APIのデバッグと導入を容易にするために、このドキュメントではGMEカスタマイズオーディオ転送ルーティング機能に適している使用参考ドキュメントを紹介します。


## シナリオ

**場面説明：2人の友達がチームを組んだ後、3人の知らない人をマッチングして大きなチームを組み、チーム全員の声を聞いて、チームの友達と話すような機能が必要です。**

カスタムオーディオルーティング機能でそれを実装することができます。ここでは5人全員が同じ音声ルームに入り、音声ルーティングのインターフェース設定を行い、2人チームの音声のみまたは全ルームの音声が聞こえるように設定したり、2人チームの者のみに話が聞こえるように設定したり、全ルームの者に話が聞こえるように設定したりすることができます。

オーディオルール距離：SetServerAudioRouteSendOperateType(AUDIO_ROUTE_SEND_WHITE_LIST,"2人チームのlist",ITMG_SERVER_AUDIO_ROUTE_RECV_TYPE,"2人チームのlist");
これにより、音声はlistに含まれる人にのみ送信されるととも、3人チームの音声のみが受信されます。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/KH6i143_819dd334b2ba7af9f2813f2d6f28aea2.png)


##  前提条件

- **リアルタイムボイスサービスを有効にしました：[サービス有効化ガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
- **GME SDK導入済み**：コアインターフェースとリアルタイム音声インターフェースの導入が含まれます。詳細については、[Native SDKのクイック導入](https://intl.cloud.tencent.com/document/product/607/40858)、[Unity SDKクイック導入](https://intl.cloud.tencent.com/document/product/607/44544)、[Unreal SDKクイック導入](https://intl.cloud.tencent.com/document/product/607/44545)をご参照ください。
-　GMEリアルタイムボイス機能を使用して音声ルームへの参加に成功し、マイク（EnableMic）、スピーカー（EnableSpeaker）をオンにしました。


##　音声転送ルーティング機能の導入


###　オーディオ転送ルールの設定

このインターフェースを呼び出して音声転送ルールを設定します。このインターフェースは、入室のコールバックに成功したときに呼び出され、呼び出し後にこの入室が有効になり、退室後に無効になります。


<dx-alert infotype="notice" title="注意">
発言禁止機能AddBlackListはネイティブに有効で、カスタムオーディオルーティングよりも優先されます。例えば、AはSetServerAudioRouteSendOperateTypeでBの発話のみを聞くように設定したが、AddBlackListを呼び出してBの発言を禁止した場合、AはBの声を聞くことができなくなります。
</dx-alert>




#### インターフェースのプロトタイプ

<dx-codeblock>
::: Unity c#
public abstract class ITMGRoom{
	public abstract int SetServerAudioRouteSendOperateType(ITMG_SERVER_AUDIO_ROUTE_SEND_TYPE Sendtype, string[] OpenIDforSend, ITMG_SERVER_AUDIO_ROUTE_RECV_TYPE Recvtype, string[] OpenIDforRecv);
}
:::
::: C++ c++
virtual int SetServerAudioRoute(ITMG_SERVER_AUDIO_ROUTE_SEND_TYPE SendType, const char OpenIDforSend[][21], int OpenIDforSendSize, ITMG_SERVER_AUDIO_ROUTE_RECV_TYPE RecvType,const char OpenIDforRecv[][21], int OpenIDforRecvSize) = 0;
:::
::: Android java
public abstract int SetServerAudioRoute(ITMGContext.ITMG_SERVER_AUDIO_ROUTE_SEND_TYPE sendType, ArrayList<String> SendList, ITMGContext.ITMG_SERVER_AUDIO_ROUTE_RECV_TYPE recvType, ArrayList<String> RecvList);
:::
::: iOS objectc
-(int)SetServerAudioRouteSendOperateType:(ITMG_SERVER_AUDIO_ROUTE_SEND_TYPE) Sendtype  SendList:(NSArray *)OpenIDForSend  RecvOperateType:(ITMG_SERVER_AUDIO_ROUTE_RECV_TYPE) Recvtype RecvList:(NSArray *)OpenIDForRecv;
:::
</dx-codeblock>


#### タイプの説明

**ITMG_SERVER_AUDIO_ROUTE_SEND_TYPE**

音声送信ルールを設定し、異なるルールを入力すると、異なる送信ルールが設定されます。

| 受信タイプ                       | 効果                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| AUDIO_ROUTE_NOT_SEND_TO_ANYONE | ローカルオーディオは上りリンクによりバックグラウンドに送信されますが、バックグラウンドは誰にも転送されません。これは自分自身をミュートすることに相当します。この場合、パラメータOpenIDForSendが無効で、nullを入力すればよい |
| AUDIO_ROUTE_SEND_TO_ALL        | ローカルオーディオは上りリンクによりすべての人に送信されます。この場合、パラメータOpenIDForSendは無効で、nullを入力すればよい |
| AUDIO_ROUTE_SEND_BLACK_LIST    | ローカルオーディオは上りリンクによりブラックリストの人に転送されません。ブラックリストはパラメータOpenIDForSendから提供されます |
| AUDIO_ROUTE_SEND_WHITE_LIST    | ローカルオーディオは上りリンクによりホワイトリストの人に転送されます。ホワイトリストはパラメータOpenIDForSendから提供されます |
>?
-　タイプにAUDIO_ROUTE_NOT_SEND_TO_ANYONEおよびAUDIO_ROUTE_SEND_TO_ALLが渡された場合、パラメータOpenIDForSendは有効でなく、nullを入力すればよい。
-　タイプにAUDIO_ROUTE_SEND_BLACK_LISTが渡された場合、パラメータOpenIDForSendはブラックリストで、最大10個までサポートされます。
-　タイプにAUDIO_ROUTE_SEND_WHITE_LISTが渡された場合、パラメータOpenIDForSendはホワイトリストで、最大10個までサポートされます。
>

**ITMG_SERVER_AUDIO_ROUTE_RECV_TYPE**

音声受信ルールを設定します。異なるルールが入力されると、異なる受信ルールが設定されます。

| 受信タイプ                       | 効果                                                         |
| -------------------------------- | ------------------------------------------------------------ |
| AUDIO_ROUTE_NOT_RECV_FROM_ANYONE | ローカルではオーディオを受け付けません。これはルームスピーカーエフェクトをオフにすることと同じです。この場合、パラメータOpenIDForSendは無効です。nullを入力すればよい |
| AUDIO_ROUTE_RECV_FROM_ALL        | ローカルではすべての人のオーディオを受信します。この場合、パラメータOpenIDForSendが無効です。nullを入力すればよい |
| AUDIO_ROUTE_RECV_BLACK_LIST      | ローカルではブラックリストの人からの音声を受信しません。ブラックリストはパラメータOpenIDForSendによって提供されます |
| AUDIO_ROUTE_RECV_WHITE_LIST      | ローカルではホワイトリストの人の音声のみを受信します。ホワイトリストはパラメータOpenIDForSendによって提供されます |

>?
-　タイプにAUDIO_ROUTE_NOT_RECV_FROM_ANYONEとAUDIO_ROUTE_RECV_FROM_ALLが渡された場合、OpenIDForSendが有効ではありません。
-　タイプにAUDIO_ROUTE_RECV_BLACK_LISTが渡された場合、パラメータOpenIDForSendはブラックリストで、最大10個までサポートされます。
-　タイプにAUDIO_ROUTE_RECV_WHITE_LISTが渡された場合、パラメータOpenIDForSendはホワイトリストで、最大10個までサポートされます。
>

#### 戻り値

インターフェースの戻り値がQAV_OKの場合、成功したことを示します。
-　コールバックが1004を返した場合、パラメータが間違っていることを示します。パラメータが正しいかどうかを再確認することをお勧めします。
−　コールバックが1001を返した場合は、動作が繰り返されることを示します。
-　コールバックが1201を返した場合は、ルームが存在しないことを示します。ルーム番号が正しいかどうかを確認することをお勧めします。
-　コールバックが10001と1005を返した場合は、インターフェースをもう一度呼び出すことをお勧めします。

返された結果の詳細について、[エラーコード](https://intl.cloud.tencent.com/document/product/607/33223)をご参照ください。


####  サンプルコード

 **実行ステートメント**
```
@synthesize _sendListArray;
@synthesize _recvListArray;

int ret =  [[[ITMGContext GetInstance] GetRoom] SetServerAudioRouteSendOperateType:SendType  SendList:_sendListArray RecvOperateType:RecvType RecvList:_recvListArray];
if (ret != QAV_OK) {
    UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"audiorouteリストの更新に失敗しました" message:[NSString stringWithFormat:@"エラーコード:%d",ret] delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
    [alert show];
}
```
**コールバック**
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSString *log = [NSString stringWithFormat:@"OnEvent:%d,data:%@", (int)eventType, data];
    switch (eventType) {
                case ITMG_MAIN_EVENT_TYPE_SERVER_AUDIO_ROUTE_EVENT:{
            {
                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"audioroute更新" message:[NSString stringWithFormat:@"結果:%@,sub_type: %@ errorinof: %@", data[@"result"],data[@"sub_type"],data[@"error_info"]] delegate:NULL cancelButtonTitle:@"OK" otherButtonTitles:nil];
                              [alert show];
            }
        }
        default:
            break;
    }
}
```


### オーディオ設定転送ルールの取得

このインターフェースを呼び出すとオーディオ転送ルールを取得します。呼び出し後、インターフェースはルールを返します。渡された配列パラメータは、対応するルールのopenIdを返します。

#### インターフェースのプロトタイプ

```
//iOSインターフェース
-(ITMG_SERVER_AUDIO_ROUTE_SEND_TYPE)GetCurrentSendAudioRoute:(NSMutableArray *) OpenIDForSend;
-(ITMG_SERVER_AUDIO_ROUTE_RECV_TYPE)GetCurrentRecvAudioRoute:(NSMutableArray *)OpenIDForRecv;
//Unityインターフェース
public abstract ITMG_SERVER_AUDIO_ROUTE_SEND_TYPE GetCurrentSendAudioRoute(List<string> OpenIDforSend);
public abstract ITMG_SERVER_AUDIO_ROUTE_RECV_TYPE GetCurrentRecvAudioRoute(List<string> OpenIDforRecve);
```


#### 戻りルール

**ITMG_SERVER_AUDIO_ROUTE_SEND_TYPE**

| 受信タイプ                       | 効果                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| AUDIO_ROUTE_NOT_SEND_TO_ANYONE | ローカルオーディオは上りリンクによりバックグラウンドに送信されますが、バックグラウンドは誰にも転送されず、自分自身をミュートすることになります |
| AUDIO_ROUTE_SEND_TO_ALL        | ローカルオーディオは上りリンクにより全ての人に転送されます                                   |
| AUDIO_ROUTE_SEND_BLACK_LIST    | ローカルオーディオは上りリンクによりブラックリストの人に転送されません                             |
| AUDIO_ROUTE_SEND_WHITE_LIST    | ローカルオーディオは上りリンクによりホワイトリストの人に転送されます                             |
|AUDIO_ROUTE_RECV_INQUIRE_ERROR |取得エラーです。ルームに入ったかどうか、SDKが初期化されたかどうかを確認します

**ITMG_SERVER_AUDIO_ROUTE_RECV_TYPE**

| 受信タイプ                       | 効果                                                         |
| -------------------------------- | ---------------------------------------------- |
| AUDIO_ROUTE_NOT_RECV_FROM_ANYONE | ローカルはオーディオを受け付けません。ルームスピーカーの効果をオフにすることに相当します |
| AUDIO_ROUTE_RECV_FROM_ALL        | ローカルはすべての人の音声を受信します                           |
| AUDIO_ROUTE_RECV_BLACK_LIST      | ローカルはブラックリストの人からのオーディオ音声を受信しません                 |
| AUDIO_ROUTE_RECV_WHITE_LIST      | ローカルはホワイトリストの人物の音声のみを受信します                 |
|AUDIO_ROUTE_RECV_INQUIRE_ERROR |取得エラーです。ルームに入ったかどうか、SDKが初期化されたかどうかを確認します

>!`SetServerAudioRouteSendOperateType`インターフェースで`AUDIO_ROUTE_RECV_INQUIRE_ERROR`を使用しないでください。



