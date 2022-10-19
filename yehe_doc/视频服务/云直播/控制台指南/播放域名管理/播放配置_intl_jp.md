ドメイン名で正常にプッシュした後、CSSコンソールに入り、再生アドレスジェネレーターにプッシュアドレスのStreamNameを入力し、対応するストリーミングの再生アドレスを生成します。生成された再生アドレスでライブストリーミング画面を見ることができます。

## 前提条件
 - [CSSコンソール](https://console.cloud.tencent.com/live)にログインしていること。
 - **再生ドメイン名**を追加していること。詳しくは[ユーザー保有ドメイン名を追加する](https://intl.cloud.tencent.com/document/product/267/35970)をご参照ください。

## 操作手順
1. **[ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)**を選択し、設定する再生ドメイン名または**管理**をクリックして、ドメイン名管理に進みます。
2. **再生設定**>**再生アドレスジェネレーター**を選択して、以下の設定を行います：
	1. **オリジナルストリームを再生**、**トランスコーディングストリームを再生**、**アダプティブ・ビットレートストリームを再生**から選択します。**トランスコーディングストリームを再生**を選択した場合、設定済みのトランスコーディングテンプレートを使用しトランスコーディングストリームを出力することができます。**アダプティブ・ビットレートストリームを再生**を選択した場合、設定済みのアダプティブ・ビットレートテンプレートを使用しアダプティブ・ビットレートストリームを出力することができます。
	2. カスタマイズしたストリーム名StreamNameを入力します（例：liveteststream）。再生アドレスのStreamNameがプッシュアドレスStreamNameと一致している場合のみ、対応するストリームを再生できます。
	3. アダプティブ・ビットレートストリームの場合、アダプティブ・ビットレートサブテンプレート名が表示され、ビットレートが降順で並びます。
	4. アドレスの有効期間を選択します（例：2021-06-30 19:00:44）。
5. **アドレスを生成**をクリックすれば完了です。
![](https://qcloudimg.tencent-cloud.cn/raw/ae67aa5386d9f47d7bd20d7cce7c7603.png)
3. 再生ドメイン名の再生認証が有効になっていない場合は、**再生設定**>**再生アドレス解析**タグで、当該再生ドメイン名の配下でRTMP、FLV、HLS、UDPの4種類の再生アドレスを確認し、再生アドレスの中のStreamName（ストリーム名）を置き換えてプッシュアドレスと関連を付けます。関連を付けると、再生アドレスでライブストリーミングの画面を見ることができるようになります。
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
- domain：ユーザー保有のICP登録済みの再生ドメイン名。
- AppName：ライブストリーミングのアプリケーション名。デフォルトはliveで、カスタマイズ可能です。
- StreamName：ストリーム名。ユーザーがカスタマイズし、CSSストリームの識別に使用します。
- txSecret：再生認証を有効にした後に生成される認証文字列。
- txTime：再生アドレスに対して設定するタイムスタンプで、再生アドレスの有効期間を制御することに使用されます。

>!
>- ドメイン名認証を有効にした場合、「実際の有効期限」 = 「txTime + 認証有効期間」となります。
>- 利用しやすくするために、コンソールで設定した時間は実際の有効期間です。ドメイン名認証を有効にした場合、再生アドレス計算時に、式に基づきtxTimeを逆算します。
>- 有効期限までにストリームのプッシュ/プルを行った場合、ストリームのプッシュ/プルが中断や停止しない限り、有効期限が切れてもストリームのプッシュ/プル状態を維持することができます。

### トランスコーディングしたライブストリーミングアドレス
再生ドメイン名に対してトランスコーディングテンプレートを設定し、トランスコーディングしたCSSストリームを再生する場合は、トランスコーディングした再生アドレスの接合方法として、オリジナル再生アドレスの中の StreamNameの後ろに`_トランスコーディングテンプレート名`を追加します。

例：オリジナル再生アドレスが`http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`で、関連付けられたトランスコーディングテンプレート名が`hd`の場合、トランスコーディング再生アドレスは`http://domain/AppName/StreamName_hd.flv?txSecret=Md5(key+StreamName_hd+hex(time))&txTime=hex(time)`です。

### アダプティブ・ビットレートのライブストリーミングアドレス

再生ドメイン名にアダプティブ・ビットレートテンプレートを設定した場合は、現在、アダプティブ・ビットレートはHLSプロトコルとWebRTCプロトコルだけをサポートしています。これらの2プロトコルのアダプティブ・ビットレートアドレスの接合方法は異なります。
HLSアダプティブ・ビットレートアドレスの接合方法として、オリジナル再生アドレスの中のStreamNameの後ろに`_アダプティブ・ビットレートテンプレート名`を追加します。
例：オリジナル再生アドレスが`http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`で、関連付けられたアダプティブ・ビットレートテンプレート名が`autobitrate`の場合、HLSアダプティブ・ビットレート再生アドレスは`http://domain/AppName/StreamName_autobitrate.m3u8?txSecret=Md5(key+StreamName_hd+hex(time))&txTime=hex(time)`です。

WebRTCアダプティブ・ビットレートアドレスの接合方法として、「再生ドメイン名(domain)+AppName(デフォルトはlive)+StreamName(ストリームID)+認証情報+アダプティブ・ビットレートテンプレート名リスト+開始再生ビットレートサブテンプレート名+ビットレート切替方法」となります。アダプティブ・ビットレートサブテンプレート名は、ビットレートの降順で並びます。
例：アダプティブ・ビットレートテンプレートに次のサブテンプレートがあるとします。サブテンプレート1は名前がtest1で、ビットレートが200です。サブテンプレート2は名前がtest2で、ビットレートが300です。サブテンプレート3は名前がtest3で、ビットレートが400です。
では、WebRTCアダプティブ・ビットレートアドレスが`webrtc://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)&tabr_bitrates=test3,test2,test1&tabr_start_bitrate=test1&tabr_control=auto`になります。




### H.265でエンコードされたものの再生アドレス
CSSはH.265エンコーディングを介してストリームのプッシュと再生を行います。ライブストリーミングのオリジナルストリームがH.264でエンコードされている場合も、ライブストリーミングトランスコーディングテンプレートを使用し、H.265のCSSストリームにトランスコーディングして再生することができます。コンソールによるトランスコーディングの使用方法については、[CSSコンソールでトランスコーディング](https://intl.cloud.tencent.com/document/product/267/31561)、APIによるトランスコーディングについては、[CSSトランスコーディングAPI](https://intl.cloud.tencent.com/document/product/267/31561)をご参照ください。