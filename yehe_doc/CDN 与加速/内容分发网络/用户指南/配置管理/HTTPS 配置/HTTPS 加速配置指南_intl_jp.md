## 設定シナリオ
Tencent Cloud CDNはHTTPSアクセラレーションサービスをサポートしています。証明書をアップロードすることで展開できます。または、Tencent Cloud SSL証明書管理にホスティングされている証明書をCDNプラットフォームに直接展開し、HTTPSアクセラレーションサービスを有効にして、ネットワーク全体でのデータの暗号化転送を実現できます。

## 設定ガイド
### 設定の確認

[CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、左側のナビゲーションメニューバーで【ドメイン管理】を選択して、ドメイン名の右側にある【管理】をクリックすると、ドメイン名設定ページにアクセスします。【高度な設定】タブで指定されたドメイン名のHTTPS設定を確認できます。
![](https://main.qcloudimg.com/raw/df6c4966cfee58661251f88550214576.png)
左側のナビゲーションメニューバーで【証明書管理】をクリックすると、証明書管理ページに進んで、アカウント配下でHTTPSアクセラレーションが設定されているすべてのドメイン名のリストを確認することもできます。
![](https://main.qcloudimg.com/raw/91335ed0a426118b76ad6b27a53d5197.png)

### 証明書の設定
#### 1. ドメイン名の選択
【証明書管理】ページで、【証明書の設定】をクリックし、証明書を設定するアクセラレーションドメイン名を選択します。
+ アクセラレーションドメイン名の状態は、「展開中」または「有効化済み」である必要があります。無効になっているドメイン名は、HTTPSアクセラレーションを設定できません。
+ `.file.myqcloud.com`サフィックスはTencent Cloud COSデフォルトのアクセラレーションドメイン名であり、証明書を設定する必要がなく、HTTPSアクセラレーションを直接実行できます。
+ `.image.myqcloud.com`サフィックスのドメイン名は、Tencent Cloud CIデフォルトの加速ドメイン名であり、証明書を設定する必要がなく、HTTPSアクセラレーションを直接実行できます。

![](https://main.qcloudimg.com/raw/13c71dc1fc13576620768f7ae61d6c9e.png)

#### 2. 証明書の選択
PEM形式の既存の証明書がある場合は、その証明書の内容とプライベートキーを対応するフィールドに直接貼り付けることができます。
+ Tencent Cloud CDNサービスがECC証明書の展開をサポートするようになりました。
+ 証明書の内容はPEM形式である必要があります。PEM形式以外の場合は、[他の形式からPEM形式への変換](https://intl.cloud.tencent.com/document/product/228/35212)をご参照ください。
+ Tencent Cloud ホスト証明書を選択して、ワンクリックで直接展開できます。

![](https://main.qcloudimg.com/raw/d847eb87f076b972808b8e680705f706.png)

#### 3. back-to-origin方式

アクセラレーションドメイン名にアクセスする時や、オリジンサーバーでモジュールを設定する時にback-to-origin方式を設定できるほか、証明書を設定する時にも、back-to-originプロトコルを調整することもできます。Tencent Cloud CDNサービスは、次の3つのback-to-originプロトコルをサポートしています。
+ HTTP back-to-origin：すべてのリクエストはHTTP back-to-originを使用します。
+ HTTPS back-to-origin：すべてのリクエストはHTTPS back-to-originを使用します。
+ Follow protocol：リクエストプロトコルに従ってback-to-originを行い、HTTPSリクエストはHTTPS back-to-originを使用し、HTTPリクエストはHTTP back-to-originを使用します。

![](https://main.qcloudimg.com/raw/62b122177e6ee043d0063c8e5328e1e5.png)

>
> + Follow protocolまたはHTTPS back-to-originを設定する場合、オリジンサーバーに有効な証明書をデプロイする必要があります。そうしないと、back-to-originが失敗する場合があります。
> + 現在、HTTPS back-to-originはポート443のみをサポートしています。ご利用のオリジンサーバーが別のポートに指定されている場合、設定が失敗する場合があります。

### 一括設定
上部の【一括設定】をクリックすると、証明書をアップロードして、適応するドメイン名を自動的にマッチングして、一括設定を行います。
#### 1. 証明書の選択
PEM形式の既存の証明書がある場合は、その証明書の内容とプライベートキーを対応するフィールドに直接貼り付けることができます。
+ Tencent Cloud CDNサービスがECC証明書の展開をサポートするようになりました。
+ 証明書の内容はPEM形式である必要があります。PEM形式以外の場合は、[他の形式からPEM形式への変換](https://intl.cloud.tencent.com/document/product/228/35212)をご参照ください。
+ Tencent Cloud ホスト証明書を選択して、ワンクリックで直接展開できます。

![](https://main.qcloudimg.com/raw/fcadb92849ebd780acbbc5b35f343478.png)

#### 2. ドメイン名の選択
アップロード/選択された証明書に基づいて、CDNサービスは設定可能なドメイン名リストを自動的にマッチングして、必要に応じてドメイン名を選択できます。
![](https://main.qcloudimg.com/raw/04a8ad1088655f24282201da7b5ebd74.png)

#### 3. back-to-origin方式
アクセラレーションドメイン名にアクセスする時や、オリジンサーバーでモジュールを設定する時にback-to-origin方式を設定できるほか、証明書を設定する時にも、back-to-originプロトコルを調整することもできます。Tencent Cloud CDNサービスは、次の3つのback-to-originプロトコルをサポートしています。
+ HTTP back-to-origin：すべてのリクエストはHTTP back-to-originを使用します。
+ HTTPS back-to-origin：すべてのリクエストはHTTPS back-to-originを使用します。
+ Follow protocol：リクエストプロトコルに従ってback-to-originを行い、HTTPSリクエストはHTTPS back-to-originを使用し、HTTPリクエストはHTTP back-to-originを使用します。

>
> + 一括設定が送信された後、選択されたドメイン名が1つずつ証明書を展開します。異常が発生した場合、リストページに「更新に失敗しました」という状態が表示され、元の設定が引き続き有効になります。
> + 更新に失敗した場合は、右側の【編集】をクリックして再設定できます。

### 証明書の変更
#### 証明書の変更
証明書の右側にある【編集】をクリックして、ドメイン名を指定して証明書を更新するか、再度一括設定して元の証明書設定を上書きできます。
![](https://main.qcloudimg.com/raw/bb2ed5ec740aa67abf2750dc58baae0d.png)
更新された証明書は実稼働環境のHTTPSサービスに影響を与えることなく、ネットワーク全体でノードごとに有効になります。【削除】をクリックしてHTTPSアクセラレーションサービスをキャンセルすることもできます。

#### 証明書の有効期限切れ
証明書は有効期限切れの30日前、15日前、7日前及び期限切れ当日には、Tencent CloudはSMS、メール、サイト内メッセージでユーザーのアカウントへ有効期限切れ通知を送ります。現在、SSL証明書のアラームの受信者をカスタマイズできます。お客様は[メッセージの購読](https://console.cloud.tencent.com/message/subscription) にアクセスして設定することが可能です。

### リージョンの特別な設定
アクセラレーションドメイン名のサービスエリアがグローバルの場合、設定されたHTTPS証明書は中国本土と中国本土以外の両方で有効になり、中国本土と中国本土以外で異なる証明書を設定することは現在サポートされません。

ドメイン名が中国本土と中国本土以外で異なる証明書がある場合、【証明書管理】ページで中国本土と中国本土以外などのマークが表示されていれば、対象ドメイン名に特別な地域設定が残っていることが分かります。　
![](https://main.qcloudimg.com/raw/23192c43c0611c34d07490f19ea7dfb0.png)
ドメイン名の1【高度な設定】タブには、次の2つの設定も確認できます。
![](https://main.qcloudimg.com/raw/febb17a67f10eb81941013895e67913f.png)
アクセラレーションドメイン名にこのような特殊な設定があり、証明書のいずれを変更する必要がある場合は、[チケットを送信](https://console.cloud.tencent.com/workorder/category) して変更してください。

