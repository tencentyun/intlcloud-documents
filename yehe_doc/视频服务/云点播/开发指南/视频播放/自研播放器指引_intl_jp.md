VODは、長い動画やビデオ暗号化のシナリオを対象に、Android、iOS、Webの3種類の端末の[プレーヤーSKD](https://intl.cloud.tencent.com/document/product/266/7836)を提供しています。VODのSDKを使用すれば、VODでの再生機能を素早く統合することができます。VOD Super Player SDKでカスタマイズのニーズを満たすことができない場合は、Player+とVODバックエンドの通信プロトコルを参照して、プレーヤーを自社開発することができます。以下で、プレーヤーSDKとVODバックエンドの通信プロトコルの詳細をご紹介します。

## プロトコル
リクエストをHTTP Getメソッドで発信します。URLは、`https://playvideo.qcloud.com/{interface}/{version}/{appId}/{fileId}?psign=xxx&cipheredOverlayKey=xxx&cipheredOverlayIv=xxx&keyId=x`です。

### ドメイン名
* メインドメイン名：`playvideo.qcloud.com`
* バックアップドメイン名：`bkplayvideo.qcloud.com`

### リクエストフィールド
#### pathフィールド

| フィールドの定義 | 入力必須か | フィールドの値 |
| -- | -- | -- |
| appId | はい | appidを入力します（サブアプリケーションを使用している場合はsubappidを入力）。 |
| fileId | はい | 再生したいビデオファイルID。 |
| version | はい | v4と入力（固定値）。 |
| interface | はい | getplayinfoと入力（固定値）。 |

#### querystringフィールド

| フィールドの定義 | 入力必須か | フィールドの値 |
| -- | -- | -- |
| psign | いいえ | Super Playerの署名。パラメータの入力については後述のSuper Player署名の章を参考にし、署名方法については、[Super Player署名ドキュメント](https://intl.cloud.tencent.com/document/product/266/38099)をご参照ください。 |
|context|いいえ|パススルーフィールド。リターンパケットの中に元のままの状態で戻されます。|
|cipheredOverlayKey|いいえ |所定外のKey暗号化に使用する暗号化Key。256文字の16進数で表示します。例：5872bd2fcc76176a2db6fcd1341c04e891643e938bf8901310846de62d6942f49e7393cbaf96fd48bfeb7f50878d5bafe93017670e4483e6ccc3c8908ee2ae42823b875aa171a44781cc417163d19d503dda2ba1e6242f41b49c1de12bed52de310a71ba3d8660a9a086289a54f573f1141c451b6ec88ca917c586b4d7735e20。|
|cipheredOverlayIv|いいえ| 所定外のKey暗号化に使用する暗号化のための初期化ベクトル。256文字の16進数で表示します。例：5872bd2fcc76176a2db6fcd1341c04e891643e938bf8901310846de62d6942f49e7393cbaf96fd48bfeb7f50878d5bafe93017670e4483e6ccc3c8908ee2ae42823b875aa171a44781cc417163d19d503dda2ba1e6242f41b49c1de12bed52de310a71ba3d8660a9a086289a54f573f1141c451b6ec88ca917c586b4d7735e20。|
|keyId|いいえ|暗号鍵のバージョン。値の範囲：[0,1]。値が0の時は、cipheredOverlayKeyとcipheredOverlayIvが無効であることを表し、値が1の時は、cipheredOverlayKeyとcipheredOverlayIvが有効であることを表します。|

### Super Playerの署名
#### 署名パラメータ

| パラメータ名 | 記入必須 | タイプ | 説明 |
| -- | -- | -- | -- |
| appId | はい | Integer | アカウントappId。|
| fileId | はい | String | ファイルID。|
| currentTimeStamp | はい | Integer | 配布した署名の現在のUnixタイムスタンプ。 |
| expireTimeStamp | はい | Integer | 配布された署名の有効期限のUnixタイムスタンプ。未入力の場合は署名配布後1日間で期限切れとなることを表します。 |
| pcfg | いいえ | String | 使用するSuper Player設定名。Defaultの場合は、入力不要です。|
| urlAccessInfo | いいえ | Object | 再生リンクのホットリンク防止設定パラメータ、UrlAccessInfoタイプ。 |
| drmLicenseInfo | いいえ | Object | 暗号化コンテンツのキー設定パラメータ、DrmLicenseInfo タイプ。 |

##### UrlAccessInfoタイプ

| パラメータ名 | 記入必須 | タイプ | 説明 |
| -- | -- | -- | -- |
| t | いいえ | String | 16進数の文字列。リンクの期限切れ時間を表します。具体的な定義と値については、[ホットリンク防止パラメータ](https://intl.cloud.tencent.com/document/product/266/33986)の中のtパラメータをご参照ください。未入力の場合は、署名生成後1日間で期限切れとなることを表します。|
| exper | いいえ | Integer |  プレビュー時間。単位は秒、10進数で表示します。プレビュー時間を指定したい場合、時間は30秒（すなわち1/2分）以上とする必要があります。具体的な定義と値については、[ホットリンク防止パラメータ](https://intl.cloud.tencent.com/document/product/266/33986)の中のexperパラメータをご参照ください。|
| rlimit | いいえ | Integer | 異なるIPの端末で再生を許可する最大数。10進数で表示します。具体的な定義と値については、[ホットリンク防止パラメータ](https://intl.cloud.tencent.com/document/product/266/33986)の中のrlimitパラメータをご参照ください。 |
| us | いいえ | String | リンクID。リンクの一意性の強化のため使用します。具体的な定義および値については、[ホットリンク防止パラメータ](https://intl.cloud.tencent.com/document/product/266/33986)の中のusパラメータをご参照ください。|

##### DrmLicenseInfoタイプ

| パラメータ名 | 記入必須 | タイプ | 説明 |
| -- | -- | -- | -- |
| expireTimeStamp | いいえ | Integer | キーの有効期限のUnix タイムスタンプ。未入力の場合は署名配布後1日で期限切れとなることを表します。 |
| strictMode | いいえ | Integer | 検証レベル。値の範囲は[0,1,2]。値が0の時は、コンテンツキーの直接パススルー、または対称キーを採用したコンテンツキーの暗号化、もしくはペアキーおよび非対称キーを採用したコンテンツキーの暗号化の3種類のストラテジーを許可することを表します。値が1の時は、ペアキーを採用したコンテンツキーの暗号化または対称キーおよび非対称キーを採用したコンテンツキーの暗号化の2種類のストラテジーを許可することを表します。値が2の時は、対称キーおよび非対称キーを採用したコンテンツキーの暗号化のストラテジーのみを許可することを表します。コンテンツキーの直接パススルーは、いずれの端末でも再生できます。コンテンツキーの暗号化後は、クライアントでコンテンツキーを復号することで再生できるようになります。 |

### レスポンスフィールド

| パラメータ名 | タイプ | 説明 |
| -- | -- | -- |
| code | Integer | エラーコード。codeが0でない時はエラーであることを表します。 |
| message | String | エラーメッセージ。codeが0でない時は値があります。 |
| version | Integer | 現在の戻ってくる結果のバージョンタイプ。値は4です（固定値）。 |
| warning | String | 警告メッセージ。ホットリンク防止を有効にしていない時にpsignパラメータが含まれていると、警告が返ってきます。 |
| media | Object | メディア情報。エレメントのタイプはMediaです。

#### Mediaタイプ

| パラメータ名 | タイプ | 説明 |
| -- | -- | -- |
| basicInfo | Object | ビデオ基本情報。タイプはBasicInfoです。 |
| streamingInfo | Object | マルチビットレートビデオ情報。タイプはStreamingInfoです。 |
| imageSpriteInfo | Object | サムネイル情報。主にプレーヤーでのビデオプレビューの実装に使用します。タイプはImageSpriteInfoです。 |
| keyFrameDescInfo | Object | ビデオのキーフレーム情報。プレーヤーの時間軸上のキーフレームの表示に使用されます。タイプはKeyFrameDescInfoです。 |

#### BasicInfoタイプ

| パラメータ名 | タイプ | 説明 |
| -- | -- | -- |
| name | String | ビデオ名。 |
| size | Integer | ビデオサイズ。単位：byte。 |
| duration | Float | ビデオの長さ。単位：秒。 |
| description | String | ビデオの説明。 |
| coverUrl | String |ビデオカバー。 |

#### StreamingInfoタイプ

| パラメータ名 | タイプ | 説明 |
| -- | -- | -- |
|plainOutput|String|非暗号化の出力。タイプはStreamingOutputです。 |
|drmOutput|Array|ビデオをDRM暗号化した後に出力します。タイプはStreamingOutputです。 |
|drmToken|String| DRM暗号化の出力を再生する時に使用するDRM Token。再生時にはこのフィールドをstreamingOutput.url の中に合成します。 |

#### StreamingOutputタイプ

| パラメータ名 | タイプ | 説明 |
| -- | -- | -- |
| type | String | アダプティブビットレートストリーミング保護タイプ。現在、設定値にはplain とsimpleAESがあります。plainは非暗号化を表し、simpleAESはHLSのノーマルな暗号化を表します。 |
| url | String | 再生URL。 |
| subStreams | Array | サブストリーム情報。タイプはSubStreamInfoです。 |

#### SubStreamInfoタイプ

| パラメータ名 | タイプ | 説明 |
| -- | -- | -- |
| type | String | サブストリームのタイプ。現在設定可能な値はvideoのみです。 |
| width | Integer | サブストリームのビデオの幅。単位：px。 |
| height | Integer | サブストリームのビデオの高さ。単位：px。 |
| resolutionName | String | プレーヤーで表示するサブストリームのビデオの仕様名。 |

#### ImageSpriteInfoタイプ

| パラメータ名 | タイプ | 説明 |
| -- | -- | -- |
| imageUrls | Array | サムネイルダウンロードURLアレイ。タイプはString 。 |
| webVttUrl | String | サムネイルVTTファイルダウンロードURL 。 |

### 暗号化出力の再生

リクエストによって戻ってきた結果が暗号化後のビデオ（streamingOutput.typeがsimpleAES）の場合は、streamingInfo.drmTokenをstreamingOutput.url のファイル名の中に合成して、リンクを生成し再生する必要があります。

**スプライシングルール**：新しいファイル名 = voddrm.token.{合成が必要なtoken}.{元のファイル名}

例えば、streamingOutput.url が`http://125xxx167.vod2.myqcloud.com/xxx/xxx/xx.m3u8?t=5c08d9fa&us=someus&sign=xxx`、drmToken が`JhbGciOxxxsInR5cCI6Ikp`だとします。
この場合、再生のためのURLは次のようになります。
`http://125xxx167.vod2.myqcloud.com/xxx/xxx/voddrm.token.JhbGciOxxxsInR5cCI6Ikp.xx.m3u8?t=5c08d9fa&us=someus&sign=xxx`。


## プライベート化した暗号化の詳細説明

HLSの通常の暗号化の原理は、m3u8ファイルのEXT-X-KEY タグの中のURIにコンテンツキー（Key）を取得するアドレスを指定し、プレーヤーで再生する時にリアルタイムにコンテンツキー（Key）を取得し、復号して再生するというものです。
このKeyは平文形式で渡されるため、セキュリティレベルは低くなり、一部のブラウザのプラグインでは解読される可能性があります。
VODではこの問題に対処するため、暗号化をプライベート化する方法を提供しています。すなわち、リアルタイムに生成したOverlayKeyとOverlayIvを使用し、コンテンツキー（Key）に対して、AES-128 CBCアルゴリズムを採用して二次暗号化を行います。さらにクライアントでも指定公開鍵を採用し、RSAアルゴリズムを使ってOverlayKeyとOverlayIvを暗号化し、コンテンツキー（Key）の漏洩を防止します。
具体的な方法の手順は次のとおりです。
### 1 Psignの取得
**プレーヤー：**
プレーヤーの再生開始時に、まず業務サーバーにPsignの取得をリクエストします 。
**業務サーバー：**
それぞれのシナリオに応じてStrictModeパラメータを入力して、Psignを計算し、配布する必要があります。
### 2 一時キーに対する暗号化
**プレーヤー：**
プレーヤーが一時キーであるOverlayKey とOverlayIvをランダム生成します。その後、暗号鍵バージョン（KeyId）に1を指定し、KeyId=1に対応するPublicKeyを使用して、OverlayKeyとOverlayIvに対してそれぞれRSAでの暗号化を行い、CipheredOverlayKeyとCipheredOverlayIvを取得します。その後さらに手順1で取得したPsignと一緒にVODリクエストのquerystring中に書き込みます。

### 3 一時キーを使用したKeyの復号
**プレーヤー：**
暗号化されたビデオの再生時、m3u8のEXT-X-KEYの指定URLから取得できたKeyは、すでにOverlayKeyとOverlayIVによって暗号化されています。この時、プレーヤーはOverlayKeyとOverlayIVを使用してKeyに対して復号を行なってから、さらに復号後のKeyを使用して復号し再生する必要があります。

### 4 暗号化アップグレードプランの全体的な業務フローチャート：

![](https://main.qcloudimg.com/raw/872e8921a291877be233da67f25138bb.png)


## 事例
以下に、暗号化して出力したビデオの再生を例として示します。

### リクエスト
`https://playvideo.qcloud.com/getplayinfo/v4/125xxx167/52858xxx74597?psign=0eef1a12dxxxf0f48ebf34b4&cipheredOverlayKey=5872bd2fcc76176a2db6fcd1341c04e891643e938bf8901310846de62d6942f49e7393cbaf96fd48bfeb7f50878d5bafe93017670e4483e6ccc3c8908ee2ae42823b875aa171a44781cc417163d19d503dda2ba1e6242f41b49c1de12bed52de310a71ba3d8660a9a086289a54f573f1141c451b6ec88ca917c586b4d7735e20&cipheredOverlayIv=5872bd2fcc76176a2db6fcd1341c04e891643e938bf8901310846de62d6942f49e7393cbaf96fd48bfeb7f50878d5bafe93017670e4483e6ccc3c8908ee2ae42823b875aa171a44781cc417163d19d503dda2ba1e6242f41b49c1de12bed52de310a71ba3d8660a9a086289a54f573f1141c451b6ec88ca917c586b4d7735e20&keyId=1`

### レスポンス
```json
{
    "code":0,
    "message":"",
    "requestId":"377d94185f0342c5b67b038501f54974",
    "version":4,
    "context":"",
    "warning":"",
    "media":{
        "basicInfo":{
            "name":"アニマルワールド",
            "size":26246026,
            "duration":30.5,
            "description":"ソース元はCCTVの人気動物番組",
            "coverUrl":"http://125xxx167.vod2.myqcloud.com/xxx/xxx/xx.jpg?t=5c08d9fa&amp;someus&amp;sign=xxx"
        },
        "streamingInfo":{
            "plainOutput":{

            },
            "drmOutput":[
                {
                    "type":"simpleAes",
                    "url":"http://125xxx167.vod2.myqcloud.com/xxx/xxx/xx.m3u8?t=5c08d9fa&amp;us=someus&amp;sign=xxx",
                    "subStreams":[
                        {
                            "type":"video",
                            "width":427,
                            "height":240,
                            "resolutionName":"LD"
                        },
                        {
                            "type":"video",
                            "width":853,
                            "height":480,
                            "resolutionName":"SD"
                        },
                        {
                            "type":"video",
                            "width":1280,
                            "height":720,
                            "resolutionName":"HD"
                        }
                    ]
                }
            ],
            "drmToken":"JhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9xxx",
        },
        "imageSpriteInfo":{
            "imageUrls":[
                "http://125xxx167.vod2.myqcloud.com/xxx/xxx/xx.jpg?t=5c08d9fa&amp;us=someus&amp;sign=xxx"
            ],
            "webVttUrl":"http://125xxx167.vod2.myqcloud.com/xxx/xxx/xx.vtt?t=5c08d9fa&amp;us=someus&amp;sign=xxx"
        },
        "keyFrameDescInfo":{
            "keyFrameDescList":[
                {
                    "timeOffset":1.1,
                    "content":"オープニングスタート..."
                },
                {
                    "timeOffset":100.2,
                    "content":"間もなく終了..."
                }
            ]
        }
    }
}
```

## 用語集
| パラメータ名 | タイプ | 説明 |
| -- | -- | -- |
| OverlayKey | String | クライアントでの二次暗号化の暗号鍵。コンテンツキー（Key）に対する暗号化に使用します。128bitのキーを16進数に変換して取得したものとなり、長さ32byteの文字列です。|
| OverlayIv | String | クライアントでの二次暗号化の初期化ベクトル。コンテンツキー（Key）に対する暗号化に使用します。32bit、1つの文字を16進数で表します。 |
| cipheredOverlayKey | String | 所定外のKey暗号化に使用する暗号化Key。256文字の16進数で表示します。|
| cipheredOverlayIv | String | 所定外のKey暗号化に使用する暗号化のための初期化ベクトル。256文字の16進数で表示します。|



## 推奨するデバッグ
次の手順によるデバッグを推奨します。
1. 非暗号化での再生。
2. プライベート化した暗号化による再生。

## 公開鍵
 KeyId =1の時に対応する公開鍵は次のようになります。
```
-----BEGIN PUBLIC KEY-----
MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC3pDA7GTxOvNbXRGMi9QSIzQEI
+EMD1HcUPJSQSFuRkZkWo4VQECuPRg/xVjqwX1yUrHUvGQJsBwTS/6LIcQiSwYsO
qf+8TWxGQOJyW46gPPQVzTjNTiUoq435QB0v11lNxvKWBQIZLmacUZ2r1APta7i/
MY4Lx9XlZVMZNUdUywIDAQAB
-----END PUBLIC KEY-----
```
