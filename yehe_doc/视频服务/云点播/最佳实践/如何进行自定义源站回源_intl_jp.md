## 概要

カスタムオリジンサーバーのback-to-originとは、Video on Demand（VOD）のCDN機能を利用し、カスタムドメイン名を作成してback-to-origin情報を設定することで、ユーザーがサードパーティオリジンサーバーに保存したメディアファイルをVODによってアクセラレーション配信できるようにし、マルチクラウドシナリオにおけるメディア配信ソリューションをご提供するものです。ここではVODのカスタムオリジンサーバーback-to-origin機能の設定および使用方法についてご説明します。

## シナリオ

- **オリジンサーバーの移行コストが高い**：ユーザーのメディアが他のサードパーティクラウド上に保存され、そのオリジンサーバーのコンテンツがサードパーティプラットフォームと高度に結びついているためにオリジンサーバーの移行が困難な場合、カスタムback-to-originによって、オリジンサーバーを移行せずにVOD CDNを使用してコンテンツのアクセラレーション配信を行うことができます。
- **高い再生品質が求められる**：ユーザーのコンテンツがネットワーク遅延やラグに対する要件が厳しく、他のサードパーティプラットフォームではニーズを満たせない場合、カスタムback-to-originによってお客様のオーディオビデオ再生をよりスムーズにし、業務サービス品質を保証することができます。
- **複数のクラウドの共存によりリスクを低減**：ユーザーのコンテンツおよび業務が、その信頼性を保障し、業務の障害復旧機能を向上させるために複数のコンテンツアクセラレーションチャネルを必要とするものである場合は、Tencent Cloud VOD CDNを選択してオーディオビデオアクセラレーション配信を行うことができます。

##  前提条件

