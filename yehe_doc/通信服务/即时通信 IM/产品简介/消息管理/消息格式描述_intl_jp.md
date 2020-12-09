## メッセージ内容MsgBodyの説明
MsgBodyに入力されたフィールドはメッセージの内容です。インスタントメッセージIMは、1つのメッセージにテキストメッセージ要素と表情メッセージ要素の両方を含むなど、複数のメッセージ要素のタイプを含むことをサポートします。したがって、MsgBodyはArray型として定義され、必要に応じて複数のタイプのメッセージ要素を追加できます。メッセージ要素名はTIMMsgElementです。メッセージ要素TIMMsgElementからなるMsgBodyの例については、[メッセージ内容MsgBodyインスタンス](https://intl.cloud.tencent.com/document/product/1047/33527)をご参照ください。

メッセージ要素TIMMsgElementのフォーマットは、次のように統一します。
```
{
    "MsgType": "",
    "MsgContent": {}
}
```

| フィールド | タイプ | 説明 |
|---------|---------|---------|
| MsgType | String | メッセージ要素のタイプ。現在サポートされているメッセージオブジェクトは、TIMTextElem（テキストメッセージ）、TIMLocationElem（位置メッセージ）、TIMFaceElem（絵文字メッセージ）、TIMCustomElem（カスタムメッセージ）、TIMSoundElem（音声メッセージ）、TIMImageElem（画像メッセージ）、TIMFileElem（ファイルメッセージ）、TIMVideoFileElem（動画メッセージ）です。|
|MsgContent|Object|メッセージ要素の内容。MsgTypeによってMsgContentフォーマットが異なります。具体的には以下をご参照ください。|

現在サポートされているメッセージタイプMsgTypeを次の表に示します。

| MsgTypeの値 | タイプ |
|---------|---------|
| TIMTextElem | テキストメッセージ。|
|TIMLocationElem|地理位置メッセージ。|
|TIMFaceElem|絵文字メッセージ。|
|TIMCustomElem|カスタムメッセージ。受信者がiOSシステムであり、アプリがバックグラウンドになる場合、このメッセージタイプはテキスト以外のフィールドをAPNsに組み入れます。1つの組み合わせメッセージには1つのTIMCustomElemカスタムメッセージ要素だけを含めることができます。|
|TIMSoundElem|音声メッセージ。（サービス側に統合されたRest APIは、このようなメッセージの送信をサポートしていません）。
|TIMImageElem|画像メッセージ。（サービス側に統合されたRest APIは、このようなメッセージの送信をサポートしていません）。
|TIMFileElem|ファイルメッセージ。（サービス側に統合されたRest APIは、このようなメッセージの送信をサポートしていません）。
|TIMVideoFileElem|動画メッセージ。（サービス側に統合されたRest APIは、このようなメッセージの送信をサポートしていません）。

>!サービス側に統合されたRest APIインターフェースを介して送信できるのは、TIMTextElem、TIMLocationElem、TIMFaceElem、TIMCustomElemタイプのメッセージのみです。その他のタイプのメッセージ（TIMSoundElem、TIMImageElem、TIMFileElem、TIMVideoFileElem）は、Rest APIインターフェースを介して送信できません。

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
| Text | String | メッセージ内容。受信者がiOSまたはAndroidのバックグラウンドでオンラインになる場合、オフラインでプッシュされたテキストとして表示されます。|

受信者がiOSまたはAndroidであり、かつアプリがバックグラウンドになる場合、JSON要求パッケージボディ内のTextフィールドはオフラインでプッシュされたテキストとして表示されます。

### 地理位置メッセージ要素

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
| Desc | String | 地理位置説明情報。|
|Latitude|Number|緯度。|
|Longitude|Number|経度。|

受信者がiOSまたはAndroidであり、かつアプリがバックグラウンドになる場合、オフラインでプッシュされたテキストは中国語版の場合、「[位置]」、英語版の場合、「[Location]」になります。

### 絵文字メッセージ要素

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
| Index | Number | ユーザ定義の絵文字索引。|
|Data|String|追加データ。|

受信者がiOSまたはAndroidであり、かつアプリがバックグラウンドになる場合、オフラインでプッシュされたテキストは中国語版の場合、「[表情（絵文字）]」、英語版の場合、「[Face]」になります。

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
| Data | String | カスタムメッセージデータ。APNsのpayloadフィールドとして送信されないため、payloadからDataフィールドを取得できません。|
|Desc|String|カスタムメッセージの説明情報。受信者がiOSまたはAndroidのバックグラウンドでオンラインになる場合、オフラインでプッシュされたテキストとして表示されます。<br>カスタムメッセージを送信する同時に[OfflinePushInfo.Desc](https://intl.cloud.tencent.com/document/product/1047/33527)フィールドが設定されている場合、このフィールドは上書きされます。OfflinePushInfo.Descフィールドを優先して入力してください。<br>メッセージにTIMCustomElemカスタムメッセージ要素が1つしかない場合、DescフィールドとOfflinePushInfo.Descフィールドの両方が入力されていないと、そのメッセージのオフラインプッシュは受信されません。このメッセージのオフラインプッシュを受信するために、OfflinePushInfo.Descフィールドを入力する必要があります。|
|Ext|String|拡張フィールド。受信者がiOSシステムであり、かつアプリがバックグラウンドになる場合、このフィールドはAPNs要求パケットPayloads内のExtキー値として送信され、Extのプロトコルフォーマットはサービス側によって決定され、APNsはパススルーのみを行います。|
|Sound|String|カスタマイズしたAPNsのプッシュ音。|

受信者がiOSシステムであり、かつアプリがバックグラウンドになる場合、Descはプッシュテキストとして送信され、ExtフィールドはAPNS要求パケットPayloadsのextキー値として送信されますが、DataフィールドはAPNsのPayloadsフィールド以外のフィールドとして送信されます。注意：1つの組み合わせメッセージには1つのTIMCustomElemカスタムメッセージ要素だけを含めることができます。

### 音声メッセージ要素

>!音声メッセージは、サービス側に統合されたRest APIインターフェースを介して送信することはできません。音声メッセージを送信するには、クライアント側に適切なインターフェースを統合する必要があります。

4.XバーションのIM SDK（Android、iOS、MacおよびWindows）からの音声メッセージ要素の形式は次の通りです。
```
{
    "MsgType": "TIMSoundElem",
    "MsgContent": {
        "Url": "https://1234-5678187359-1253735226.cos.ap-shanghai.myqcloud.com/abc123/c9be9d32c05bfb77b3edafa4312c6c7d",
        "Size": 62351,
        "Second": 1,
		"Download_Flag": 2
    }
}
```

| フィールド | タイプ | 説明 |
|---------|---------|---------|
| Url | String | 音声ダウンロードアドレス。このURLアドレスを通じて必要な音声を直接ダウンロードできます。|
| Size | Number | 音声データのサイズ（単位：バイト）。|
| Second | Number | 音声時間（単位：秒）。|
| Download_Flag | Number | 音声ダウンロード方式のフラグ。現在、Download_Flagの値は2だけです。これは、`Url`フィールド値のURLアドレスから音声を直接ダウンロードできることを意味します。|

>?2.Xと3.XバーションのIM SDK（Android、iOS、MacおよびWindows）からの音声メッセージ要素は次の通りです。
>```
{
    "MsgType": "TIMSoundElem",
    "MsgContent": {
        "UUID": "305c0201", //音声シリアル番号、String型。バックグラウンドで音声の検索に使用されるキー値。このフィールドから必要な音声をダウンロードすることができません。この音声を取得するには、IM SDKバーションを4.Xにアップグレードしてください。
        "Size": 62351,		//音声データのサイズ、Number型、単位：バイト。
        "Second": 1         //音声時間、Number型、単位：秒。
    }
}
>```


### 画像メッセージ要素

>!画像メッセージは、サービス側に統合されたRest APIインターフェースを介して送信することはできません。画像メッセージを送信するには、クライアント側に適切なインターフェースを統合する必要があります。

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
                "Type": 2,      //大アイコン
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
| UUID | String | 画像シリアル番号。バックグラウンドで画像の検索に使用されるキー値。|
| ImageFormat | Number | 画像形式。JPG = 1、GIF = 2、PNG = 3、BMP = 4、その他 = 255。|
| ImageInfoArray | Array | 元の画像、サムネイルまたは大アイコンのダウンロード情報。|
| Type | Number | 画像のタイプ：1-元の画像、2-大アイコン、3-サムネイル。|
| Size | Number | 画像データのサイズ（単位：バイト）。|
| Width | Number | 画像の幅。|
| Height | Number | 画像の高さ。|
| URL | String | 画像のダウンロードアドレス。|

### ファイルメッセージ要素

>!ファイルメッセージは、サービス側に統合されたRest APIインターフェースを介して送信することはできません。ファイルメッセージを送信するには、クライアント側に適切なインターフェースを統合する必要があります。

4.XバーションのIM SDK（Android、iOS、MacおよびWindows）からのファイルメッセージ要素の形式は次の通りです。
```
{
    "MsgType": "TIMFileElem",
    "MsgContent": {
        "Url": "https://7492-5678539059-1253735326.cos.ap-shanghai.myqcloud.com/abc123/49be9d32c0fbfba7b31dafa4312c6c7d",
        "FileSize": 1773552,
        "FileName": "file:///private/var/Application/tmp/trim.B75D5F9B-1426-4913-8845-90DD46797FCD.MOV",
		"Download_Flag": 2
    }
}
```

| フィールド | タイプ | 説明 |
|---------|---------|---------|
| Url | String | ファイルダウンロードアドレス。このURLアドレスを通じて必要なファイルを直接ダウンロードできます。|
| FileSize | Number | ファイルデータのサイズ、単位：バイト。|
| FileName | String | ファイル名。|
| Download_Flag | Number | ファイルダウンロード方式のフラグ。現在、Download_Flagの値は2だけです。これは、`Url`フィールド値のURLアドレスからファイルを直接ダウンロードできることを意味します。|

>?2.Xと3.XバーションのIM SDK（Android、iOS、MacおよびWindows）からのファイルメッセージ要素は次の通りです。
>```
>{
>    "MsgType": "TIMFileElem",
>    "MsgContent": {
>        "UUID": "305c02010", //ファイルシリアル番号、String型。バックグラウンドでファイルの検索に使用されるキー値。このフィールドから必要なファイルをダウンロードすることができません。このファイルを取得するには、IM SDKバーションを4.Xにアップグレードしてください。
>        "FileSize": 1773552, //ファイルデータのサイズ、Number型、単位：バイト。
>        "FileName": "file:///private/var/Application/tmp/trim.B75D5F9B-1426-4913-8845-90DD46797FCD.MOV" //ファイル名、String型。
>    }
>}
>```


### 動画メッセージ要素

>!動画メッセージは、サービス側に統合されたRest APIインターフェースを介して送信することはできません。動画メッセージを送信するには、クライアント側に適切なインターフェースを統合する必要があります。

4.XバーションのIM SDK（Android、iOS、MacおよびWindows）からの動画メッセージ要素の形式は次の通りです。
```
{
    "MsgType": "TIMVideoFileElem",
    "MsgContent": {
        "VideoUrl": "https://0345-1400187352-1256635546.cos.ap-shanghai.myqcloud.com/abcd/f7c6ad3c50af7d83e23efe0a208b90c9",
        "VideoSize": 1194603,
        "VideoSecond": 5,
		"VideoFormat": "mp4",
		"VideoDownloadFlag":2,
		"ThumbUrl": "https://0345-1400187352-1256635546.cos.ap-shanghai.myqcloud.com/abcd/a6c170c9c599280cb06e0523d7a1f37b",
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
| VideoUrl | String | 動画ダウンロ一ドアドレス。このURLアドレスから必要な動画を直接ダウンロードできます。|
| VideoSize | Number | 動画データのサイズ、単位：バイト。|
| VideoSecond | Number | 動画時間、単位：秒。|
| VideoFormat | String | 動画形式、例えば、mp4。|
| VideoDownloadFlag | Number | 動画ダウンロード方式のフラグ。現在、VideoDownloadFlagの値は2だけです。これは、`VideoUrl`フィールド値のURLアドレスから動画を直接ダウンロードできることを意味します。|
| ThumbUrl | String | 動画サムネイルのダウンロードアドレス。このURLアドレスから必要な動画サムネイルを直接ダウンロードできます。|
| ThumbSize | Number | サムネイルのサイズ、単位：バイト。|
| ThumbWidth | Number | サムネイルの幅。|
| ThumbHeight | Number | サムネイルの高さ。|
| ThumbFormat | String | サムネイルの形式、例えば、JPG、BMPなど。|
| ThumbDownloadFlag | Number | 動画サムネイルダウンロード方式のフラグ。現在、ThumbDownloadFlagの値は2だけです。これは、`ThumbUrl`フィールド値のURLアドレスから動画サムネイルを直接ダウンロードできることを意味します。|


>?2.Xと3.XバーションのIM SDK（Android、iOS、MacおよびWindows）からの動画メッセージ要素は次の通りです。
>```
{
    "MsgType": "TIMVideoFileElem",
    "MsgContent": {
        "VideoUUID": "1400123456_dramon_34ca36be7dd214dc50a49238ef80a6b5",//動画シリアル番号、String型。バックグラウンドで動画の検索に使用されるキー値。このフィールドから必要な動画をダウンロードすることができません。この動画を取得するには、IM SDKバーションを4.Xにアップグレードしてください。
        "VideoSize": 1194603, //動画データのサイズ、Number型、単位：バイト。
        "VideoSecond": 5,     //動画時間、Number型、単位：秒。
		"VideoFormat": "mp4", //動画形式、String型、例えば、mp4。
		"ThumbUUID": "1400123456_dramon_893f5a7a4872676ae142c08acd49c18a",//動画サムネイルシリアル番号、String型。バックグラウンドで動画サムネイルの検索に使用されるキー値。このフィールドから必要な動画サムネイルをダウンロードすることができません。この動画サムネイルを取得するには、IM SDKバーションを4.Xにアップグレードしてください。
		"ThumbSize": 13907,   //サムネイルのサイズ Number型、単位：バイト。
		"ThumbWidth": 720,    //サムネイルの幅。Number型。
		"ThumbHeight": 1280,  //サムネイルの高さ。Number型。
		"ThumbFormat": "JPG"  //サムネイルの形式、String型、例えば、JPG、BMPなど。
    }
}
>```

## MsgBodyメッセージ内容のインスタンス

### 単一テキスト要素メッセージ

単一メッセージには、テキスト内容がhello worldであるテキストメッセージ要素を含みます。

```
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

### 組み合わせ情報

下記の単一メッセージには、2つのテキストメッセージ要素と1つの絵文字要素が含まれており、メッセージ要素の順序はテキスト+絵文字+テキストとなっています。
```
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

>!1つの組み合わせメッセージにTIMCustomElemカスタムメッセージ要素を1つだけ含むことができ、他のメッセージ要素の数量に制限はありません。

## Apple Push Notification Service（APNs）関連説明
### クライアントへのプッシュの表示形式の説明
- **アカウントのニックネームが設定されていない**
アカウントにニックネームが設定されていない場合、APNsプッシュはプッシュテキストの内容のみを表示します。1対1チャットメッセージは「プッシュテキスト」のみを表示し、グループメッセージは「（グループ名」：プッシュテキスト」のように表示します。
![](https://main.qcloudimg.com/raw/7bdb0f41aaa943190ce949fea8d20095.png)

- **アカウントのニックネームが設定された**
アカウントにニックネームが設定された場合、1対1チャットメッセージの表示形式は「ニックネーム：プッシュテキストの内容」であり、グループメッセージの表示形式はニックネーム（グループ名）：プッシュテキスト内容です。

- **組み合わせメッセージの表示形式**
組み合わせメッセージについて、各メッセージ要素のプッシュテキストを表示テキストとして順次重畳します。以下はアカウントニックネームを設定した1対1チャットメッセージです。プッシュテキストは「helloworld」です。helloworldにはスペースがなく、バックグラウンドで順番に重畳し、各メッセージ要素のプッシュテキストの間に文字が一切追加されていないことに注意してください。異なるメッセージ要素の間にスペースやその他の文字を追加する必要がある場合、呼び出し側が自ら判断します。
<pre>
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
</pre>
![](https://main.qcloudimg.com/raw/8a9b70df695ecf77c10c5ffba03d9864.png)

各メッセージ要素のプッシュテキストフィールドは次のようにまとめます。

| MsgTypeの値 | タイプ |メッセージ要素プッシュテキスト|
|---------|---------|---------|
| TIMTextElem | テキストメッセージ。|Textフィールド。|
|TIMLocationElem|地理位置メッセージ。|中国語版のオフラインプッシュテキストは「[位置]」；英文版は「[Location]」です。|
|TIMFaceElem|絵文字メッセージ。|中国語版のオフラインプッシュテキストは「[表情（絵文字）]”；英文版は「[Face]」です。|
|TIMCustomElem|カスタム情報。|Descフィールド。|

### ニックネームとグループ名のREST API設定インターフェース
アカウントニックネームのREST APIインターフェースを設定する：[情報設定](https://intl.cloud.tencent.com/document/product/1047/34916)。
グループ名のREST APIインターフェースを設定する：[グループ基本情報変更](https://intl.cloud.tencent.com/document/product/1047/34962)。

### 高級アプリケーション
#### プッシュ音声のカスタマイズ、APNsから拡張フィールドの送信。
カスタムメッセージ要素TIMCustomElemを使用して、Soundはカスタム音声ファイル名を入力し、Extは送信された拡張フィールドを入力します。要求拡張フィールドはAPNsプッシュPayLoadのExtフィールドから取得できます。
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

クライアントが受信したAPNsからプッシュされたJSON Payloadは：

```
{
    "aps": {
        "alert": "Nickname:helloworld",   //各メッセージ要素のプッシュテキストの順番重畳
        "badge": 5,                       
        "sound": "dingdong.aiff"         //TIMCustomElemのSoundフィールドに対応する
    }, 
    "ext": "www.qq.com"                //TIMCustomElemのExtフィールドに対応する
}

```

## オフラインプッシュOfflinePushInfoの説明

OfflinePushInfoは、オフラインプッシュの設定に使用されるJSONオブジェクトです。このメッセージのプッシュの無効化、テキスト記述内容のプッシュ、パススルー文字列のプッシュをするかどうかを構成できます。オフラインプッシュ情報を簡単に設定するため、TIMCustomElemカプセル化をせずに、OfflinePushInfoを使用するだけでよいです。

>!OfflinePushInfoが設定された場合、TIMCustomElem内のオフラインプッシュに関連する情報の構成は無視されます。OfflinePushInfoは現在、APNsプッシュおよびAndroidメーカーのプッシュ配信（Xiaomi、Huawei、MEIZU、OPPO、vivoのプッシュ）に適用されています。

OfflinePushInfoの形式例は次の通りです。

```
{
    // ...
    "MsgBody": [...] // MsgBodyの関連記述
    "OfflinePushInfo": {
        "PushFlag": 0,
        "Title":"これはプッシュ配信の表題",
        "Desc": "これはオフラインプッシュ配信内容",
        "Ext": "これはパススルー内容",
        "AndroidInfo": { 
			"Sound": "android.mp3",
			"OPPOChannelID": "test_OPPO_channel_id"
        },
        "ApnsInfo": {
            "Sound": "apns.mp3",
            "BadgeMode": 1,
            "Title":"apns title",
            "SubTitle":"apns subtitle",
            "Image":"www.image.com"
        }
    }
}
```

フィールドの説明は以下の通りです。

| フィールド | タイプ | 属性 | 説明 |
|---------|---------|---------|---------|
| PushFlag | Integer | オプション | 0はプッシュすること、1はオフラインプッシュしないことを意味します。  |
| Title | String | オプション | オフラインプッシュ表題。このフィールドはiOSとAndroidが共通します。|
| Desc | String | オプション | オフラインプッシュ内容。このフィールドは上記の各メッセージ要素 [TIMMsgElement](https://intl.cloud.tencent.com/document/product/1047/33527)のオフラインプッシュ表示テキストを上書きします。<br>送信されたメッセージには[TIMCustomElem](https://intl.cloud.tencent.com/document/product/1047/33527)カスタムメッセージ要素が1つしかありません。このDescフィールドはTIMCustomElemのDescフィールドを上書きします。どちらのDescフィールドが設定されないと、このカスタムメッセージのオフラインプッシュを受信することができません。|
| Ext | String | オプション | オフラインプッシュのパススルー内容。国内のAndroid携帯電話メーカーのプッシュ配信プラットフォームに対する要求がそれぞれ異なるため、このフィールドがJSON形式であることを確保してください。そうでない場合、一部のメーカーからのオフラインプッシュ配信を受信できない可能性があります。|
| AndroidInfo.Sound | String | オプション | Androidがオフラインで音声ファイルをプッシュ配信するパス。|
| AndroidInfo.HuaWeiChannelID | String | オプション | Huawei携帯電話EMUI 10.0以降の通知経路フィールド。|
| AndroidInfo.XiaoMiChannelID | String | オプション | Xiaomi携帯電話MIUI 10以降の通知種類（Channel）の適用フィールド。|
| AndroidInfo.OPPOChannelID | String | オプション | OPPO携帯電話Android 8.0以降のNotificationChannel通知の適用フィールド。|
| AndroidInfo.GoogleChannelID | String | オプション | Google携帯電話Android 8.0以降の通知経路フィールド。Googleのプッシュ配信のための新しいインターフェース（証明書ファイルをアップロードする）は、channel idをサポートするが、旧いインターフェース（サーバーキーを記入）はサポートしません。|
| ApnsInfo.BadgeMode | Integer | オプション | このフィールドはデフォルト設定または0の場合はカウントされることを意味します。1はこのメッセージがカウントされない（右上隅のアイコン数字が増加しない）ことを意味します。|
| ApnsInfo.Title|String|オプション|このフィールドは、APNsからプッシュされた表題を識別するために使用されます。設定されると最上層のTitleを上書きます。|
| ApnsInfo.SubTitle|String|オプション|このフィールドはAPNsからプッシュされたサブ表題を識別するために使用されます。|
| ApnsInfo.Image|String|オプション|このフィールドはAPNsに含まれている画像アドレスを識別するために使用されます。クライアントがこのフィールドを取得した場合、画像リソースをダウンロードして画像を、表示ウィンドウ内に表示できます。|

>!APNsのプッシュはパケットサイズを4K以内に制限するため、他の管理フィールドを除いて、DescフィールドとExtフィールドの合計は3Kを超えないようにすることをお勧めします。

## 参考資料

Apple Push Notification Service(APNs) [アップル社プッシュ配信開発ドキュメント](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/Introduction.html#//apple_ref/doc/uid/TP40008194-CH1-SW1)。
iOSオフラインメッセージのプッシュ設定：[オフラインプッシュ(iOS)](https://intl.cloud.tencent.com/document/product/1047/34347)。

