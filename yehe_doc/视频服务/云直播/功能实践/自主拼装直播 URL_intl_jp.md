### 前提条件
- Tencent Cloudアカウントが登録済みであり、かつ [Tencent LVBサービス](https://intl.cloud.tencent.com/product/LVB)がアクティブ化されていること。
- 独自のドメイン名があること。
- 【LVBコンソール】>【[Domain Management](https://console.cloud.tencent.com/live/domainmanage)】にプッシュ/再生ドメイン名が追加され、かつCNAMEが正常に実行されていること。詳細な操作については、[独自のドメイン名の追加](https://intl.cloud.tencent.com/document/product/267/35970)をご参照ください。

<span id="push"></span>
### プッシュURLのスプライス
実際のサービスを使用中で、ライブルームが多い場合、キャスターごとに手動でプッシュと再生のURLを作成することはできませんが、サーバーでプッシュと再生のアドレスを**スプライス**することができます。Tencent Cloud標準仕様に準拠するURLであれば、プッシュに使用でき、4つの部分で構成される標準的なプッシュURLは、次のとおりです。
![](https://main.qcloudimg.com/raw/679602c838e8dfd3b61acefebb221d13.jpg)

- **Domain**
プッシュドメイン名には、Tencent Cloud LVBが提供するデフォルトのプッシュドメイン名が使用でき、またはCNAMEが正常に設定された独自のプッシュドメイン名も使用できます。
- **AppName**
LVBアプリケーション名のデフォルトはlive ですが、カスタマイズすることができます。
- **StreamName（ストリームID）**
カスタムストリーム名、各ライブストリーミングのストリームの一意IDには、ランダムな数字または数字とアルファベットの組み合わせを使用することをお勧めします。
- **認証Key（オプション）**
txSecretとtxTimeの両部分を含みます：`txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`。
プッシュ認証が有効な場合は、プッシュに使用されるURLには認証Keyが含まれている必要があります。プッシュ認証が有効でない場合は、プッシュアドレスに「?」とそれに続く内容を含める必要はありません。
 - **txTime（アドレスの有効期限）** 
これはURLの有効期限が切れる時期を意味し、UNIXの16進数のタイムスタンプをサポートしています。
	
	>?例えば、`5867D600`は、2017年1月1日0:00:00に期限が切れることを意味し、クライアントは、通常、txTimeは現在の時間から24時間後に期限切れとなるように設定されます。キャスターがライブストリーミング中にネットワークが途切れた場合にプッシュを再開できるよう、期限切れまでの時間は長すぎず、また短すぎないように設定する必要があります。期限切れまでの時間が短すぎると、キャスターはプッシュ URLの期限切れによってプッシュを再開することができません。
 - **txSecret（ホットリンク防止署名）**
攻撃者がバックエンドを偽造してプッシュURLを生成することを防ぐために使用されます。計算方法については、 [ベストプラクティス-ホットリンク防止の計算](https://intl.cloud.tencent.com/document/product/267/31560)をご参照ください。

<span id="play"></span>
### 再生URL のスプライス
次に例示するとおり、再生アドレスは、主に再生プレフィックス、再生ドメイン名（domain）、アプリケーション名（AppName）、ストリーム名（StreamName）、再生プロトコルサフィックス、認証パラメータ、およびその他のカスタムパラメータで構成されます。	

```	
http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time) 	
rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)	
http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)	
```

- **再生プレフィックス**	
<table>
    <tr><th>再生プロトコル</th><th>再生プレフィックス</th><th>備考</th></tr>
    <tr>
        <td>RTMP</td>
        <td><code>rtmp://</code> </td>
        <td>非推奨。インスタントブロードキャスティングのパフォーマンス不良。高度な同時実行性をサポートせず</td>
    </tr><tr>
        <td>HTTP-FLV </td>
				<td><code>http://</code> または <code>https://</code> </td>
        <td>推奨。インスタントブロードキャスティングのパフォーマンス良好。極めて高度な同時実行性をサポート。</td>
    </tr><tr>
        <td>HLS（m3u8）</td>
        <td><code>http://</code>  または <code>https://</code> </td>
        <td>スマートフォンとMac safariブラウザに推奨される再生プロトコル。</td>
    </tr>
</table>
- **Domain**	
	再生ドメイン名、CNAMEが正常に設定された独自の再生ドメイン名。
- **AppName**	
  ライブストリーミングのアプリケーション名であり、ライブストリームメディアファイルの格納パスを参照するために使用されます。デフォルトはliveで、カスタマイズできます。
- **StreamName（ストリーム名）<span id="streamname"></span>**	
  カスタムストリーム名、各ライブストリーミングのストリームの一意IDには、ランダムな数字または数字とアルファベットの組み合わせを使用することをお勧めします。
- **認証パラメータ（オプション）**	
	txSecretとtxTimeの両部分を含みます：`txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`。
再生認証が有効な場合は、再生に使用されるURLには認証Keyが含まれている必要があります。再生認証が有効ではない場合、再生アドレスに「?」とそれに続く内容を含める必要はありません。
 - **txTime（アドレスの有効期限）：** このURLの有効期限が切れる時期を意味し、UNIXの16進数のタイムスタンプをサポートしています。
 - **txSecret（ホットリンク防止の署名）：**攻撃者がバックエンドを偽造してプッシュURLを生成することを防ぐために使用されます。計算方法については、 [ベストプラクティス-ホットリンク防止の計算](https://intl.cloud.tencent.com/document/product/267/31560)をご参照ください。


<span id="push_code"></span>
### プッシュサンプルコードの表示
【LVBコンソール】>[【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)に移動し、事前に設定したプッシュドメイン名を選択して、【管理】>【プッシュ設定】ページの下半分にホットリンク防止アドレスの生成方法を示す【プッシュアドレスサンプルコード】（PHPとJavaの両バージョン）があります。さらに詳細な情報と操作については、[プッシュ設定](https://intl.cloud.tencent.com/document/product/267/31059)をご参照ください。

