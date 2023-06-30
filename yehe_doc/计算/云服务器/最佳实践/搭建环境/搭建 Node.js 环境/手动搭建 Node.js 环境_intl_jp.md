## 概要
ここでは、Tencent CloudのCloud Virtual Machine(CVM)にNode.js環境を手動でデプロイする方法と、サンプルプロジェクトを作成する方法についてご説明します。

手動でNode.js環境を構築するには、[CentOS環境でYUMを介したソフトウェアのインストール](https://intl.cloud.tencent.com/document/product/213/2046)などの一般的なLunuxコマンドに精通している必要があります。また、インストールされているソフトウェアの使い方や設定、互換性について十分に理解しておく必要があります。
<dx-alert infotype="explain" title="">
Tencent Cloudでは、クラウドマーケットのイメージ環境を通じてNode.js環境をデプロイすることをお勧めしています。Node.js環境を手動で構築すると時間がかかる可能性があります。
</dx-alert>



## ソフトウェアのバージョン
Node.js環境を構築するために使用するソフトウェアのバージョンと構成について、以下にご説明します。
- オペレーティングシステム：Linuxシステム。ここでは、CentOS 7.6を例とします。
- Node.js：JavaScriptの実行環境です。ここでは、Node.js 10.16.3とNode.js 6.9.5を例とします。
- npm：Node.jsノードバージョンマネージャーで、複数のNode.jsバージョンを管理します。ここでは、npm 6.9.0を例とします。

##  前提条件
Linux CVMを購入済みであること。

## 操作手順
### ステップ1：Linuxインスタンスにログインする
[標準的な方法を使用してLinuxインスタンスにログインする（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)。実際の操作方法に応じて、他のログイン方法を選択することもできます：
- [リモートログインソフトウェアを使用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32502)
- [SSHキーを使用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32501)


### 手順2：Node.jsのインストール
1. 次のコマンドを実行して、Node.js Linux 64ビットバイナリーインストールパッケージをダウンロードします。
```
wget https://nodejs.org/dist/v10.16.3/node-v10.16.3-linux-x64.tar.xz
```
<dx-alert infotype="explain" title="">
詳細なインストール情報については、[Node.js公式サイト](https://nodejs.org/zh-cn/download/)をご覧ください。
</dx-alert>
2. 次のコマンドを実行して、インストールパッケージを解凍します。
```
tar xvf node-v10.16.3-linux-x64.tar.xz
```
3. 次のコマンドを順に実行して、シンボリックリンクを作成します。
```
ln -s /root/node-v10.16.3-linux-x64/bin/node /usr/local/bin/node
```
```
ln -s /root/node-v10.16.3-linux-x64/bin/npm /usr/local/bin/npm
```
シンボリックリンクの作成に成功すると、CVMの任意のディレクトリでnodeやnpmコマンドを使用できるようになります。
4. 次のコマンドを順に実行して、Node.jsとnpmのバージョン情報を確認します。
```
node -v
```
```
npm -v
```

### 手順3：Node.jsの複数バージョンのインストール（オプション）


<dx-alert infotype="explain" title="">
この手順では、npm経由で複数のバージョンのNode.jsをインストールし、すばやく切り替えられるようにします。開発者向けで、実際のニーズに応じてインストールすることができます。
</dx-alert>


1. 次のコマンドを実行して、gitをインストールします。
```
yum install -y git
```
2. 次のコマンドを実行して、NVMのソースコードをダウンロードし、最新バージョンをチェックします。
```
git clone git://github.com/cnpm/nvm.git ~/.nvm && cd ~/.nvm && git checkout `git describe --abbrev=0 --tags`
```
3. 次のコマンドを実行して、NVM環境変数を設定します。
```
echo ". ~/.nvm/nvm.sh" >> /etc/profile
```
4. 次のコマンドを実行して、環境変数を読み込みます。
```
source /etc/profile
```
4. 次のコマンドを実行して、Node.jsのすべてのバージョンを確認します。
```
nvm list-remote
```
5. 次のコマンドを順に実行して、複数のバージョンのNode.jsをインストールします。
```
nvm install v6.9.5
```
```
nvm install v10.16.3
```
6. 次のコマンドを実行して、インストール済みのNode.jsのバージョンを確認します。
```
nvm ls
```
次のような結果が返された場合、インストールに成功したことを示し、現在の使用バージョンはNode.js 10.16.3です。
![](https://main.qcloudimg.com/raw/a315fe51314357fb44ec725f20c101ed.png)
7. 次のコマンドを実行して、使用するNode.jsのバージョンを切り替えます。
```
nvm use v6.9.5
```
実行結果は下図に示すように：
![](https://main.qcloudimg.com/raw/817fd96fef77f818e65ce41a3723e5bc.png)

### 手順4：Node.jsプロジェクトの作成
1. 次のコマンドを順に実行して、ルートディレクトリにプロジェクトファイル`index.js`を作成します。
```
cd ~
```
```
vim index.js
```
2. **i**を押して編集モードに切り替え、以下の内容を`index.js`ファイルに入力します。
```
const http = require('http');
const hostname = '0.0.0.0';
const port = 7500;
const server = http.createServer((req, res) => { 
    res.statusCode = 200;
    res.setHeader('Content-Type', 'text/plain');
    res.end('Hello World\n');
}); 
server.listen(port, hostname, () => { 
    console.log(`Server running at http://${hostname}:${port}/`);
});
```
<dx-alert infotype="explain" title="">
ここでは、プロジェクトファイル`index.js`にポート番号7500を使用していますが、実際のニーズに応じてポート番号を変更することができます。
</dx-alert>
3. **Esc**を押して**:wq**と入力し、**Enter**を押してファイルを保存し、戻ります。
4. 次のコマンドを実行して、Node.jsプロジェクトを実行します。
```
node index.js
```
5. ローカルブラウザで以下のアドレスにアクセスし、プロジェクトが正常に実行されていることを確認します。
```
http://CVMインスタンスのパブリックIP:設定済みのポート番号
```
次のような結果が表示された場合、Node.js環境の構築は成功しています。
![](https://main.qcloudimg.com/raw/5b72798dc9e988eee8d8186055aa45e9.png)


## よくあるご質問
CVMの使用中に問題が発生した場合は、下記のドキュメントを参照しながら実際状況に合わせ分析した上で問題を解決することが可能です。
- CVMのログインに関する問題は、[パスワードとキー](https://intl.cloud.tencent.com/document/product/213/18120)、[ログインとリモート接続](https://intl.cloud.tencent.com/document/product/213/17278)ドキュメントをご参照ください。
- CVMのネットワークに関する問題は、 [IPアドレス](https://intl.cloud.tencent.com/document/product/213/17285)、[ポートとセキュリティグループ](https://intl.cloud.tencent.com/document/product/213/2502)ドキュメントをご参照ください。
- CVMのハードディスクに関する事項については、[システムディスクとデータディスク](https://intl.cloud.tencent.com/zh/document/product/213/17351)をご参照ください。

