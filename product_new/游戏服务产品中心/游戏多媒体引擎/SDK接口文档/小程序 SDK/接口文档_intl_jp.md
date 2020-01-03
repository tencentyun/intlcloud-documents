## 運用シナリオ
このドキュメントでは、ミニプログラム開発者がミニプログラムSDKインターフェースを使用して、Tencent Cloud のGaming Multimedia Engine製品APIをデバッグおよびアクセスする方法を説明します。


## 前提条件
Tencent Cloudの バックグラウンドでGME関連のサービスに申請しました、詳細については、[SDKアクセスガイド](https://intl.intl.cloud.tencent.com/document/product/607/10782)をご参照ください。


## 操作手順
### Live Video Broadcastingサービスを申請する
>Live Video Broadcastingサービスを申請する前に、実名認証が必要です。【アカウント情報】で実名認証を申請します。

1. Tencent Cloud コンソールにログインし、【Live Video Broadcasting】サービスを選択して、[Live Video Broadcastingサービス申請インターフェース](https://console.cloud.tencent.com/live)に入ります。
2. 【『Tencent Cloudサービス契約』に同意する】をチェックし、[アクティブ化を申請]をクリックして、Live Video Broadcastingサービスをアクティブ化します。
3. 【確認】をクリックすると、下図に示すように、Live Video Broadcastingサービスの申請が完了しました。

4.サービスの申請が完了すると、左側のメニューバーの【ドメイン名管理】をクリックして、ドメイン名管理インターフェースに入ります。
5.Live Video Broadcastingサービスはプッシュドメイン名を自動的に生成します、【ドメイン名の追加】をクリックして、再生ドメイン名を申請します。
 >お持ちのICP申告済みドメイン名を追加して、ライブブロードキャストのプッシュと再生を行ってください。ドメイン名管理の使用方法については、[ドメイン名管理](https://intl.cloud.tencent.com/document/product/267/31056)および[CNAME構成](https://cloud.tencent.com/document/product/)をご参照ください。 



再生用アドレスの申請が完了すると、インターフェースにプッシュドメイン名と再生ドメイン名の2つのドメイン名が表示されます。



### rtmp ストリームアドレスを生成する
ルーム内で会話するすべてのメンバーで結合されたrtmpストリームを引き込みます。

rtmpストリームアドレスを生成するには、次の情報が必要です。

|パラメータ|意味|取得方法|
|-----|-----|-----|
| AppID | GMEコンソールによって申請されたAppIDです。 | Tencent Cloudコンソールについて、[SDKアクセスガイド](https://intl.intl.cloud.tencent.com/document/product/607/10782)をご参照ください。|
|RoomID |このユーザーが聞く必要のあるルームIDです。 |このパラメータは、開発者によってアプリケーションで生成されます。|
| BizID |Live Video Broadcastingサービスコンソールによって生成された識別コードです。|このパラメータの取得方法について、次の[ステップ1](＃step1)をご参照ください。|
| StreamKey |Live Video Broadcastingサービスコンソールによって生成されたキーです|このパラメータの取得方法について、次の[ステップ1](＃step1)をご参照ください。|
| StreamID | rtmpストリームの一意の識別子です。|このパラメータの取得方法について、次の[ステップ2](＃step2)をご参照ください。|
| StreamIDMD5 |StreamIDはMd5処理を実行します|このパラメータの取得方法について、次の[ステップ3](＃step3)をご参照ください。|
|Timestamp|タイムスタンプの単位が秒です。|このパラメータは、開発者によってアプリケーションで生成および入力されます。|


rtmp ストリームアドレスを生成するには、次の手順があります。
<span id="step1"></span>
#### BizIDとStreamKeyを取得する
1.ドメイン名管理インターフェースに入り、再生ドメイン名の列で【管理】をクリックして、再生ドメイン名の管理インターフェースに入ります。

2. CNAMEの列では、「.liveplay.myqcloud.com」サフィックスの前の再生ドメイン名がBizIDパラメータです。たとえば、次の図のBizIDは38251であり、APIキーはStreamKeyパラメータです。
 

<span id="step2"></span>
#### StreamIDを生成する

```
mixer_{AppID}_{RoomID}
```

<span id="step3"></span>
####  StreamIDMD5を生成する 
```
{BizID}_{AppID}_{RoomID}_MD5({StreamID};
```

#### 最終アドレスを生成する
```
rtmp://{BizID}.liveplay.myqcloud.com/live/{StreamIDMD5}?txSecret= MD5({StreamKey}{StreamIDMD5}{timestamp})&txTime={timestamp}
```

>MD5()；はMD5を計算するための関数です。



この例に必要な情報は次のとおりです。

```
Bizid:38251
streamKey:4531cddc5bd6dc28a812bb87121a5853
AppID:1400089356
RoomID:20190301
timestamp:5c7913f8
```

rtmpアドレスは次のとおりです。

```
rtmp://38251.liveplay.myqcloud.com/live/38251_1400089356_20190301_fed2b77fb622dcbf978ed6041d9f52d9?txSecret=95c396245d68aed1fa25b8dd79e81aa9&txTime=5c7913f8
```