1. Tencent Cloudアカウントを[登録](https://intl.cloud.tencent.com/register?&s_url=https%3A%2F%2Fcloud.tencent.com%2F)して[ログイン](https://intl.cloud.tencent.com/login?s_url=https%3A%2F%2Fcloud.tencent.com%2F)し、アカウントの実名認証を完了していること。
2. Tencent Cloud VODサービスがアクティブ化されました。まだアクティブ化されていない場合は、[VODサービス](https://console.cloud.tencent.com/vod/overview)に移動してアクティブ化してください。

## サポートするback-to-originオリジンサーバータイプ

- **ユーザー保有オリジンサーバー**
- **サードパーティCOS**

## 実践手順

### ステップ1：カスタムドメイン名の作成とback-to-origin情報の設定

1. カスタムオリジンサーバーback-to-origin機能を有効化した後、VODコンソールにログインし、左側ナビゲーションバーで**配信と再生の設定**>[**ドメイン名管理**](https://console.cloud.tencent.com/vod/distribute-play/domain)を選択し、**ドメイン名管理**ページに進みます。
2. 上の**カスタムオリジンサーバーアクセラレーションドメイン名**をクリックし、**カスタムオリジンサーバーアクセラレーションドメイン名**のページに進みます。
![](https://qcloudimg.tencent-cloud.cn/raw/e68e04641c3ad616450a70c72d5d3dcd.png)
3. **ドメイン名の追加**をクリックし、ICP登録済みのドメイン名を入力し、アクセラレーションリージョンを選択します。具体的な操作については、 [VODアクセラレーションドメイン名](https://intl.cloud.tencent.com/document/product/266/35572)をご参照ください。
![](https://qcloudimg.tencent-cloud.cn/raw/0fbcc49821fd7eebffd9ad17a81072b1.png)
4. ユーザーの実際のback-to-originニーズに応じてオリジンサーバーの設定を入力します。現在は**ユーザー保有オリジンサーバー**と**サードパーティCOS**のback-to-origin方式をサポートしています。具体的な設定についての説明は次のとおりです。     
![](https://qcloudimg.tencent-cloud.cn/raw/9ac80033d6fb055e299a2f355d0d1825.png) 

**ユーザー保有オリジンサーバー**
安定して稼働する業務用サーバーをback-to-originオリジンサーバーとし、VOD CDNによってサーバー上のメディアファイルをアクセラレーション配信したい場合は、以下の方法でオリジンサーバーを設定してください。
<table>
   <tr>
      <th width="0px" style="text-align:center">設定項目</td>
      <th width="0px"  style="text-align:center">説明</td>
   </tr>
   <tr>
      <td>オリジンサーバータイプ</td>
      <td><b>ユーザー保有オリジンサーバー</b>を選択します</td>
   </tr>
   <tr>
      <td>back-to-originプロトコル</td>
      <td>オリジンサーバーのサポート状況に応じてback-to-originリクエストプロトコルを選択します。HTTP、HTTPSおよびプロトコル追従をサポートしています</td>
   </tr>
	   <tr>
      <td>オリジンサーバーアドレス</td>
      <td>	複数のIPオリジンサーバー（コンマで区切る）または1つのドメイン名オリジンサーバーを入力できます</td>
   </tr>
	 <tr>
      <td>back-to-origin HOST</td>
      <td>ユーザー保有オリジンサーバーではback-to-origin HOSTを指定できます。back-to-origin HOSTは、CDNノードのback-to-originの際に、オリジンサーバーでアクセスするサイトのドメイン名/IPの具体的なサイトを指定するために用いられます<br>back-to-origin HOSTを指定していない場合は、デフォルトで現在作成されているアクセラレーションドメイン名となります</td>
   </tr>
</table>

<dx-alert infotype="explain" title="">
- オリジンサーバーアドレスにはVODデフォルトドメイン名は使用できません。
- プロトコル追従では、HTTPアクセスはHTTP back-to-originを使用し、HTTPSアクセスはHTTPS back-to-originを使用することができます（オリジンサーバーがHTTPSアクセスをサポートしていることが必要です）。
- ドメイン名をback-to-originアドレスとして選択できます。このドメイン名は、業務用のアクセラレーションドメイン名と同じものにすることはできません。
</dx-alert>
<b>サードパーティCOS</b><br>
サードパーティCOSに保存されたメディアファイルを、VOD CDN機能によってアクセラレーション配信したい場合は、以下の方法でオリジンサーバーを設定してください。              
<table>
   <tr>
      <th width="0px" style="text-align:center">設定項目</td>
      <th width="0px"  style="text-align:center">説明</td>
   </tr>
   <tr>
      <td>オリジンサーバータイプ</td>
      <td><b>サードパーティCOS</b>を選択します</td>
   </tr>
   <tr>
      <td>サードパーティCOS</td>
      <td>現在サポートしているサードパーティCOSはAlibaba Cloud OSSとAWS S3です</td>
   </tr>
	   <tr>
	<td>back-to-originプロトコル</td>
	  <td>HTTP、HTTPSをサポートしています</td>
   </tr>
	 <tr>
      <td>オリジンサーバーアドレス</td>
      <td>有効なバケットアクセスアドレスをオリジンサーバーとして入力します（http://またはhttp://プロトコルヘッダーを含めることはできません）</td>
   </tr>
</table>

<img src="https://qcloudimg.tencent-cloud.cn/raw/f5ca4759794c94ffba9f6a960b9a8641.png" /><br>
プライベートアクセスのサードパーティCOSをオリジンサーバーとして選択する場合は、有効なアクセスIDおよびkeyを入力してback-to-origin認証を行う必要があります。認証に成功するとプライベートバケットへのアクセスが有効になります。<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/66864ace26867520f76172f2901ad138.png" />

### ステップ2：カスタムドメイン名の解決

追加済みのカスタムアクセラレーションドメイン名については、このドメイン名が指定するDNSサービスプロバイダでCNAMEを設定しなければ、ユーザーはアクセラレーションドメイン名によるメディアファイルへのアクセスができません。具体的な操作については、[VODアクセラレーションドメイン名-ドメイン名の解決](https://intl.cloud.tencent.com/document/product/266/42076)をご参照ください。

### ステップ3：カスタムオリジンサーバーback-to-originの設定結果の確認と変更
1. ドメイン名管理に進み、**カスタムオリジンサーバーアクセラレーションドメイン名**で、作成済みのドメイン名を選択して**設定**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/3522690fd01bd3c0f90eb1065dc87965.png)
2. **基本設定**をクリックすると、現在のカスタムドメイン名のback-to-origin設定情報を確認して変更できます。
![](https://qcloudimg.tencent-cloud.cn/raw/bb04aa08590e9f88680c29eb19a502b9.png)

上記の手順によって操作することで、ユーザーはユーザー保有オリジンサーバーまたはサードパーティCOSに基づくback-to-origin設定を完了し、VOD CDNによってカスタムオリジンサーバー上のメディアファイルを配信できるようになります。具体的な配信のフローについての説明は次のとおりです。

1. ユーザーがカスタムドメイン名（例：`test.com`）を追加してドメイン名解決とback-to-origin設定を完了した後、ブラウザからこのドメイン名下のメディアファイルにアクセスする場合（例：`http://www.test.com/test.mp4`）、まずLocal DNSに対しドメイン名解決リクエストを送信します。
2. Local DNSがドメイン名`test.com`を解決する際、すでにCNAME：`www.test.com.cdn.dnsv1.com`が設定されていることを発見し、リクエストをTencent GSLB（Global Server Load Balance。Tencentが自社開発したグローバルロードバランサシステム）に解決します。
3. GSLBは最適なアクセスノードのIPリストを返し、Local DNSはこれに応じた解決IPを取得します。
4. ユーザーは最適なアクセスIPノードを取得します。
5. ユーザーは最適なアクセスIPノードに、`http://www.test.com/test.mp4`に対するアクセスリクエストを送信します。
6. このCDNノード上にtest.mp4がキャッシュされている場合、ユーザーはデータを取得し、このリクエストを終了します。このCDNノードにこのリソースがキャッシュされていない場合、このノードは設定された**業務オリジンサーバー**に、test.mp4に対するリクエストを送信し、リソースを取得した後、デフォルトで現在のノードにキャッシュし、リソースをユーザーに返します。リクエストはこの時点で終了します。

>? ユーザーがカスタムオリジンサーバーback-to-origin機能を使用してメディアファイルのアクセラレーション配信および再生を行うと、**ダウンストリームトラフィック**料金と**back-to-originオリジンサーバートラフィック**料金が発生します。このうちダウンストリームトラフィック料金はVODによって課金されます。具体的なルールについては[トラフィック課金](https://intl.cloud.tencent.com/document/product/266/14666)および[トラフィックリソースパック](https://www.tencentcloud.com/document/product/266/52806#2.-.E6.B5.81.E9.87.8F.E8.B5.84.E6.BA.90.E5.8C.85)をご参照ください。back-to-originオリジンサーバーのトラフィック料金はオリジンサーバーによって課金されます。