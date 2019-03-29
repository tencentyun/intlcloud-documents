このドキュメントでは、Tencent Cloudを使用し始めたばかりの個人ユーザーのために、CentOSシステムでnginxプロジェクトを配置する方法を紹介します。
## ソフトウェアバージョン
例のステップにおけるこのドキュメントのソフトウェアバージョンは以下のとおりですが、実際に操作する時は、実際のソフトウェアのバージョンを基準にしてください。
- オペレーティングシステム：CentOS 7.5
- Nginxのバージョン：nginx 1.12.2

## nginxのインストール
購入完了後、CVMの詳細ページで【ログイン】をクリックするとCVMに直接ログインすることができます。自身のユーザー名とパスワードを入力した後、nginx環境の構築が開始されます。CVMインスタンスの作成方法については、[CVMインスタンスの購入と起動](https://cloud.tencent.com/document/product/213/4855)を参照してください。

```
# nginxのインストール：
yum -y install nginx  

# nginxバージョンの確認
nginx -v

# nginxインストールディレクトリの確認
rpm -ql nginx

# nginxの起動
service nginx start
```
現在、このCVMのパブリックネットワークIPアドレスにアクセスすると、nginxの配置が完了したことを示す以下のページが現れます。
![](https://main.qcloudimg.com/raw/c3d248fcfdfa45ad40c96cdca6769551.png)
nginxのデフォルトのルートディレクトリrootは`/usr/share/nginx/html`です。当社ではこのページの特殊性を表示するため、html下のindex.html静的ページを直接変更します。
```
vim /usr/share/nginx/html/index.html
# ページに以下のとおり入力
Hello nginx , This is rs-1!
URL is index.html
```

アプリケーション型CLBはRSのパスに基づきリクエストの転送を行うことができ、現在、/imageパスの下で静的ページを配置します。関連コマンドは以下のとおりです。
```
# ディレクトリimageの新規作成
mkdir /usr/share/nginx/html/image
cd /usr/share/nginx/html/image
vim index.html
# ページに以下のとおり入力
Hello nginx , This is rs-1!
URL is image/index.html
```

> 注：nginxのデフォルトポートは`80`です。ポートを変更したい場合は、構成ファイルを変更しnginxを再起動してください。

## nginxサービスの検証
CVMのパブリックネットワークIP + パスにアクセスし、配置済みの静的ページを表示することができる場合、nginxの配置が完了したことが証明されます。
rs-1のndex.htmlページ：
![](https://main.qcloudimg.com/raw/02c7524bedbd68ae25a36577a2fcb148.png)
rs-1の/image/index.htmlページ：
![](https://main.qcloudimg.com/raw/5663e2ee65aede1069a8ecf0d6003cc4.png)

