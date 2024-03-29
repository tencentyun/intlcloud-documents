## ユースケース

VODのオープンCDNホスト機能は、ユーザーによるユーザー保有オリジンサーバーのメディアリソースの配信をサポートし、ユーザー保有オリジンサーバーとサードパーティCOSオリジンサーバーでback-to-origin機能を使用できるようにします。ユーザーはカスタムドメイン名を作成してオリジンサーバータイプ、back-to-originリクエストプロトコル、オリジンサーバーアドレスなどの情報を設定することで、カスタムオリジンサーバー機能を実装できます（カスタムドメイン名によって設定するカスタムback-to-origin機能に限ります）。

## 設定ガイド
1. [VODコンソール](https://console.cloud.tencent.com/vod)にログインして、左側ナビゲーションバーの**アプリケーション管理**をクリックして、アプリケーションリストページへ進みます。
2. 設定したいアプリケーションを見つけ、アプリケーション名をクリックし、アプリケーション管理ページに進みます。
3. デフォルトでは、**メディア情報管理**>**オーディオビデオ管理**、「アップロード済み」ページへ進みます。
4. 左側ナビゲーションバーの**配信と再生の設定**>[**ドメイン名管理**](https://console.cloud.tencent.com/vod/distribute-play/domain)を選択し、**ドメイン名管理**ページに進みます。
5. 上の**カスタムオリジンサーバーアクセラレーションドメイン名**をクリックし、「カスタムオリジンサーバーアクセラレーションドメイン名」リストページに進みます。
![img](https://qcloudimg.tencent-cloud.cn/raw/f0536b39ee6156173e7cd27b3642f791.png)
6. **ドメイン名の追加**をクリックし、実際のニーズに応じてドメイン名の設定とオリジンサーバーの設定を完了します。
 - ドメイン名の設定
ドメイン名の名前を入力し、ドメイン名のアクセラレーションリージョンを選択します。関連内容については[ドメイン名の追加](https://intl.cloud.tencent.com/document/product/266/35572)をご参照ください。
![](https://qcloudimg.tencent-cloud.cn/raw/ceb83e97ffdd3118c4890c13a68c6971.png)
 - オリジンサーバーの設定
![](https://qcloudimg.tencent-cloud.cn/raw/43279ccef236c0211c4b996f8ff92fd6.png)

**オリジンサーバータイプ**
VODはユーザー保有オリジンサーバーとサードパーティCOSの3種類のback-to-originタイプをご提供しています。ユーザーは実際のニーズに応じて設定を選択できます。
<table>
   <tr>
      <td >ユーザー保有オリジンサーバー</td>
      <td >すでに安定して稼働する業務用サーバー（オリジンサーバー）がある場合です。対応するIPアドレスリストを入力するか、または1つのドメイン名をオリジンサーバーアドレスとします。</td>
   </tr>
   <tr>
      <td>サードパーティCOS</td>
      <td>Tencent Cloud以外のサードパーティCOSです。現在サポートしているサードパーティはAlibaba Cloud OSSとAWS S3です。</td>
   </tr>
</table>


**back to originプロトコル**
VODアクセラレーションノードからユーザーオリジンサーバーへのback-to-originの際に使用するプロトコルであり、HTTPまたはHTTPSです。
<table>
   <tr>
      <td >HTTP back-to-origin</td>
      <td>アクセスがHTTP、HTTPSのどちらの場合もHTTP back-to-originを使用します。</td>
   </tr>
   <tr>
      <td>HTTPS back-to-origin</td>
      <td>アクセスがHTTP、HTTPSのどちらの場合もHTTPS back-to-originを使用します。</td>
   </tr>
	    <tr>
      <td>プロトコル追従</td>
      <td>HTTPリクエストの場合はHTTP back-to-originを使用し、HTTPSリクエストの場合はHTTPS back-to-originを使用します。</td>
   </tr>
</table>

>? HTTPS back-to-originが存在する場合は、オリジンサーバーがHTTPSアクセスをサポートしていないとback-to-originに失敗しますので、サポートしていることを確認してください。

**オリジンサーバーのアドレス**

<table>
   <tr>
      <td>ユーザー保有オリジンサーバー</td>
      <td>複数のIPオリジンサーバーまたは1つのドメイン名オリジンサーバー（コンマで区切る）を入力できます。</td>
   </tr>
   <tr>
      <td>サードパーティCOS</td>
      <td><li>リソースがすでにサードパーティCOSに保存されている場合は、有効なバケットアクセスアドレスをオリジンサーバーとして入力してください（`http://`または`http://`プロトコルヘッダーを含めることはできません）。現在サポートされているサードパーティは、Alibaba Cloud OSSとAWS S3 です。</li><br><li>サードパーティのプライベートバケットにback-to-originするには、有効なキーを入力し、back-to-origin認証を有効にして、プライベートバケットアクセスを有効にする必要があります。</li> </td>
   </tr>
</table>


>? ユーザー保有オリジンサーバーではback-to-origin HOSTを指定できます。back-to-origin HOSTは、CDNノードのback-to-originの際に、オリジンサーバーでアクセスするサイトのドメイン名/IPの具体的なサイトを指定するために用いられます。back-to-origin HOSTを指定していない場合は、デフォルトで現在作成されているアクセラレーションドメイン名となります。
4. ドメイン名解決を行います。追加済みのカスタムアクセラレーションドメイン名については、このドメイン名が指定するDNSサービスプロバイダでCNAMEを設定しなければ、ユーザーがドメイン名によってビデオメディアにアクセスすることができません。具体的な操作については、[VODアクセラレーションドメイン名-ドメイン名の解決](https://intl.cloud.tencent.com/document/product/266/35572#.E8.A7.A3.E6.9E.90.E5.9F.9F.E5.90.8D)をご参照ください。


## back-to-origin設定の変更
追加済みのカスタムドメイン名については、ユーザーの実際のニーズに応じて調整と変更を行うことができます。変更方法は次のとおりです。
1. [**ドメイン名管理**](https://console.cloud.tencent.com/vod/distribute-play/domain)>**カスタムオリジンサーバーアクセラレーションドメイン名**のページで、変更したいカスタムドメイン名を選択し、**設定**をクリックして詳細ページに進みます。
2. **変更**をクリックすると、元の設定情報を変更することができます。変更結果が反映されるまで5分ほどかかります。
![](https://qcloudimg.tencent-cloud.cn/raw/5df5f46ec7dc7fdc55f9bc3b780f8ac7.png)

>?
>- ユーザーがカスタムオリジンサーバーをVODオリジンサーバーに切り替える場合は、先にカスタムオリジンサーバードメイン名を無効化して削除してから、VODアクセラレーションドメイン名に対応するドメイン名を追加する必要があります。
>- ユーザーがカスタムオリジンサーバーを使用してback-to-originを行いたい場合は、先にVODアクセラレーションドメイン名に設定したドメイン名を無効化して削除してから、カスタムオリジンサーバーアクセラレーションドメイン名に移動して追加する必要があります。