ここではCentOSシステムにNginxプロジェクトをデプロイする方法について詳細にご説明します。Tencent Cloudのご利用を開始したばかりの個人ユーザーの方向けの内容となります。
## ソフトウェアバージョン
ここで例に挙げる手順で使用するソフトウェアバージョンは次のとおりです。実際の操作の際は、お使いのソフトウェアバージョンに準じてください。
- OS：CentOS 7.5
- Nginxバージョン：Nginx 1.16.1

## Nginxのインストール
1. ご購入の完了後、CVMの詳細ページで【ログイン】をクリックすると、CVMに直接ログインできます。ご自身のユーザー名とパスワードを入力すると、Nginx環境の構築を開始できます。CVMインスタンスの作成方法に関しては、[CVMインスタンスの作成](https://cloud.tencent.com/document/product/213/4855)をご参照ください。
```
# Nginxのインストール：
yum -y install nginx  
# Nginxバージョンの確認
nginx -v
# Nginxインストールディレクトリの確認
rpm -ql nginx
# Nginxの起動
service nginx start
```
2. このCVMのパブリックIPアドレスにアクセスし、以下のページが表示された場合は、Nginxのデプロイが完了しています。
![](https://main.qcloudimg.com/raw/8807f9fd819eb93d46c5646ba3572fac.png)
3. Nginxのデフォルトルートディレクトリrootは`/usr/share/nginx/html`であり、`html`下の`index.html`静的ページを直接変更し、このページの特殊性を表します。関連の操作は次のとおりです。
   1. 次のコマンドを実行し、html下のindex.html静的ページに進みます。
```bash
vim /usr/share/nginx/html/index.html
```
   2. 「i」を押して編集モードに進み、`<body></body>`タグ内に次を入力します。
```bash
# <body>の下に直接入力することをお勧めします
Hello nginx , This is rs-1!
URL is index.html
```
   ![](https://main.qcloudimg.com/raw/02e833dd08a6873d5d015f4531d24645.png)
   3. 「Esc」を押し、`:wq`を入力して編集を保存します。
4. CLB（旧「アプリケーション型CLB」）はバックエンドサーバーのパスに基づいてリクエストを転送し、`/image`パスに静的ページをデプロイすることができます。関連の操作は次のとおりです。
   1. 次のコマンドを順に実行し、ディレクトリ`image`を新規作成してこのディレクトリに進みます。
```bash
mkdir /usr/share/nginx/html/image
cd /usr/share/nginx/html/image
```
   2. 次のコマンドを実行し、`image`ディレクトリ下に`index.html`静的ページを作成します。
```
vim index.html
```
   3. 「i」を押して編集モードに進み、ページ内に次を入力します。
```bash
Hello nginx , This is rs-1!
URL is image/index.html
```
   4. 「Esc」を押し、`:wq`を入力して編集を保存します。
>!Nginxのデフォルトポートは`80`です。ポートを変更したい場合は、設定ファイルを変更してからNginxを再起動してください。

## Nginxサービスの検証
CVMのパブリックIP + パスにアクセスし、デプロイ済みの静的ページが表示された場合は、Nginxのデプロイに成功したことを表しています。
- rs-1のindex.htmlページ：
![](https://main.qcloudimg.com/raw/ede62fecd2106869d53bf142ad51903e.png)
- rs-1の/image/index.htmlページ：
![](https://main.qcloudimg.com/raw/f0f87422487177722291c2260cac9d35.png)
