## 操作シナリオ

ここでは主に、TEMコンソールでアプリケーションアクセスとルートを設定する具体的な手順について説明します。転送ルールを設定することにより、パブリックネットワークにHTTP/HTTPSプロトコル転送ルールを実装することができます。適用ケースは主に次のとおりです。

- マイクロサービスやゲートウェイアプリケーションなどの、パブリックネットワークアクセスのエントリーが必要なアプリケーション。
- ドメイン名を関連付ける必要があるケース。
- 同じドメイン名に、異なるパスのルート転送が存在するケース。
- ドメイン名は異なるが、同じアプリケーションを指す必要があるケース。

## 操作手順

1. [TEMコンソール](https://console.cloud.tencent.com/tem)にログインします。
2. 【環境】ページで、デプロイリージョンを選択後、目的の環境カードの下部にある【詳細の表示】をクリックして、環境の詳細情報ページに進みます。
3. ページトップの【CAM】タブを選択し、【新規作成】をクリックして、転送ルールの名称を入力します。
      ![](https://main.qcloudimg.com/raw/d123003055bc8ed29d40afb9dd020194.png)
   - ネットワークタイプ：パブリックネットワークアクセスです。環境内へのアクセスについては、[アプリケーションの作成とデプロイ](https://intl.cloud.tencent.com/document/product/1094/40362)をご参照ください。
   - Cloud Load Balance：自動作成
   - プロトコルとポート：HTTP:80とHTTPS:443をサポートし、HTTPSドメイン名バインド証明書をサポートします
   - 転送構成：
     - ドメイン名:既存のドメイン名のバインドをサポートしています。ドメイン名がない場合は、デフォルトでIPv4 IPが割り当てられます
     - パス：デフォルトは「/」で、実際の状況に応じて設定します
     - バックエンドサービス：実際の状況に応じて選択します
     - サービスポート：実際の状況に応じて選択します
   - サーバー証明書：HTTPプロトコルを選択する場合は、サーバー証明書を選択する必要があります。既存の証明書が適切でない場合は、[サーバー証明書の新規作成](https://console.cloud.tencent.com/clb/cert)に移動できます
4. 【確定】をクリックして、アプリケーションアクセスルートの設定を完了します。

## 関連操作

- **アクセス設定ルールを変更：**対象ルールの操作列の【編集】をクリックすると、ポップアップウィンドウでアクセス設定情報を変更できます。
- **アクセス設定ルールを削除：**対象ルールの操作列の【削除】をクリックし、ポップアップウィンドウで確認を選択すると、アクセス設定情報を削除できます。
- **転送ルールの詳細を確認：**対象ルールの操作列の【転送ルールの確認】をクリックすると、ポップアップウィンドウに転送ルール情報が表示されます。
