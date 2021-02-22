## シナリオ
ドメイン名でのプッシュ成功後、LVBコンソールに入り、再生アドレスジェネレーターを使用してプッシュアドレスのStreamNameと同じStreamNameを入力すれば、対応する再生アドレスを生成でき、当該再生アドレスによってライブストリーミング画面を見ることができるようになります。

## 前提条件
 -  [LVBコンソール](https://console.cloud.tencent.com/live)にログイン済みであること。
 - **再生ドメイン名**を追加済みであること 。

## 操作手順
1. [【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)を選択し、設定したい**再生ドメイン名**または【管理】をクリックして、ドメイン名管理に入ります。
2. 【再生設定】>【再生アドレスジェネレーター】を選択して、以下の設定を行います。
	1. 期限切れ時間を選択します（例：`2019-02-28 23:59:59）。
	2. カスタマイズしたストリームネームStreamNameを入力します（例：`liveteststream`）。再生アドレスのStreamNameがプッシュアドレスStreamNameと一致している場合のみ、対応するストリームを再生できます。
	3. 【再生アドレスの生成】をクリックして完了です。
![](https://main.qcloudimg.com/raw/6bea977acb754ec9c36422aef3189f39.png)
3. 再生ドメイン名の再生認証を有効にしていない場合は、【再生設定】>【再生アドレス】で、当該再生ドメイン名でのRTMP、FLV、HLSの3種類の再生アドレスが確認できます。再生アドレスの中の StreamName（ストリーム名）を交換してプッシュアドレスを関連付けると、その後すぐに再生アドレス経由でライブストリーミングの画面を見ることができるようになります。
![](https://main.qcloudimg.com/raw/8d8a9ee63dc12045da418c1539051eb6.png)

>LVB再生関連のより詳しい情報については、 [LVB再生](https://intl.cloud.tencent.com/document/product/267/31559)をご参照ください。




## 再生アドレス
### 1. 再生アドレス生成ルール
```
RTMP形式：rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
FLV形式：http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
M3U8形式：http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```
- **domain**：独自のICP申告済み再生ドメイン名。
- **AppName**：アプリケーション名。デフォルトはliveで、カスタマイズによる設定を希望する場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category) する必要があります。
- **StreamName**：ストリーム名。ユーザーがカスタマイズし、ライブストリームの識別に使用します。
- **txSecret**：再生認証を有効にした後に生成される認証文字列。
- **txTime**：再生アドレス設定のタイムスタンプ。コンソールの再生アドレスの有効時間に使用します。

>
>- ドメイン名認証を有効にした場合、「実際の期限切れの時間」=「txTime + 認証有効時間」となります。
>- コンソールでは、利用しやすいように、設定時間を実際の期限切れ時間としています。ドメイン名認証を有効にした場合、再生アドレスの計算時に、公式にもとづきtxTimeが逆算されます。

### 2. トランスコーディング後のライブストリーミングアドレス
再生ドメイン名にトランスコードテンプレートを設定した場合は、同時にトランスコーディング後のライブストリーミングを再生する必要があります。トランスコーディングの再生アドレスの接合方式は、初期再生アドレスの中の StreamNameの後に`_トランスコードテンプレート名`を追加します。

例：初期再生アドレスが`http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)` 、関係付けしたトランスコードテンプレート名が`hd`の場合、トランスコーディング再生アドレスは次となります。`http://domain/AppName/StreamName_hd.flv?txSecret=Md5(key+StreamName_hd+hex(time))&txTime=hex(time)`

### 3. H.265の再生アドレスの再生 
H.265を採用してプッシュし、同時にH.265のライブストリーミングを再生する場合は、StreamNameの後に「_h265」を追加し、再生アドレスを改めて生成する必要があります。
>
>- 「_h265」を追加しない場合、H.264のライブストリーミング再生にはトランスコーディング料金が発生します。
>- StreamNameに「_h265」を追加した後には、再生アドレスを改めて生成する必要があり、直接生成済みの再生アドレスの中に追加することはできません。こうしない場合は、再生アドレスが使用できなくなります。
>
例えば、初期再生アドレスが `http://domain/AppName/StreamName1.flv?txSecret=Md5(key+StreamName1+hex(time))&txTime=hex(time)`で、H.265でプッシュする場合は、「StreamName1_h265」を使って生成した次の再生アドレスが必要となります。：`http://domain/AppName/StreamName1_h265.flv?txSecret=Md5(key+StreamName1_h265+hex(time))&txTime=hex(time)`
