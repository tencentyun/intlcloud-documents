ドメイン名でのプッシュ成功後、CSSコンソールに入り、再生アドレスジェネレーターを使用してプッシュアドレスのStreamNameと同じStreamNameを入力すれば、対応する再生アドレスを生成でき、当該再生アドレスによってライブストリーミング画面を見ることができるようになります。

##  前提条件
 -  [CSSコンソール](https://console.cloud.tencent.com/live)にログイン済みであること。
 - **再生ドメイン名**を追加済みの場合、詳細について[独自のドメイン名の追加](https://intl.cloud.tencent.com/document/product/267/35970)をご参照ください。

## 操作手順
1. **[ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)**を選択し、設定したい再生ドメイン名または**管理**をクリックして、ドメイン名管理に進みます。
2. **再生設定**>**再生アドレスジェネレーター**を選択して、以下の設定を行います。
	1. **オリジナルストリームを再生**、**トランスコーディングストリームを再生**、**アダプティブ・ビットレートストリームを再生**から選択します。**トランスコーディングストリームを再生**を選択した場合、設定済みのトランスコーディングテンプレートを使用しトランスコーディングストリームを出力することができます。**アダプティブ・ビットレートストリームを再生**を選択した場合、設定済みのアダプティブ・ビットレートテンプレートを使用しアダプティブ・ビットレートストリームを出力することができます。
	2. カスタマイズしたStreamNameを入力します（例：`liveteststream`）。再生アドレスのStreamNameがプッシュアドレスStreamNameと一致している場合のみ、対応するストリームを再生できます。
	3. アダプティブ・ビットレートストリームの場合、アダプティブ・ビットレートサブテンプレート名が表示され、ビットレートが降順で並びます。
	4. アドレスの有効期間を選択します（例：2021-06-30 19:00:44）。
3. **アドレスの発行**をクリックすれば完了です。
![](https://qcloudimg.tencent-cloud.cn/raw/ae67aa5386d9f47d7bd20d7cce7c7603.png)
4. 再生ドメイン名の再生認証が有効になっていない場合は、**再生設定**>**再生アドレス解析**タグで、当該再生ドメイン名でのRTMP、FLV、HLS、UDPの4種類の再生アドレスが確認できます。再生アドレスの中のStreamName（ストリーム名）を置き換えてプッシュアドレスをバインドすると、その後すぐに再生アドレス経由でライブストリーミングの画面を見ることができるようになります。
![](https://qcloudimg.tencent-cloud.cn/raw/16a192a0090e8f4f470ace2b78cac52e.png)
>? CSSの再生については、 [CSS再生](https://intl.cloud.tencent.com/document/product/267/31559)をご参照ください。


## 再生アドレス
### 再生アドレス発行ルール
```
RTMP形式：rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
FLV形式：http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
M3U8形式：http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
UDP形式：webrtc://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```
- domain：独自のICP登録済み再生ドメイン名。
- AppName：ライブストリーミングのアプリケーション名。デフォルトはliveで、カスタマイズ可能です。
- StreamName：ストリーム名。ユーザーがカスタマイズし、CSSストリームの識別に使用します。
- txSecret：再生認証を有効にした後に生成される認証文字列。
- txTime：再生アドレス設定のタイムスタンプ。コンソールの再生アドレスの有効時間に使用します。

>!
>- ドメイン名認証を有効にした場合、「実際の期限切れの時間」 = 「txTime + 認証有効時間」となります。
>- コンソールでは、利用しやすいように、設定時間を実際の期限切れ時間としています。ドメイン名認証を有効にした場合、再生アドレスの計算時に、公式にもとづきtxTimeが逆算されます。
>- 有効期限までにプッシュプルストリームを行った場合、プッシュプルストリームが正常であり、中断や停止がなければ、有効期限が過ぎても正常なプッシュプルストリームの状態を維持することができます。

### トランスコーディング後のライブストリーミングアドレス
再生ドメイン名にトランスコードテンプレートを設定した場合は、同時にトランスコーディング後のライブストリーミングを再生する必要があります。トランスコーディングの再生アドレスの接合方式は、初期再生アドレスの中の StreamNameの後に`_トランスコードテンプレート名`を追加します。

例：初期再生アドレスが`http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)` 、関係付けしたトランスコードテンプレート名が`hd`の場合、トランスコーディング再生アドレスは次のようになりますなります。`http://domain/AppName/StreamName_hd.flv?txSecret=Md5(key+StreamName_hd+hex(time))&txTime=hex(time)`

### アダプティブ・ビットレートのライブストリーミングアドレス

再生ドメイン名にアダプティブ・ビットレートテンプレートを設定した場合は、現在、アダプティブ・ビットレートはHLSプロトコルとWebRTCプロトコルだけをサポートしています。これらの2プロトコルのアダプティブ・ビットレートアドレスの接合方法は異なります。
- **HLSアダプティブ・ビットレートアドレスの接合方法として、**オリジナル再生アドレスの中のStreamNameの後ろに`_アダプティブ・ビットレートテンプレート名`を追加します。
例：元の再生アドレスは`http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`とし、关関連するアダプティブ・ビットレートテンプレート名は`autobitrate`とすれば、
HLSアダプティブ・ビットレート再生アドレスは`http://domain/AppName/StreamName_autobitrate.m3u8?txSecret=Md5(key+StreamName_autobitrate+hex(time))&txTime=hex(time)`となります。
- **WebRTCアダプティブ・ビットレートアドレスの接合方法として、**`再生ドメイン名(domain)+AppName(デフォルトはlive)+StreamName(ストリームID)+認証情報+アダプティブ・ビットレートテンプレート名リスト+開始再生ビットレートサブテンプレート名+ビットレート切替方法`となります。アダプティブ・ビットレートサブテンプレート名は、ビットレートの降順で並びます。
例：アダプティブ・ビットレートテンプレートに次のサブテンプレートがあるとします。サブテンプレート1は名前がtest1で、ビットレートが200です。サブテンプレート2は名前がtest2で、ビットレートが300です。サブテンプレート3は名前がtest3で、ビットレートが400です。
では、WebRTCアダプティブ・ビットレートアドレスが`webrtc://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)&tabr_bitrates=test3,test2,test1&tabr_start_bitrate=test1&tabr_control=auto`になります。




### H.265の再生アドレスの再生
Cloud Streaming ServicesはH.265エンコーディングを介したプッシュおよびライブストリーミングをサポートしています。ライブストリーミングのオリジナルストリームがH.264コーデックを使用する場合も、ライブストリーミングトランスコードテンプレートを介してCSSストリームをH.265にトランスコードして再生することができます。コンソールのトランスコードの使用については、[CSSコンソールのトランスコード](https://intl.cloud.tencent.com/document/product/267/31561)、APIトランスコードについては[CSSトランスコードAPI](https://intl.cloud.tencent.com/document/product/267/31561)を参照してください。
