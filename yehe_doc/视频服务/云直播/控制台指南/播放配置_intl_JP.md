## 操作シナリオ
ドメイン名でのプッシュ成功後、CSSコンソールに入り、再生アドレスジェネレーターを使用してプッシュアドレスのStreamNameと同じStreamNameを入力すれば、対応する再生アドレスを生成でき、当該再生アドレスによってライブストリーミング画面を見ることができるようになります。

## 前提条件
 - [CSSコンソール](https://console.cloud.tencent.com/live)にログイン済みであること。
 - **再生ドメイン名**を追加済みの場合、詳細について[独自のドメイン名の追加](https://intl.cloud.tencent.com/document/product/267/35970)をご参照ください。

## 操作手順
1. [【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)を選択し、設定したい**再生ドメイン名**または【管理】をクリックして、ドメイン名管理に入ります。
2. 【再生設定】>【再生アドレスジェネレーター】を選択して、以下の設定を行います。
	1. 期限切れ時間を選択します（例：`2019-02-28 23:59:59）。
	2. カスタマイズしたストリーム名StreamNameを入力します（例：`liveteststream`）。再生アドレスのStreamNameがプッシュアドレスStreamNameと一致している場合のみ、対応するストリームを再生できます。
	3. 設定済みのトランスコードテンプレートを選択することができます。
	3. 【再生アドレスの生成】をクリックして完了です。
![](https://main.qcloudimg.com/raw/6118cad9cca141bcee5c54d8211a9567.png)
3. 再生ドメイン名の再生認証を有効にしていない場合は、【再生設定】>【再生アドレス】タグで、当該再生ドメイン名でのRTMP、FLV、HLSの3種類の再生アドレスが確認できます。再生アドレスの中のStreamName（ストリーム名称）を置き換えてプッシュアドレスを関連付けると、その後すぐに再生アドレス経由でライブストリーミングの画面を見ることができるようになります。
![](https://main.qcloudimg.com/raw/eb03329524d2ccfc2470e27c1b2b8eef.png)

>? CSS再生に関連する詳細情報については、[CSS再生](https://intl.cloud再生.tencent.com/document/product/267/31559)をご参照ください。




## 再生アドレス
### 1. 再生アドレス生成ルール
```
RTMP形式：rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
FLV形式：http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
M3U8形式：http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```
- domain : 独自の再生ドメイン名。
- AppName：ライブストリーミングのアプリケーション名。デフォルトはliveで、カスタマイズ可能です。
- StreamName：ストリーム名。ユーザーがカスタマイズし、CSSストリームの識別に使用します。
- txSecret：再生認証を有効にした後に生成される認証文字列。
- txTime：再生アドレス設定のタイムスタンプ。コンソールの再生アドレスの有効時間に使用します。

>!
>- ドメイン名認証を有効にした場合、「実際の期限切れの時間」 = 「txTime + 認証有効時間」となります。
>- コンソールでは、利用しやすいように、設定時間を実際の期限切れ時間としています。ドメイン名認証を有効にした場合、再生アドレスの計算時に、公式に基づきtxTimeが逆算されます。

### 2. トランスコーディング後のライブストリーミングアドレス
再生ドメイン名にトランスコードテンプレートを設定した場合は、同時にトランスコーディング後のCSSストリームを再生する必要があります。トランスコーディングの再生アドレスのスプライシング方式は、初期再生アドレスの中のStreamNameの後に`_トランスコードテンプレート名`を追加します。

例：初期再生アドレスが`http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`、関係付けしたトランスコードテンプレート名が`hd`の場合、トランスコーディング再生アドレスは次となります。`http://domain/AppName/StreamName_hd.flv?txSecret=Md5(key+StreamName_hd+hex(time))&txTime=hex(time)`

### 3. H.265の再生アドレスの再生
Cloud Streaming ServicesはH.265エンコーディングを介したプッシュおよびライブストリーミングをサポートしています。ライブストリーミングのオリジナルストリームがH.264コーデックを使用する場合も、ライブストリーミングトランスコードテンプレートを介してCSSストリームをH.265にトランスコードして再生することができます。コンソールのトランスコードの使用については、[CSSコンソールのトランスコード](https://intl.cloud.tencent.com/document/product/267/31561)、APIトランスコードについては[CSSトランスコードAPI](https://intl.cloud.tencent.com/document/product/267/31561)を参照してください。
