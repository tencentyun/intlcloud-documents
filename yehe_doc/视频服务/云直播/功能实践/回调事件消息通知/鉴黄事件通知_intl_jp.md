CSSポルノ検出では、ライブストリーミング中にポルノ関係の疑いのある画面をリアルタイムで切り取ってイメージにし、さらに生成した画像をCOSの中に保存します。ポルノ検出コールバックはライブストリーミングのポルノ検出画像情報のプッシュに用いられ、これには問題画像が属するタイプ、レベル評価、スクリーンキャプチャの時間などが含まれます。コールバックテンプレートの中でポルノ検出コールバックメッセージの受信サーバーアドレスを設定し、当該テンプレートとプッシュドメイン名をバインドする必要があります。ライブストリーミングがポルノ検出イベントをトリガーした後、Tencent Cloud CSSのバックエンドがポルノ関連画像情報をお客様が設定した受信サーバーにコールバックします。

ここでは、主にポルノ検出コールバックイベントがトリガーされた後、Tencent Cloudバックエンドがユーザーに送信するコールバックメッセージ通知のフィールドについてご説明します。

## 注意事項
- このドキュメントを読む前に、Tencent Cloud CSSによるコールバック機能の設定方法とコールバックメッセージの受信方法についてご理解下さると幸いです。詳細については、[イベント通知の受信方法](https://intl.cloud.tencent.com/document/product/267/38080)をご参照ください。
- CSSポルノ検出は、デフォルトでは疑わしい結果に対してのみコールバックを行い、通常の結果にはコールバックを行いません。
- 画像の [type](#type)を利用してポルノ画像に対する評定を行う場合、検出システムの判定を100%の精度にすることはできないため、時折判定が誤っていることもあります。よって、実際のユースケースに応じて、人による二次確認を実施することをお勧めします。

## スクリーンキャプチャイベントのパラメータ説明
### イベントタイプパラメータ

| イベントタイプ | フィールド設定値の説明           |
| :------- | :------------- |
| CSSポルノ検出 | event_type = 317 |


### コールバック共通パラメータ

<table>
<tr><th>フィールド名</th><th>タイプ</th><th>説明</th></tr>
<tr>
<td>t</td>
<td>int64</td>
<td>期限、イベント通知サイン期限切れのUNIX タイムスタンプ。<ul style="margin:0"><li>Tencent Cloudからのメッセージ通知のデフォルトの期限は10分です。メッセージ通知中の t 値が示す時間が期限切れならば、この通知を無効と判断でき、さらにはネットワークのリプレイアタックを防止することもできます。<li>t の形式は10進数UNIXタイムスタンプとなり、1970年1月1日（UTC/GMT 午後）から経過した秒数となります。</ul></td>
</tr><tr>
<td>sign</td>
<td>string</td>
<td>イベント通知セキュリティサイン sign = MD5（key + t）。<br>説明：Tencent Cloudが、暗号化 <a href="#key">key</a> と t で文字列を結合した後、MD5でsignの値を算出し、それを通知メッセージに入れます。お客様のバックエンドサーバーは、通知メッセージの受信後、同じアルゴリズムに基づきsignが正確か確認し、さらにメッセージが確実にTencent Cloudバックエンドから来たものかを確認することができます。</td>
</tr></table>

>? <span id="key"></span>keyは、【機能テンプレート】>[【コールバック設定】](https://console.cloud.tencent.com/live/config/callback)におけるコールバックキーで、主に認証のために使用します。お客様のデータ情報を安全に保護するため、入力することをお勧めします。
>![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)




### コールバックメッセージのパラメータ

| **パラメータ**       | **入力必須の有無** | **データタイプ** | **説明**                                                     |
| :------------- | :----------- | :----------- | :----------------------------------------------------------- |
| tid            | 入力必須         | Number       | 予備警告ポリシーID、ビデオコンテンツ予備警告：20001                             |
| streamId       | オプション         | String       | ストリーム名                                                       |
| channelId      | オプション         | string       | チャネルID                                                      |
| img            | 入力必須         | string       | 予備警告画像リンク                                                 |
| <span id="type"></span>type        | 入力必須        | Array        | 画像タイプ、0：通常の画像、1 - 5：不適切な画像 |
| confidence     | 入力必須         | Number       | ポルノ関連の信頼度、範囲 0-100。normalScore、 hotScore、 pornScore の総合評価の点数 |
| normalScore    | 入力必須         | Number       | 画像がノーマルな画像である評点                                         |
| hotScore       | 入力必須         | Number       | 画像がセクシー画像である評点                                         |
| pornScore      | 入力必須         | Number       | 画像がアダルト画像である評点                                         |
| level          | オプション         | Number       | 画像のレベル                                                   |
| ocrMsg         | オプション         | string       | 画像のOCR識別情報（該当する場合）                              |
| screenshotTime | 入力必須         | Number       | スクリーンキャプチャ時間                                                     |
| sendTime       | 入力必須         | Number       | リクエスト送信時間、UNIXタイムスタンプ                                    |
| [gameDetails](#gamedetails)    | オプション         | Object       | ゲーム詳細情報                                                 |
| similarScore   | オプション         | Number       | 画像の類似度の評点                                               |
| stream_param   | オプション         | String       | プッシュパラメータ                                                     |
| app            | オプション         | String       | プッシュドメイン名                                                     |
| appid          | オプション         | Number       | 業務ID                                                      |
| appname        | オプション         | String       | プッシュpathパス                                               |


#### gameDetails

| **パラメータ名**  | **入力必須の有無** | **タイプ** | **説明**     |
| :------------ | :----------- | :------- | :----------- |
| battlegrounds | オプション         | Object   | BATTLEGROUNDSの情報 |
| [gameList](#gamelist)      | オプション         | Array    | ゲームリスト     |

#### gameList

| **パラメータ名** | **入力必須の有無** | **タイプ** | **説明** |
| :----------- | :----------- | :------- | :------- |
| name         | オプション         | String   | ゲーム名 |
| confidence   | オプション         | Number   | 確率     |

### コールバックメッセージの例

HTTP Body:
```
{
    "event_type":317,
    
    "ocrMsg":"",
    
    "type":[2],
    
    "confidence":0,
    
    "normalScore":2,
    
    "hotScore":97,
    
    "pornScore":0,
    
    "screenshotTime":1575513174,
    
    "level":0,
    
    "img":"http://test-10000.cos.ap-shanghai.myqcloud.com/2019-12-05/teststream-screenshot-10-32-54-960x540.jpg",
    
    "sendTime":1575513176,
    
    "similarScore":0,
    
    "tid":20001,
    
    "streamId":"teststream",
    
    "channelId":"teststream",
    
    "stream_param":"txSecret=40f38f69f574fd51126c421a3d96c374&txTime=5DEBEC80",
    
    "app":"testlive.myqcloud.com",
    
    "appname":"live",
    
    "appid":10000
}  
```





