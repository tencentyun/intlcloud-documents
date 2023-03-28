## メッセージ内容MsgBodyの説明
MsgBodyに入力されたフィールドはメッセージの内容です。IMは、1つのメッセージにテキストメッセージ要素と顔絵文字メッセージ要素の両方を含むなど、メッセージ内へのさまざまなメッセージ要素タイプの包含をサポートします。従ってMsgBodyはArray型として定義され、必要に応じて複数のタイプのメッセージ要素を追加できます。メッセージ要素名はTIMMsgElementです。メッセージ要素TIMMsgElementによって構成されるMsgBodyの例については、[メッセージ内容MsgBodyインスタンス](https://intl.cloud.tencent.com/document/product/1047/33527)をご参照ください。

メッセージ要素TIMMsgElementの形式は次のように統一されています：
```
{
    "MsgType": "",
    "MsgContent": {}
}
```

| フィールド | タイプ | 説明 |
|---------|---------|---------|
| MsgType | String | メッセージ要素タイプ。現在サポートされているメッセージオブジェクトには、TIMTextElem（テキストメッセージ）、TIMLocationElem（位置メッセージ）、TIMFaceElem（顔絵文字メッセージ）、TIMCustomElem（カスタムメッセージ）、TIMSoundElem（音声メッセージ）、TIMImageElem（画像メッセージ）、TIMFileElem（ファイルメッセージ）、TIMVideoFileElem（ビデオメッセージ）が含まれます。 |
| MsgContent | Object |メッセージ要素の内容。MsgTypeが異なれば、MsgContent形式も異なります。詳細については、下記の文をご参照ください。|

現在サポートされているメッセージタイプMsgTypeを次の表に示します：

| MsgTypeの値 | タイプ |
|---------|---------|
| TIMTextElem | テキストメッセージ。|
|TIMLocationElem|地理的位置メッセージ。|
|TIMFaceElem|顔絵文字メッセージ。|
|TIMCustomElem|カスタムメッセージ。受信者がiOSシステムで、アプリケーションがバックグラウンドにある場合、このメッセージタイプはテキスト以外のフィールドをAPNに送信できます。結合されたメッセージには、TIMCustomElemカスタムメッセージ要素を1つしか含めることができません。|
|TIMSoundElem|音声メッセージ。|
|TIMImageElem|画像メッセージ。|
|TIMFileElem|ファイルメッセージ。|
|TIMVideoFileElem|ビデオメッセージ。|

>!上記タイプのメッセージは、サーバーに統合されたRest APIインターフェースを介して送信できます。

## メッセージ要素TIMMsgElement

### テキストメッセージ要素

```
{
    "MsgType": "TIMTextElem",
    "MsgContent": {
        "Text": "hello world"
    }
}
```

| フィールド | タイプ | 説明 |
|---------|---------|---------|
| Text | String | メッセージ内容。受信者がiOSまたはAndroidのバックグラウンドでオンラインの場合、オフラインプッシュのテキストとして表示されます。 |

受信者がiOSまたはAndroidで、アプリケーションがバックグラウンドにある場合、JSONリクエストパケットのTextフィールドは、オフラインプッシュのテキストとして表示されます。

### 地理的位置メッセージ要素

```
{
    "MsgType": "TIMLocationElem", 
    "MsgContent": {
        "Desc": "someinfo", 
        "Latitude": 29.340656774469956, 
        "Longitude": 116.77497920478824
    }
}
```

| フィールド | タイプ | 説明 |
|---------|---------|---------|
| Desc | String | 地理的位置の説明情報。 |
|Latitude|Number|緯度。|
|Longitude|Number|経度。|

受信者がiOSまたはAndroidで、アプリケーションがバックグラウンドにある場合、中国語版のオフラインプッシュテキストは「[位置]となり、英語版のオフラインプッシュテキストは「[Location]」となります。

### 顔絵文字メッセージ要素

```
{
    "MsgType": "TIMFaceElem", 
    "MsgContent": {
        "Index": 1, 
        "Data": "content"
    }
}
```

| フィールド | タイプ | 説明 |
|---------|---------|---------|
| Index | Number | 顔絵文字インデックス、ユーザーカスタマイズ。 |
|Data|String|追加データ。|

受信者がiOSまたはAndroidで、アプリケーションがバックグラウンドにある場合、中国語版のオフラインプッシュテキストは「[表情]となり、英語版のオフラインプッシュテキストは「[Face]」となります。


<dx-alert infotype="explain" title="説明">
メッセージにTIMCustomElemカスタムメッセージ要素が1つしかない場合、DescフィールドとOfflinePushInfo.Descフィールドが入力されていないと、メッセージのオフラインプッシュを受信できません。このメッセージのオフラインプッシュを受信するには、OfflinePushInfo.Descフィールドに入力する必要があります。
</dx-alert>


### カスタムメッセージ要素

```
{
    "MsgType": "TIMCustomElem", 
    "MsgContent": {
        "Data": "message", 
        "Desc": "notification", 
        "Ext": "url", 
        "Sound": "dingdong.aiff"
    }
}
```

| フィールド | タイプ | 説明 |
|---------|---------|---------|
| Data | String | カスタムメッセージデータ。APNsのpayloadフィールドとして発行されないため、payloadからDataフィールドを取得できません。|
|Desc|String|カスタムメッセージの説明情報。受信者がiOSまたはAndroidのバックグラウンドでオンラインの場合、オフラインプッシュテキストを表示します。<br>カスタムメッセージの送信中に[OfflinePushInfo.Desc](https://intl.cloud.tencent.com/document/product/1047/33527)フィールドが同時に設定されている場合、このフィールドは上書きされますので、OfflinePushInfo.Descフィールドを優先的に入力してください。<br><dx-alert infotype="explain" title="说明">
メッセージにTIMCustomElemカスタムメッセージ要素が1つしかない場合、DescフィールドとOfflinePushInfo.Descフィールドが入力されていないと、メッセージのオフラインプッシュを受信できません。このメッセージのオフラインプッシュを受信するには、OfflinePushInfo.Descフィールドに入力する必要があります。
</dx-alert>|
|Ext|String|拡張フィールド。受信者がiOSシステムで、アプリケーションがバックグラウンドにある場合、このフィールドはAPNリクエストパケットPayloadsのExtキー値として発行されます。Extのプロトコル形式は業務側が決定し、APNsは透過的な送信のみを行います。|
|Sound|String|APNsのプッシュリングトーンをカスタマイズします。|

受信者がiOSシステムで、アプリケーションがバックグラウンドにある場合、Descはプッシュテキストとして使用され、ExtフィールドはAPNSリクエストパケットPayloadsのextキー値として発行され、DataフィールドはAPNsのPayloadsフィールドとして発行されません。結合されたメッセージには、TIMCustomElemカスタムメッセージ要素を1つしか含めることができないので、ご注意ください。

### 音声メッセージ要素

>!サーバーに統合されたRest APIインターフェースを介して音声メッセージを送信する場合、必ず音声のUrl、UUID、Download_Flagフィールドに入力してください。対応する音声がUrl経由でダウンロードできることを確認する必要があります。UUIDフィールドは、グローバルに一意のString値を入力する必要があり、通常、音声ファイルのMD5値を入力します。メッセージ受信者はV2TIMSoundElem.getUUID()を介して設定されたUUIDフィールドを取得できます。ビジネスAppはこのフィールドを使用することで音声を区別できます。Download_Flagフィールドには、必ず2を入力してください。

4.Xおよびそれ以降のバージョンIM SDK（Android、iOS、Mac 以及 Windows）によって送信される音声メッセージ要素の形式は次のとおりです：
```
{
    "MsgType": "TIMSoundElem",
    "MsgContent": {
        "Url": "https://1234-5678187359-1253735226.cos.ap-shanghai.myqcloud.com/abc123/c9be9d32c05bfb77b3edafa4312c6c7d",
        "UUID": "1053D4B3D61040894AC3DE44CDF28B3EC7EB7C0F",
        "Size": 62351,
        "Second": 1,
        "Download_Flag": 2
    }
}
```

| フィールド | タイプ | 説明 |
|---------|---------|---------|
| Url | String | 音声ダウンロードアドレス。対応する音声は、このURLアドレスから直接ダウンロードできます。 |
| UUID | String | 音声の一意の識別子。クライアントが音声にインデックスを付けるために用いるキー値。 |
| Size | Number | 音声データサイズ。単位：バイト。 |
| Second | Number | 音声の長さ。単位：秒。 |
| Download_Flag | Number | 音声ダウンロード方法のフラグ。現在、Download_Flagの値は2のみです。これは、`Url`フィールド値のURLアドレスを介して音声を直接ダウンロードできることを意味します。 |

>?2.Xおよび3.XバージョンのIM SDK（Android、iOS、MacおよびWindows）によって送信される音声メッセージ要素は次のとおりです：
```
{
    "MsgType": "TIMSoundElem",
    "MsgContent": {
        "UUID": "305c0201"、//音声の一意の識別子。タイプはStringです。クライアントが音声にインデックスを付けるために用いるキー値です。このフィールドからは、対応する音声をダウンロードできません。音声を取得する必要がある場合は、IM SDKバージョンを4.Xにアップグレードしてください。
        "Size": 62351,      //音声データサイズ、タイプはNumber、単位：バイト。
        "Second": 1         //音声の長さ、タイプはNumber。単位：秒。
    }
}
```


### 画像メッセージ要素

>!サーバー側に統合されたRest APIインターフェースを介して画像メッセージを送信する場合、URL、UUID、幅、高さなどの、画像のフィールドに入力する必要があります。対応する画像がURLからダウンロードできることを確認する必要があります。それにより、[画像基本情報の取得](https://intl.cloud.tencent.com/document/product/1045/33722)および[画像処理](https://intl.cloud.tencent.com/document/product/1045/33726)ができるようになります。WidthとHeightは、それぞれ画像の幅と高さ（ピクセル単位）です。UUIDフィールドには、グローバルに一意の文字列値（通常は画像のMD5値）を入力する必要があります。メッセージ受信者は、V2TIMImageElem.getImageList()を呼び出してV2TIMImageオブジェクトを取得し、次にV2TIMImage.getUUID()を呼び出して設定されたUUIDフィールドを取得することで、業務Appはこのフィールドを使用して画像を区別できます。

```
{
    "MsgType": "TIMImageElem",
    "MsgContent": {
        "UUID": "1853095_D61040894AC3DE44CDFFFB3EC7EB720F",
        "ImageFormat": 1,
        "ImageInfoArray": [
            {
                "Type": 1,           //元の画像
                "Size": 1853095,
                "Width": 2448,
                "Height": 3264,
                "URL": "http://xxx/3200490432214177468_144115198371610486_D61040894AC3DE44CDFFFB3EC7EB720F/0"
            },
            {
                "Type": 2,      //大きな画像
                "Size": 2565240,
                "Width": 0,
                "Height": 0,
                "URL": "http://xxx/3200490432214177468_144115198371610486_D61040894AC3DE44CDFFFB3EC7EB720F/720"
            },
            {
                "Type": 3,   //サムネイル
                "Size": 12535,
                "Width": 0,
                "Height": 0,
                "URL": "http://xxx/3200490432214177468_144115198371610486_D61040894AC3DE44CDFFFB3EC7EB720F/198"
            }
        ]
    }
}
```

| フィールド | タイプ | 説明 |
|---------|---------|---------|
| UUID | String | 画像の一意の識別子。クライアントが画像にインデックスを付けるために用いるキー値。 |
| ImageFormat | Number | 画像形式。JPG = 1、GIF = 2、PNG = 3、BMP = 4、その他 = 255。 |
| ImageInfoArray | Array | 元の画像、サムネイル、または大きな画像のダウンロード情報。 |
| Type | Number | 画像タイプ：1-元の画像、2-大きな画像、3-サムネイル。 |
| Size | Number | 画像データサイズ。単位：バイト。 |
| Width | Number | 画像幅。単位はピクセル。 |
| Height | Number | 画像高さ。単位はピクセル。 |
| URL | String | 画像のダウンロードアドレス。 |

### ファイルメッセージ要素

>!サーバーに統合されたRest APIインターフェースを介してファイルメッセージを送信する場合、ファイルのUrl、UUID、Download_Flagフィールドに入力し、対応するファイルがこのUrl経由でダウンロードできることを確認する必要があります。UUIDフィールドは、グローバルに一意のString値を入力する必要があり、通常、ファイルのMD5値を入力します。メッセージ受信者はV2TIMFileElem.getUUID()を呼び出すことで設定されたUUIDフィールドを取得できます。ビジネスAppはこのフィールドを使用することでファイルを区別できます。Download_Flagフィールドには、必ず2を入力してください。

4.Xおよびそれ以降のバージョンIM SDK（Android、iOS、Mac 以及 Windows）によって送信されるファイルメッセージ要素の形式は次のとおりです：
```
{
    "MsgType": "TIMFileElem",
    "MsgContent": {
        "Url": "https://7492-5678539059-1253735326.cos.ap-shanghai.myqcloud.com/abc123/49be9d32c0fbfba7b31dafa4312c6c7d",
        "UUID": "1053D4B3D61040894AC3DE44CDF28B3EC7EB7C0F",
        "FileSize": 1773552,
        "FileName": "file:///private/var/Application/tmp/trim.B75D5F9B-1426-4913-8845-90DD46797FCD.MOV",
		"Download_Flag": 2
    }
}
```

| フィールド | タイプ | 説明 |
|---------|---------|---------|
| Url | String | ファイルのダウンロードアドレス。対応するファイルは、このURLアドレスから直接ダウンロードできます。 |
| UUID | String | ファイルの一意の識別子。クライアントがファイルにインデックスを付けるために用いるキー値。 |
| FileSize | Number | ファイルデータサイズ。単位：バイト。 |
| FileName | String | ファイル名。 |
| Download_Flag | Number | ファイルダウンロード方法のフラグ。現在、Download_Flagの値は2のみです。これは、`Url`フィールドの値のURLアドレスを介してファイルを直接ダウンロードできることを意味します。 |

>?2.Xおよび3.XバージョンのIM SDK（Android、iOS、MacおよびWindows）によって送信されるファイルメッセージ要素は次のとおりです：
>```
{
    "MsgType": "TIMFileElem",
    "MsgContent": {
        "UUID": "305c02010", //ファイルの一意の識別子。タイプはStringです。クライアントがファイルにインデックスを付けるために用いるキー値です。このフィールドからは、対応するファイルをダウンロードできません。このファイルを取得する必要がある場合は、IM SDKバージョンを4.Xにアップグレードしてください。
        "FileSize": 1773552,//ファイルデータサイズ。タイプはNumber、単位はバイトです。
        "FileName": "file:///private/var/Application/tmp/trim.B75D5F9B-1426-4913-8845-90DD46797FCD.MOV" //ファイル名。タイプはStringです。
    }
}
```

### ビデオメッセージ要素

>!サーバーに統合されたRestAPIインターフェースを介してビデオメッセージを送信する場合、必ずVideoUrl、VideoUUID、ThumbUrl、ThumbUUID、ThumbWidth、ThumbHeight、VideoDownloadFlagおよびThumbDownloadFlagフィールドに入力してください。対応するビデオがVideoUrlを介してダウンロードできること、および対応するビデオサムネイルがThumbUrlを介してダウンロードできることを確認する必要があります。VideoUUIDとThumbUUIDフィールドには、グローバルに一意のString値を入力する必要があります。通常、対応するビデオとビデオサムネイルのMD5値を入力します。メッセージ受信者は、V2TIMVideoElem.getVideoUUID()とV2TIMVideoElem.getSnapshotUUID()をそれぞれ呼び出すことで、設定されたUUIDフィールドを取得できます。ビジネスAppは、このフィールドを使用することでビデオを区別できます。VideoDownloadFlagとThumbDownloadFlagフィールドには、必ず2を入力してください。

4.Xおよびそれ以降のバージョンIM SDK（Android、iOS、Mac 以及 Windows）によって送信されるビデオメッセージ要素の形式は次のとおりです：
```
{
    "MsgType": "TIMVideoFileElem",
    "MsgContent": {
        "VideoUrl": "https://0345-1400187352-1256635546.cos.ap-shanghai.myqcloud.com/abcd/f7c6ad3c50af7d83e23efe0a208b90c9",
        "VideoUUID": "5da38ba89d6521011e1f6f3fd6692e35",
        "VideoSize": 1194603,
        "VideoSecond": 5,
		"VideoFormat": "mp4",
		"VideoDownloadFlag":2,
		"ThumbUrl": "https://0345-1400187352-1256635546.cos.ap-shanghai.myqcloud.com/abcd/a6c170c9c599280cb06e0523d7a1f37b",
		"ThumbUUID": "6edaffedef5150684510cf97957b7bc8",
		"ThumbSize": 13907,
		"ThumbWidth": 720,
		"ThumbHeight": 1280,
		"ThumbFormat": "JPG",
		"ThumbDownloadFlag":2
    }
}
```

| フィールド | タイプ | 説明 |
|---------|---------|---------|
| VideoUrl | String | ビデオダウンロードアドレス。対応するビデオは、このURLアドレスから直接ダウンロードできます。 |
| VideoUUID | String | ビデオの一意の識別子、クライアントがビデオにインデックスを付けるために用いるキー値。 |
| VideoSize | Number | ビデオデータサイズ。単位：バイト。 |
| VideoSecond | Number | ビデオ時間。単位：秒。Web端末は、ビデオ時間の取得をサポートしません。値は0です。|
| VideoFormat | String | mp4などのビデオ形式。 |
| VideoDownloadFlag | Number | ビデオダウンロード方法のフラグ。現在、`VideoDownloadFlagの値は2のみです。これは、``VideoUrl`フィールドの値のURLアドレスを介してビデオを直接ダウンロードできることを意味します。 |
| ThumbUrl | String | ビデオサムネイルアドレス。対応するビデオサムネイルは、このURLアドレスから直接ダウンロードできます。 |
| ThumbUUID | String | ビデオサムネイルの一意の識別子。クライアントがビデオサムネイルにインデックスを付けるために用いるキー値。 |
| ThumbSize | Number | サムネイルサイズ。単位：バイト。 |
| ThumbWidth | Number |サムネイルの幅。単位はピクセル。 |
| ThumbHeight | Number | サムネイルの高さ。単位はピクセル。 |
| ThumbFormat | String | JPG、BMPなどのサムネイル形式。 |
| ThumbDownloadFlag | Number | ビデオサムネイルダウンロード方法のフラグ。現在、`ThumbDownloadFlagの値は2のみです。これは、``ThumbUrl`フィールド値のURLアドレスを介してビデオサムネイルを直接ダウンロードできることを意味します。 |


>?2.Xおよび3.XバージョンのIM SDK（Android、iOS、MacおよびWindows）によって送信されるビデオメッセージ要素は次のとおりです：
>```
{
    "MsgType": "TIMVideoFileElem",
    "MsgContent": {
        "VideoUUID": "1400123456_dramon_34ca36be7dd214dc50a49238ef80a6b5"、//ビデオの一意の識別子。タイプはStringです。クライアントがビデオにインデックスを付けるために用いるキー値です。このフィールドからは、対応するビデオをダウンロードできません。このビデオを取得する必要がある場合は、IM SDKバージョンを4.Xにアップグレードしてください。
        "VideoSize": 1194603,//ビデオデータサイズ。タイプはNumber。単位：バイト。
        "VideoSecond": 5,//ビデオの長さ。タイプはNumber。単位：秒。
		"VideoFormat": "mp4",//ビデオ形式。タイプはmp4などのStringです。
		"ThumbUUID": "1400123456_dramon_893f5a7a4872676ae142c08acd49c18a"、//ビデオサムネイルの一意の識別子。タイプはStringです。クライアントがビデオサムネイルにインデックスを付けるために用いるキー値です。このフィールドからは、対応するビデオサムネイルをダウンロードできません。このビデオサムネイルを取得する必要がある場合は、IM SDKバージョンを4.Xにアップグレードしてください。
		"ThumbSize": 13907,//サムネイルサイズ。タイプは数値。単位：バイト。
		"ThumbWidth": 720,//サムネイルの幅。 タイプはNumberです。
		"ThumbHeight": 1280,//サムネイルの高さ。タイプはNumberです。
		"ThumbFormat": "JPG"  //サムネイル形式。タイプはJPG、BMPなどのStringです。
    }
}
```

### マージ転送メッセージの要素
>!端末5.2.210およびそれ以降のバージョン。web 2.10.1およびそれ以降のバージョンのみ、マージ転送メッセージの送受信をサポートします。

```json
{
  "MsgType": "TIMRelayElem",
  "MsgContent": {
    "Title": "グループチャットの記録",
    "MsgNum": 2,
    "CompatibleText": "このSDKバージョンはマージ転送メッセージをサポートしていません。新しいバージョンにアップグレードしてください。",
    "AbstractList": [
      "A:これについて、みなさんはどう思いますか？",
      "B:とても良いと思います"
    ],
    "MsgList": [
      {
        "From_Account": "A",
        "GroupId": "group1",
        "MsgSeq": 85,
        "MsgRandom": 3998651049,
        "MsgTimeStamp": 1664437702,
        "MsgBody": [
          {
            "MsgContent": {
              "Text": "これについて、みなさんはどう思いますか？"
            },
            "MsgType": "TIMTextElem"
          }
        ]
      },
      {
        "From_Account": "B",
        "GroupId": "group1",
        "MsgSeq": 86,
        "MsgRandom": 965790,
        "MsgTimeStamp": 1664437703,
        "MsgBody": [
          {
            "MsgContent": {
              "Text": "とても良いと思います"
            },
            "MsgType": "TIMTextElem"
          }
        ]
      }
    ]
  }
}
```

| フィールド | タイプ | 説明 |
|---------|---------|---------|
| Title | String | マージ転送メッセージのタイトル。|
| MsgNum | Integer | 転送されたメッセージの数。|
| CompatibleText | String | 互換性のあるテキスト。マージ転送メッセージをサポートしていない古いバージョンのSDKがそのようなメッセージを受信すると、IMバックグラウンドはこのメッセージを送信する前に互換性のあるテキストに変換します。|
| AbstractList | Array | マージされたメッセージのダイジェストリスト。Stringの配列です。|
| MsgList | Array | メッセージリスト。このフィールドは、転送されたメッセージの長さの合計が12KB以下の場合にのみ表示され、現時点ではJsonMsgKeyフィールドはありません。|
| JsonMsgKey | String | マージ転送されたメッセージリストKey。このフィールドは、転送されたメッセージの長さの合計が12KBよりも大きい場合にのみ表示され、現時点ではJsonMsgKeyフィールドはありません。|

MsgList内の各メッセージの構造は次のとおりです：

| フィールド | タイプ | 説明 |
|---------|---------|---------|
| From_Account | String | メッセージ送信側UserID。このフィールドは、転送されたメッセージがシングルチャットまたはグループチャットの場合に表示されます。|
| To_Account | String | メッセージ受信側UserID。このフィールドは、転送されたメッセージがシングルチャットの場合にのみ表示されます。|
| GroupId | String | グループID。このフィールドは、転送されたメッセージがグループチャットの場合にのみ表示されます。|
| MsgSeq | Integer | メッセージのシーケンス番号（32ビットの符号なし整数）。|
| MsgRandom | Integer | メッセージ乱数（32ビットの符号なし整数）。|
| MsgTimeStamp | Integer | メッセージの秒レベルのタイムスタンプ。|
| MsgBody | Array | メッセージ内容。具体的な形式については、[メッセージ形式の説明](https://intl.cloud.tencent.com/document/product/1047/33527)をご参照ください（注：1つのメッセージには複数のメッセージ要素を含めることができます。MsgBodyはArrayタイプです）。  |
| CloudCustomData | String | メッセージカスタムデータ（クラウドに保存され、反対側に送信され、プログラムをアンインストールして再インストールした後にプルできます）。|

## MsgBodyメッセージ内容インスタンス

### シングルテキスト要素メッセージ

1つのメッセージに含まれる中国語のテキストメッセージ要素は1つだけで、テキストの内容はhello worldです。

```json
{
    "MsgBody": [
        {
            "MsgType": "TIMTextElem", 
            "MsgContent": {
                "Text": "hello world"
            }
        }
    ]
}
```

### 結合されたメッセージ

次のシングルメッセージには、2つのテキストメッセージ要素と1つの顔絵文字要素が含まれています。メッセージ要素の順序は、テキスト+顔絵文字+テキストです。
```json
{
    "MsgBody": [
        {
            "MsgType": "TIMTextElem", 
            "MsgContent": {
                "Text": "hello"
            }
        }, 
        {
            "MsgType": "TIMFaceElem", 
            "MsgContent": {
                "Index": 1, 
                "Data": "content"
            }
        }, 
        {
            "MsgType": "TIMTextElem", 
            "MsgContent": {
                "Text": "world"
            }
        }
    ]
}
```

>!結合されたメッセージは1つのTIMCustomElemカスタムメッセージ要素のみを持つことができ、他のメッセージ要素の数は無制限です。

##  メッセージカスタムデータCloudCustomDataの説明
各メッセージは、カスタムデータCloudCustomDataを持つことができます。

CloudCustomDataは、メッセージのMsgBodyと一緒にクラウドに保存され、CloudCustomDataは対する相手側に送信されます。これは、プログラムをアンインストールして再インストールした後に取得できます。

CloudCustomDataとMsgBodyの形式の例は次のとおりです：
```json
{
    "MsgBody": [
        {
            "MsgType": "TIMTextElem", 
            "MsgContent": {
                "Text": "hello"
            }
        }
    ],
    "CloudCustomData": "your cloud custom data"
}
```

## Apple Push Notification Service(APNs)関連の説明
### クライアントプッシュ表示形式の説明
- **アカウントのニックネームは設定されていません**
アカウントにニックネームがない場合、APNsプッシュはプッシュテキスト内容のみを表示します。シングルチャットメッセージは「プッシュテキスト」のみを表示し、グループメッセージは「（グループ名）：プッシュテキスト」を表示します。
![](https://main.qcloudimg.com/raw/7bdb0f41aaa943190ce949fea8d20095.png)

- **アカウントのニックネームが設定されています**
アカウントにニックネームが設定されている場合、シングルチャットメッセージの表示形式は「ニックネーム：プッシュテキス内容」、グループメッセージの表示形式はニックネーム（グループ名）：プッシュテキスト内容になります。
![](https://main.qcloudimg.com/raw/7bdb0f41aaa943190ce949fea8d20095.png)

- **結合されたメッセージ表示形式**
結合されたメッセージの場合、各メッセージ要素のプッシュテキストが表示テキストとして順番に重ねられます。 以下は、アカウントのニックネームが設定されたシングルチャットメッセージであり、プッシュテキストは「helloworld」です。helloworldにはスペースがなく、バックグラウンドが順番に重ね合わされ、各メッセージ要素のプッシュテキストの間にいかなる文字も追加されないことにご注意ください。それぞれの異なるメッセージ要素の間にスペースやその他の文字を追加する必要がある場合は、呼び出し元がそれを制御する必要があります。
```json
{
    "MsgBody": [
        {
            "MsgType": "TIMTextElem", 
            "MsgContent": {
                "Text": "hello"  
            }
        },
        {
            "MsgType": "TIMCustomElem",
            "MsgContent": {
                "Data": "message",
                "Desc": "world",
                "Ext": "https://www.example.com",               
                "Sound": "dingdong.aiff"
            }
        }
    ] 
}
```
各タイプのメッセージ要素のテキストフィールドの概要をプッシュします。

| MsgTypeの値 | タイプ |メッセージ要素プッシュテキスト|
|---------|---------|---------|
| TIMTextElem | テキストメッセージ。|Textフィールド。|
|TIMLocationElem|地理的位置メッセージ。|中国語版オフラインプッシュテキストは「[位置]」、英語版は「[Location]」です。|
|TIMFaceElem|顔絵文字メッセージ。|中国語版オフラインプッシュテキストは「[表情]」、英語版は「[Face]」です。|
|TIMCustomElem|カスタムメッセージ。|Descフィールド。|

### ニックネームとグループ名REST API設定インターフェース
アカウントのニックネームを設定するREST APIインターフェース：[プロファイルの設定](https://intl.cloud.tencent.com/document/product/1047/34916)。
グループ名を設定するREST APIインターフェース：[グループの基本プロファイルの変更](https://intl.cloud.tencent.com/document/product/1047/34962)。

## 高度なアプリケーション
#### カスタムプッシュサウンド。APNsは拡張フィールドを発行します。
カスタムメッセージ要素TIMCustomElemを使用して、Soundはカスタムサウンドファイルの名前を入力し、Extは発行された拡張フィールドを入力します。リクエスト拡張フィールドは、APNsからプッシュされたPayLoadのExtフィールドから取得できます。
```
{
    "To_Account": "lumotuwe5", 
    "MsgRandom": 121212, 
    "MsgBody": [
        {
            "MsgType": "TIMCustomElem", 
            "MsgContent": {
                "Data": "other information", 
                "Desc": "hello", 
                "Ext": "www.qq.com", 
                "Sound": "dingdong.aiff"
            }
        }, 
        {
            "MsgType": "TIMTextElem", 
            "MsgContent": {
                "Text": "world"
            }
        }
    ]
}

```

クライアントはAPNsを受信し、JSON Payloadを次のようにプッシュします：

```
{
    "aps": {
        "alert": "Nickname:helloworld"、//各メッセージ要素のプッシュテキストシーケンスが重ねられます
        "badge": 5,                       
        "sound": "dingdong.aiff"         //TIMCustomElemのSoundフィールドに対応します
    }, 
    "ext": "www.qq.com"                //TIMCustomElemのExtフィールドに対応します
}

```

## オフラインプッシュOfflinePushInfoの説明

OffsetPushInfoは、オフラインプッシュを設定するためのJSONオブジェクトです。このメッセージがプッシュをオフにするか、テキストの説明内容をプッシュするか、透過的な文字列をプッシュするかなどを設定できます。OfflinePushInfo情報を使用してオフラインプッシュ情報を手軽に設定でき、TIMCustomElemパッケージを介して実装する必要はありません。

>!OfflinePushInfoが入力されている場合、TIMCustomElemのオフラインプッシュに関する情報の設定は無視されます。 現在、OfflinePushInfoは、APNsプッシュおよびAndroidメーカープッシュ（Xiaomi、Huawei、Meizu、OPPO、およびvivoプッシュ）に適しています。

OffsetPushInfoの形式の例は次のとおりです：

```
{
    // ...
    "MsgBody": [...] // これはMsgBodyに関する説明です
    "OfflinePushInfo": {
        "PushFlag": 0,
        "Title":"これはプッシュタイトルです"
        "Desc": "これはオフラインプッシュ内容です"
        "Ext": "これは透過的なコンテンツです"
        "AndroidInfo": { 
			"Sound": "android.mp3",
			"OPPOChannelID": "test_OPPO_channel_id",
			"VIVOClassification": 1
        },
        "ApnsInfo": {
            "Sound": "apns.mp3",
            "BadgeMode": 1,
            "Title":"apns title",
            "SubTitle":"apns subtitle",
            "Image":"www.image.com",
            "MutableContent": 1
        }
    }
}
```

フィールドの説明は次のとおりです：

| フィールド | タイプ | 属性 | 	説明 |
|---------|---------|---------|---------|
| PushFlag | Integer | オプション | 「0」はプッシュを表し、「1」はオフラインプッシュでないことを表します。  |
| Title | String | オプション | オフラインプッシュタイトル。このフィールドはiOSとAndroidで共有されています。|
| Desc | String | オプション | オフラインプッシュ内容。このフィールドは、上記のさまざまなメッセージ要素[TIMMsgElement](https://intl.cloud.tencent.com/document/product/1047/33527#.E6.B6.88.E6.81.AF.E5.85.83.E7.B4.A0-timmsgelement)のオフラインプッシュ表示テキストをカバーします。<br>送信されるメッセージに[TIMCustomElem](https://intl.cloud.tencent.com/document/product/1047/33527#.E8.87.AA.E5.AE.9A.E4.B9.89.E6.B6.88.E6.81.AF.E5.85.83.E7.B4.A0)カスタムメッセージ要素が1つしかない場合、このDescフィールドはTIMCustomElemのDescフィールドを上書きします。Descフィールドの両方ともに入力されていない場合、カスタムメッセージのオフラインプッシュは受信できません。|
| Ext | String | オプション | オフラインプッシュ透過的コンテンツ。国内のAndroidスマホメーカーごとにプッシュプラットフォームの要件が異なるため、このフィールドがJSON形式であることを確認してください。JSON形式でない場合、一部のベンダーからオフラインプッシュを受信できなくなる可能性があります。 |
| AndroidInfo.Sound | String | オプション | Androidオフラインプッシュ音声ファイルパス。 |
| AndroidInfo.HuaWeiChannelID | String | オプション | HuaweiスマホEMUI 10.0以降の通知チャネルフィールド。 このフィールドがブランクでない場合、コンソールによって設定されたChannelID値は上書きされます。このフィールドが空の場合、コンソールによって設定されたChannelID値は上書きされません。|
| AndroidInfo.XiaoMiChannelID | String | オプション | XiaomiスマホMIUI 10以降の通知カテゴリ(Channel)適合フィールド。 このフィールドがブランクでない場合、コンソールによって構成されたChannelID値は上書きされます。このフィールドがブランクの場合、コンソールによって構成されたChannelID値は上書きされません。 |
| AndroidInfo.OPPOChannelID | String | オプション | OPPOスマホAndroid 8.0以降のNotificationChannel通知適合フィールド。このフィールドがブランクでない場合、コンソールによって設定されたChannelID値は上書きされます。このフィールドがブランクの場合、コンソールによって設定されたChannelID値は上書きされません。|
| AndroidInfo.GoogleChannelID | String | オプション | GoogleスマホAndroid 8.0以降の通知チャネルフィールド。Googleプッシュの新しいインターフェース（アップロード証明書ファイル）はchannel idをサポートし、古いインターフェース（サーバーキーの入力）はサポートしません。 |
| AndroidInfo.VIVOClassification | Integer | オプション | VIVOスマホプッシュメッセージの分類。「0」は運用メッセージを表し、「1」はシステムメッセージを表します。入力されていない場合、デフォルトで「1」になります。|
| AndroidInfo.HuaWeiImportance | String | オプション | Huaweiプッシュ通知メッセージの分類。値はLOW、NORMALであり、入力されていない場合のデフォルト値はNORMALです。|
| AndroidInfo.ExtAsHuaweiIntentParam | Integer | オプション | コンソールでHuaweiプッシュを「アプリで指定されたページを開く」ように設定することを前提として、「1」が渡された場合、透過的コンテンツExtがIntentのパラメータとして使用されることを表し、「0」は透過的コンテンツExtがActionパラメータとして使用されることを表します。入力されていない場合、デフォルト値は0です。渡される2つのパラメータの違いについては、[Huaweiプッシュドキュメント](https://developer.huawei.com/consumer/cn/doc/development/HMSCore-Guides/andorid-basic-clickaction-0000001087554076#section20203190121410)をご参照ください。|
| AndroidInfo.HuaWeiCategory | String | オプション | Huaweiスマホでメッセージのタイプを識別するために使用されます。このフィールドがブランクでない場合、コンソールによって設定されたcategory値は上書きされます。このフィールドが空の場合、コンソールによって設定されたcategory値は上書きされません。|詳細については[category説明](https://developer.huawei.com/consumer/cn/doc/development/HMSCore-References/https-send-api-0000001050986197#section13271045101216)ご参照ください。|
| ApnsInfo.BadgeMode | Integer | オプション | このフィールドをデフォルトのままにするか、「0」に設定すると、メッセージをカウントする必要があることを表し、「1」に設定すると、このメッセージをカウントする必要がないことを表します。この場合、右上隅のアイコンの数字は増加しません。|
| ApnsInfo.Title|String|オプション|このフィールドは、APNsによってプッシュされたタイトルを識別するために用いられます。入力すると、最上位階層のTitleが上書きされます。|
| ApnsInfo.SubTitle|String|オプション|このフィールドは、APNsによってプッシュされたサブタイトルを識別するために用いられます。|
| ApnsInfo.Image|String|オプション|このフィールドは、APNsが持つ画像アドレスを識別するために用いられます。クライアントがこのフィールドを取得すると、画像リソースをダウンロードすることにより、ポップアップウィンドウに画像を表示することができます。|
| ApnsInfo.MutableContent | Integer | オプション | 「1」は、iOS 10のプッシュ拡張のオンを表します。デフォルトは「0」です。|

>!APNsプッシュはデータパケットサイズを4Kを超えないよう制限するので、他の制御フィールドを削除し、DescフィールドとExtフィールドの合計が3Kを超えないようにすることをお勧めします。

## 参考

Apple Push Notification Service(APNs) [Appleプッシュ開発ドキュメント](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/Introduction.html#//apple_ref/doc/uid/TP40008194-CH1-SW1)。
iOSオフラインメッセージプッシュの設定：[オフラインプッシュ(iOS)](https://www.tencentcloud.com/document/product/1047/34347)。
