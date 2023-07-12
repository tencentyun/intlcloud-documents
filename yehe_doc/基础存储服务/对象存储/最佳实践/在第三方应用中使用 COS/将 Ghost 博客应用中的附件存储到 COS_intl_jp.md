## 概要
[Ghost](https://ghost.org/docs)はNode.jsをベースにした、ブログ系のウェブサイトをスピーディーに構築できるフレームワークです。開発者はGhostの公式cliツールによって個人ウェブサイトをワンクリックで生成し、CVMやDocker上にデプロイすることができます。

添付ファイルのアップロードはブログ系ウェブサイトにとって欠かせない機能です。Ghostは添付ファイルをデフォルトでローカルに保存します。ここではプラグインによって添付ファイルを[Tencent Cloud Object Storage（COS）](https://www.tencentcloud.com/products/cos)に保存する方法についてご説明します。フォーラムの添付ファイルをCOSに保存すると次のようなメリットがあります。
- 添付ファイルの信頼性が高まります。
- サーバーがフォーラム添付ファイルのために追加のストレージスペースを用意する必要がありません。
- ユーザーが画像添付ファイルを確認する際は直接COSサーバーに接続するため、サーバーのダウンストリーム帯域幅/トラフィックを占有せず、ユーザーのアクセス速度がより速くなります。
- [Tencent Cloud Content Delivery Network（CDN）](https://www.tencentcloud.com/products/cdn)と併用することで、フォーラムユーザーの画像添付ファイル表示速度がさらに早くなります。

## 準備作業

### Ghostウェブサイトの構築

1. [Node.js](https://nodejs.org/en/download/)環境をインストールします。
2. ghost-cliをインストールします。
```js
npm install ghost-cli@latest -g
```
3. プロジェクトを作成し、このプロジェクトのルートディレクトリで次のコマンドを実行します。
```js
ghost install local
```
作成に成功すると、プロジェクトの構造は下図のようになります。
![](https://qcloudimg.tencent-cloud.cn/raw/76e74eff7779379f2e40c5c9220453fc.jpg)
4. ブラウザを開き、localhost:2368に進むと登録ページが表示されます。登録し、管理バックエンドに進みます。
![](https://qcloudimg.tencent-cloud.cn/raw/16c412b34d8d9eda9525d12b7e34f5cf.jpg)


### COSバケットの作成

1. [COSコンソール](https://console.cloud.tencent.com/cos/bucket)で、アクセス権限が**パブリック読み取り・プライベート書き込み**のバケットを作成します。操作ガイドについては[バケットの作成](https://intl.cloud.tencent.com/document/product/436/13309)をご参照ください。
2. **セキュリティ管理>クロスドメインアクセスCORS設定**をクリックし、クロスドメイン設定を1行追加します。デバッグの利便性のため、以下の設定を使用できます。操作ガイドについては、[クロスドメインアクセスの設定](https://intl.cloud.tencent.com/document/product/436/13318)をご参照ください。




## GhostをCOSバケットにバインドする

>!サブアカウントキーを使用し、[最小権限ガイド](https://intl.cloud.tencent.com/document/product/436/32972)に従うことで、使用上のリスクを低減させることをお勧めします。サブアカウントキーの取得については、[サブアカウントのアクセスキー管理](https://intl.cloud.tencent.com/document/product/598/32675)をご参照ください。


1. Ghostプロジェクトのルートディレクトリ下のconfig.development.json設定ファイルを変更し、次の設定を追加します。
```json
  "storage": {
    "active": "ghost-cos-store",
    "ghost-cos-store": {      
      "BasePath": "ghost/", // ご自身のディレクトリ名に変更できます。入力しない場合はデフォルトでルートディレクトリになります 
      "SecretId": "AKID*************",
      "SecretKey": "***************",
      "Bucket": "xxx-125********", 
      "Region": "**-*******"
    }
  }
```
パラメータの説明は次のとおりです。
<table>
   <tr>
      <th width="0%" >設定項目</td>
      <th width="0%" >設定値</td>
   </tr>
   <tr>
      <td>BasePath</td>
      <td>ファイルの保存先のCOSパスはご自身で変更できます。入力しない場合はデフォルトでルートディレクトリになります</td>
   </tr>
   <tr>
      <td>SecretId</td>
      <td>アクセスキー情報。<a href="https://console.cloud.tencent.com/capi">Tencent Cloud APIキー</a>に進んで作成と取得を行うことができます</td>
   </tr>
   <tr>
      <td>SecretKey</td>
      <td>アクセスキー情報。<a href="https://console.cloud.tencent.com/capi">Tencent Cloud APIキー</a>に進んで作成と取得を行うことができます。</td>
   </tr>
   <tr>
      <td>Bucket</td>
      <td>バケット作成時にカスタマイズした名前。例：examplebucket-1250000000。</td>
   </tr>
   <tr>
      <td>Region</td>
      <td>バケット作成時に選択したリージョン。</td>
   </tr>
</table>
2. カスタムストレージディレクトリを作成し、このプロジェクトのルートディレクトリで次を実行します。
```js
mkdir -p content/adapters/storage
```
3. Tencent Cloud公式が提供する[ghost-cos-store](https://github.com/tencentyun/ghost-cos-store)プラグインをインストールします。
   1. npmによってインストールします。
```js
npm install ghost-cos-store
```
   2. storageディレクトリ下にghost-cos-store.jsファイルを作成します。内容は次のとおりです。
```js
//  content/adapters/storage/ghost-cos-store.js
module.exports = require('ghost-cos-store');
```
   3. git cloneによってインストールします。
```js
cd content/adapters/storage
git clone https://github.com/tencentyun/ghost-cos-store.git
cd ghost-cos-store  
npm i
```
   4. インストール完了後にGhostの再起動が必要です。
```js
ghost restart
```



## 投稿してアップロードテストを行う

1. Ghost管理バックエンドに進み、クリックして記事を1件投稿します。
![](https://qcloudimg.tencent-cloud.cn/raw/27dc54b218009f64bd319707700dba71.jpg)
2. 画像のアップロードをクリックします。ブラウザでパケットキャプチャを行うとuploadリクエストの成功が確認でき、画像に対応したCOSリンクが返されます。



