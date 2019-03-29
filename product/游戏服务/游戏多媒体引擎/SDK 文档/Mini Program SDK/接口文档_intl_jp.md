Mini Program開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、ここでMini Program開発のための導入文書を紹介します。


## GMEサービスの申請

Tencent CloudコンソールでGME関連サービスを申請してください。詳細については、[導入ガイド](https://cloud.tencent.com/document/product/607/10782)を参照してください。

## Mini Program LVBサービスの申請
### 1. Liveサービスへのアクセス
Tencent Cloudコンソールにログインした後、【Live】サービスを検索して、[Liveサービス申請インターフェース](https://console.cloud.tencent.com/live)に入ります。

### 2. Liveサービスの申請
【同意】ボタンをクリックし、【有効化の申請】ボタンをクリックしてLiveサービスを有効化します。

![](https://main.qcloudimg.com/raw/3cc2238c29b077c8c9b50a5f62ce0df6.png)

> Liveサービスを申請する前に、実名認証が必要です。【アカウント情報】で実名認証を申請してください。

### 3. サービス申請成功
次の画面が表示されたら、Liveサービスの申請が成功となります。

![](https://main.qcloudimg.com/raw/53d626f2dea1eaecf459636db1481e4b.png)

### 4. 再生用ドメイン名の申請
サービス申請が完了したら、インターフェースの左側にあるナビゲーションウィンドウの【ドメイン名管理】をクリックして、ドメイン名管理インターフェースに進みます。
Liveサービスはプッシュドメイン名を自動的に生成します。【ドメイン名の追加】ボタンをクリックして、再生ドメイン名を申請します。

![](https://main.qcloudimg.com/raw/d24740621f990a6101ee031de1a78cc4.png)
> LVBプッシュと再生のために自身の登録済みドメイン名を追加してください。ドメイン名の管理と利用方法については、[ドメイン名管理](https://cloud.tencent.com/document/product/267/30559)および[CNAME構成](https://cloud.tencent.com/document/product/267/30010)を参照してください。


### 5. 再生ドメイン名申請成功
再生アドレスの申請が成功した後、インターフェースにはプッシュドメイン名と再生ドメイン名、という2つのドメイン名があります。

![](https://main.qcloudimg.com/raw/df0850145ad53d12285e8e1b8f29cec5.png)


## RTMPストリームURLの生成
RTMPストリームは2つのモードをサポートします。1つはルーム内で発言している特定のメンバーのRTMPストリームをプルするモードで、もう1つはルーム内のすべての発言中のメンバーによって合成されたRTMPストリームをプルするモードです。モード1では指定されたメンバーの発言しか聞こえません。モード2ではすべてのメンバーの発言が聞こえます。

RTMPストリームURLの生成には、次の情報が必要です。

|パラメータ|意味|取得方法|
|-----|-----|-----|
|AppID|GMEコンソールで申請したAppID|Tencent Cloudコンソール|
|RoomID|このユーザーがリスニングする必要のあるルームID |開発者がアプリケーションで生成|
|UserID|このユーザーがリスニングする必要がある他のユーザーのID |開発者がアプリケーションで生成 |
|BizID|Liveサービスコンソールによって生成された識別コード |下記のステップ1を参照|
|StreamKey|Liveサービスコンソールによって生成された暗号鍵|下記のステップ1を参照|
|StreamID|RTMPストリームの一意なID|下記のステップ2を参照|
|Timestamp|タイムスタンプ。秒単位|開発者により生成・記入|


RTMPストリームURLの生成には、次の手順が必要です。
### 1. BizIDとStreamKeyの取得

- ドメイン名管理インターフェースに入り、再生ドメイン名の欄で【管理】ボタンをクリックして、再生ドメイン名管理インターフェースに入ります。
  
  ![](https://main.qcloudimg.com/raw/df0850145ad53d12285e8e1b8f29cec5.png)

- インターフェースは図に示すように、CNAMEの欄では、「.liveplay.myqcloud.com」サフィックスの前にある再生ドメイン名は、BizIDパラメータです。例えば、次の図のBizIDは38251です。

- インターフェース上のAPI KeyはStreamKeyパラメータです
  
  ![](https://main.qcloudimg.com/raw/6a0a8c119acd2d49b575a40aa7ededcc.png)


### 2. StreamIDの生成

モード1：
```
{AppID}_{UserID}_{RoomID}_main
```
モード2：
```
mixer_{AppID}_{RoomID}
```

### 3. 最終URLの生成
```
rtmp://{BizID}.liveplay.myqcloud.com/live/MD5({StreamID})?txSecret= MD5({StreamKey}{streamidMd5}{timestamp})&txTime={timestamp}
```

> ここでMD5()；はMD5を計算するための関数です。

## サンプルコード

サンプルに必要な情報は次のとおりです。

```
Bizid:38251
streamKey:4531cddc5bd6dc28a812bb87121a5853
AppID:1400089356
RoomID:20180301
Userid:123456
timestamp:1551438840
```

RTMPアドレスは次のとおりです。

```
モード1：
rtmp://38251.liveplay.myqcloud.com/live/38251_5a1d7c2f7e8fcb56942691035b49d960?txSecret=09fcc68fc320336c2b85071b11056bd6&txTime=5c7913f8

モード2：
rtmp://38251.liveplay.myqcloud.com/live/38251_fed2b77fb622dcbf978ed6041d9f52d9?txSecret=2d69cfbd346da4531d82624a0bed9368&txTime=5c7913f8
```


