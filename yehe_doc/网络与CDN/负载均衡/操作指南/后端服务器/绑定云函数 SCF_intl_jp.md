Serverless Cloud Function（SCF）の作成によってバックエンドWebサービスを実装後、CLBを使用してSCFをバインドし、外部にサービスを提供することができます。

## 背景情報
[Serverless Cloud Function（SCF）](https://intl.cloud.tencent.com/document/product/583)はTencent Cloudが企業および開発者向けにご提供するサーバーレスな実行環境であり、これによってサーバーを購入および管理することなくコードを実行できます。SCFを作成すると、CLBトリガーを作成することでSCFとイベントを関連付けることができます。CLBトリガーはリクエスト内容をパラメータ形式でSCFに伝達し、SCFからの戻り値をレスポンスとしてリクエスト側に返します。

## ユースケース
<dx-accordion>
::: 一般的な\sHTTP/HTTPS\s接続
eコマース、ソーシャルネットワーキング、ツールなどのAppアプリケーション、個人ブログ、イベントページなどのWebアプリケーションのシーンなどに適しています。方法のフローは次のとおりです。
1. App、ブラウザ、H5、ミニプログラムなどからHTTP/HTTPSリクエストを送信し、CLBを介してSCFにアクセスします。
2. CLBによって証明書をアンインストールします。SCFはHTTPサービスの提供のみ必要です。
3. リクエストをSCFに転送し、続いてクラウドデータベースへの書き込みやその他のAPIの呼び出しなど、その後の処理を行います。
![](https://main.qcloudimg.com/raw/534ca758662eaffdd40d243bd8384739.svg)
:::
::: CVM/SCF\sのスムーズな切り替え
HTTP/HTTPSサービスをCVMからSCFに移行するシーン、CVM（SCF）サービスに問題が生じた場合にSCF（CVM）にスピーディーに移行するフェイルオーバーのシーンに適しています。方法のフローは次のとおりです。
1. App、ブラウザ、H5、ミニプログラムなどからHTTP/HTTPSリクエストを送信します。
2. DNS解決によって、リクエストをCLBのVIPに解決します。
3. 1台のCLBからはリクエストをCVMに転送し、もう1台のCLBからはリクエストをSCFに転送します。
4. クライアントに影響することなく、CVMとSCFとの間でバックエンドサービスをスムーズに切り替えることができます。
![](https://main.qcloudimg.com/raw/d285c006b5945486a725936385d9dcb2.svg)
:::
::: CVM/SCF\s業務分離
タイムセール、買い占めなどのシーンに適しています。高い弾力性が求められるサービスの処理にはSCFを、日常業務の処理にはCVMを使用します。
1. DNS解決によって、ドメイン名Aを1台のCLBのVIPに、ドメイン名Bをもう1台のCLBのVIPに、それぞれ解決します。
2. このうち1台のCLBからはリクエストをCVMに転送し、もう1台のCLBからはリクエストをSCFに転送します。
![](https://main.qcloudimg.com/raw/96a77f06ecad23ddf13282aa2e6a496b.svg)
:::

</dx-accordion>



## 制限事項
- SCFのバインドは広州、上海、北京、成都、中国香港、シンガポール、ムンバイ、東京、シリコンバレーリージョンでのみサポートしています。
- SCFのバインドは標準アカウントタイプのみサポートしており、従来型アカウントタイプではサポートしていません。標準アカウントタイプへのアップグレードをお勧めします。詳細については、[アカウントタイプアップグレードの説明](https://intl.cloud.tencent.com/document/product/684/15246)をご参照ください。 
- SCFのバインドは基幹ネットワークタイプではサポートしていません。
- CLBは同一リージョン下のすべてのSCFのバインドをデフォルトでサポートしています。異なるVPC間でのSCFバインドはサポート可能ですが、異なるリージョン間でのバインドはサポートしていません。
- 現在はIPv4、IPv6 NAT64バージョンのCLBのみSCFのバインドをサポートしています。IPv6バージョンは現時点ではサポートしていません。
- SCFのバインドはレイヤー7（HTTP、HTTPS）リスナーのみサポートしており、レイヤー4（TCP、UDP、TCP SSL）リスナーおよびレイヤー7 QUICリスナーではサポートしていません。
- CLBのSCFバインドは「Event関数」タイプのSCFのみサポートしています。


## 前提条件
1. [CLBインスタンスの作成](https://intl.cloud.tencent.com/document/product/214/6149)
2. [HTTPリスナーの設定](https://intl.cloud.tencent.com/document/product/214/32515)または[HTTPSリスナーの設定](https://intl.cloud.tencent.com/document/product/214/32516)

## 操作手順
![](https://main.qcloudimg.com/raw/eca21ba71ea22a6c240d3b4a05dfdce0.svg)

### ステップ1：SCFの作成
1. [SCFコンソール](https://console.cloud.tencent.com/scf)にログインし、左側のナビゲーションバーで【関数サービス】をクリックします。
2. 「関数サービス」ページで、【新規作成】をクリックします。
3. 関数サービスの「新規作成」ページで、作成方法は「カスタム作成」を選択し、関数名を入力し、リージョンはCLBインスタンスと同一のリージョンを、実行環境は「Python3.6」をそれぞれ選択します。関数コード入力ボックスに次のコードを入力し（ここではHello CLBを例とします）、【完了】をクリックします。
>!CLBにSCFをバインドする際は、特定のレスポンス統合形式によって返す必要があります。詳細については、[統合レスポンス](https://intl.cloud.tencent.com/document/product/583/39849)をご参照ください。
```plaintext
# -*- coding: utf8 -*-
import json
def main_handler(event, context):

    return {
        "isBase64Encoded": False,
        "statusCode": 200,
        "headers": {"Content-Type":"text/html"},
        "body": "<html><body><h1>Hello CLB</h1></body></html>"
   }
```

### ステップ2：SCFのデプロイ
1. 「関数サービス」ページのリストで、先ほど作成した関数名をクリックします。
2. 「関数管理」ページで、【関数コード】タブをクリックし、タブの下にある【デプロイ】をクリックします。
![]()

### ステップ3：SCFのバインド
1. [CLBコンソール](https://console.cloud.tencent.com/clb)にログインし、左側のナビゲーションバーで【インスタンス管理】をクリックします。
2. 「インスタンス管理」ページの「CLB」タブで、目的のインスタンスの右側にある「操作」列の【リスナーの設定】をクリックします。
3. HTTP/HTTPSリスナーリストで、SCFをバインドしたいリスナーを選択し、目的のリスナーの左側の【+】および表示されたドメイン名の左側の【+】をそれぞれクリックし、表示されたURLパスを選択して【バインド】をクリックします。
![]()
4. ポップアップした「バックエンドサービスのバインド」ダイアログボックスで、ターゲットタイプに「SCF」を選択し、ネームスペース、関数名およびバージョン/エイリアスを選択し、重みを設定して【確定】をクリックします。
![]()
5. 「リスナーの管理」タブに戻り、「転送ルールの詳細」エリアでCLBにバインド済みのSCF、すなわち作成済みのCLBトリガーを表示します。
![]()
>? SCFコンソールでCLBトリガーを作成し、CLBとSCFをバインドする方法も選択できます。詳細については、[トリガーの作成](https://intl.cloud.tencent.com/document/product/583/31441)をご参照ください。

## 結果の検証
1. [SCFコンソール](https://console.cloud.tencent.com/scf)にログインし、左側のナビゲーションバーで【関数サービス】をクリックします。
2. 「関数サービス」ページのリストで、先ほど作成した関数名をクリックします。
3. 関数のページで、左側のリストの【トリガーの管理】をクリックします。
4. 「トリガーの管理」ページのトリガーで、アクセスパスをクリックします。
![]()
5. ブラウザでこのアクセスパスを開き、「Hello CLB」が表示された場合、関数のデプロイは成功です。
![]()


## 関連ドキュメント
[SCF関数の作成](https://intl.cloud.tencent.com/document/product/583/32742)
