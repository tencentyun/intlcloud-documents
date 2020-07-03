## 設定シナリオ
Tencent Cloud CDNはHTTPSアクセラレーションサービスをサポートしています。証明書をアップロードすることで展開できます。または、Tencent Cloud SSL証明書管理にホスティングされている証明書をCDNプラットフォームに直接展開し、HTTPSアクセラレーションサービスを有効にして、ネットワーク全体でのデータの暗号化転送を実現できます。

## 設定ガイド
### 設定の確認

[CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、メニューバーで【ドメイン名管理】を選択して、ドメイン名の右側にある【管理】をクリックすると、ドメイン名設定ページにアクセスします。【高度な設定】タブで指定されたドメイン名のHTTPS設定を確認できます。
![](https://main.qcloudimg.com/raw/26221c274317ff782a5408b9a9a2322a.png)
左のサイドバーメニューで【証明書の管理】ページにアクセスして、アカウント配下でHTTPSアクセラレーションが設定されているすべてのドメイン名のリストを確認することもできます。
![](https://main.qcloudimg.com/raw/ee27b41bc508d85ce92b6642b167cb11.png)

### ドメイン名の設定
#### 1. ドメイン名の選択
【証明書管理】メニューバーで【証明書の設定】をクリックし、証明書を設定するアクセラレーションドメイン名を選択します。
+ アクセラレーションドメイン名の状態は、「展開中」または「有効化済み」である必要があります。無効になっているドメイン名は、HTTPSアクセラレーションを設定できません。
+ `.file.myqcloud.com`サフィックスはTencent Cloud COSのデフォルトのアクセラレーションドメイン名であり、証明書を設定する必要がなく、HTTPSアクセラレーションを直接実行できます。
+ `.image.myqcloud.com`サフィックスは、Tencent Cloud CIのデフォルトのアクセラレーションドメイン名であり、証明書を設定する必要がなく、HTTPSアクセラレーションを直接実行できます。

![](https://main.qcloudimg.com/raw/e5e59c614f3e7461f088e11c7353be9e.png)

#### 2. 証明書の選択
PEM形式の既存の証明書がある場合は、その証明書の内容とプライベートキーを対応するフィールドに直接貼り付けることができます。
+ Tencent Cloud CDNサービスがECC証明書の展開をサポートするようになりました。
+ 証明書の内容はPEM形式である必要があります。PEM形式以外の場合は、[他の形式からPEM形式への変換](https://cloud.tencent.com/document/product/228/41686#.E6.A0.BC.E5.BC.8F.E8.BD.AC.E6.8D.A2)をご参照ください。
+ Tencent Cloud ホスト証明書を選択して、ワンクリックで直接デプロイできます。

![](https://main.qcloudimg.com/raw/05bf07790a4cffc1ca98877c14767471.png)

#### 3. back to origin方式

アクセラレーションドメイン名を接続する時や、オリジンサーバーでモジュールを設定する時にback to origin方式を設定できるほか、証明書を設定する時にも、back to originプロトコルを調整することもできます。Tencent Cloud CDNサービスは、次の3つのback to originプロトコルをサポートしています。
+ HTTP back to origin：すべてのリクエストはHTTP back to originを使用します。
+ HTTPS back to origin：すべてのリクエストはHTTPS back to originを使用します。
+ Follow protocol：リクエストプロトコルに従ってback to originを行い、HTTPSリクエストはHTTPS back to originを使用し、HTTPリクエストはHTTP back to originを使用します。

![](https://main.qcloudimg.com/raw/8e37661a97b431c871e3cb185f048b38.png)

>
> + Follow protocolまたはHTTPS back to originを設定する場合、オリジンサーバーに有効な証明書を展開する必要があります。そうしないと、back to originが失敗する場合があります。
> + 現在、HTTPS back to originはポート443のみをサポートしています。ご利用のオリジンサーバーが別のポートに指定されている場合、設定が失敗する場合があります。

### 一括設定
上部の【一括設定】をクリックすると、証明書をアップロードして、適応するドメイン名を自動的にマッチングして、一括設定を行います。
#### 1. 証明書の選択
PEM形式の既存の証明書がある場合は、その証明書の内容とプライベートキーを対応するフィールドに直接貼り付けることができます。
+ Tencent Cloud CDNサービスがECC証明書の展開をサポートするようになりました。
+ 証明書の内容はPEM形式である必要があります。PEM形式以外の場合は、[他の形式からPEM形式への変換](https://cloud.tencent.com/document/product/228/41686#.E6.A0.BC.E5.BC.8F.E8.BD.AC.E6.8D.A2)をご参照ください。
+ Tencent Cloud ホスト証明書を選択して、ワンクリックで直接デプロイできます。

![](https://main.qcloudimg.com/raw/35bf20677f1f640c81d289d20f056ce4.png)

#### 2. ドメイン名の選択
アップロード/選択された証明書に基づいて、CDNサービスは設定可能なドメイン名を自動的にマッチングして、必要に応じてドメイン名を選択できます。
![](https://main.qcloudimg.com/raw/89ad35a4fb3a5b30c0736c88bb06cf37.png)

#### 3. back to origin方式
アクセラレーションドメイン名を接続する時や、オリジンサーバーでモジュールを設定する時にback to origin方式を設定できるほか、証明書を一括設定する時にも、back to originプロトコルを一括調整することもできます。Tencent Cloud CDNは、次の3つのback to originプロトコルをサポートしています。
+ HTTP back to origin：すべてのリクエストはHTTP back to originを使用します。
+ HTTPS back to origin：すべてのリクエストはHTTPS back to originを使用します。
+ Follow protocol：リクエストプロトコルに従ってback to originを行い、HTTPSリクエストはHTTPS back to originを使用し、HTTPリクエストはHTTP back to originを使用します。

>
> + 一括設定が送信された後、選択されたドメイン名が1つずつ証明書を展開します。異常が発生した場合、リストページに「更新に失敗しました」という状態が表示され、元の設定が引き続き有効になります。
> + 更新に失敗した場合は、右側の【編集】をクリックして再設定できます。

### 証明書の変更
#### 証明書の変更
証明書の右側にある【編集】をクリックして、ドメイン名を指定して証明書を更新するか、再度一括設定して元の証明書設定を上書きすることもできます。
![](https://main.qcloudimg.com/raw/0156b76f7081747b9619bb171fef740d.png)
更新された証明書は実稼働環境のHTTPSサービスに影響を与えることなく、ネットワーク全体でノードごとに有効になります。【削除】をクリックしてHTTPSアクセラレーションサービスをキャンセルすることもできます。

#### 証明書の期限切れ
証明書は期限切れの30日前、15日前、7日前及び期限切れの当日には、Tencent CloudはSMS、メール、サイト内メッセージでユーザーのアカウントへ有効期限切れ通知を送ります。現在、SSL証明書のアラームの受信者をカスタマイズできます。お客様は [メッセージサブスクリプション](https://console.cloud.tencent.com/message/subscription)ページにアクセスして設定できます。

### 地域の特別な設定
アクセラレーションドメイン名のサービスエリアがグローバルの場合、設定されたHTTPS証明書は中国本土と中国本土以外の両方で有効になり、中国本土と中国本土以外で異なる証明書を設定することは現在サポートされません。

ドメイン名が中国本土と中国本土以外で異なる証明書で設定されている場合、【証明書管理】ページで中国本土と中国本土以外などのマークが表示されていれば、対象ドメイン名に特別な地域設定が残っていることが分かります。　
![](https://main.qcloudimg.com/raw/23192c43c0611c34d07490f19ea7dfb0.png)
ドメイン名の【高度な設定】タブには、次の2つの設定も確認できます。
![](https://main.qcloudimg.com/raw/febb17a67f10eb81941013895e67913f.png)
アクセラレーションドメイン名にこのような特殊な設定があり、証明書のいずれを変更する必要がある場合は、[チケットを送信](https://console.cloud.tencent.com/workorder/category) して変更してください。

