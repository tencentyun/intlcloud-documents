> CLS Loglistenerのインストール方法については、[LogListenerインストールガイド](https://cloud.tencent.com/document/product/614/17414)ドキュメントを参照し、[Loglistenerメカニズム](https://cloud.tencent.com/document/product/614/17415)について調べてください。

## 考えられる原因

Loglistenerが正しくインストールされない原因は以下のとおりです：
1.カーネルバージョンは64ビットしかサポートしていません。
2.インストール方法が正しくありません。
3.最新の機能はLoglistenerの上位バージョンに依存しています。


## 手順

1.カーネルのバージョンを確認してください。
Loglistenerインストールディレクトリのbinディレクトリにある実行可能なファイルは、Linux 64ビットカーネルのみをサポートします。**uname -a**コマンドを実行して、カーネルのバージョンがx86_64であるかどうかを確認してください。
2.インストール実行コマンドを確認してください。
Toolsディレクトリ内のスクリプトファイルはbashスクリプトですので、`sh install.sh`の実行方式はサポートされていません。`./install.sh`または`bash install.sh`の実行方式をお勧めします。[LogListenerインストールガイド](https://cloud.tencent.com/document/product/614/17414)ドキュメントに必ず従ってください。
3.Loglistenerのバージョンを確認します。
CLSの最新機能は、新しいバージョンのLoglistenerによって異なる場合がありますので、新しい機能の異常の場合は、[Loglistener最新バージョン](https://main.qcloudimg.com/raw/8656fcadd12ab9689674df09b510b52b/loglistener.2.2.2.tar.gz)をダウンロードしてください。
4.Loglistenerが正常にインストールされたことを確認します。
LogListenerプロセスが正常に動作しているかどうかを確認します。インストールディレクトリに入り、次のコマンドを実行します。
```shell
cd loglistener/tools && ./p.sh
```
通常の状況では、出力は次のようになります。
 ![](https://main.qcloudimg.com/raw/e256cf61689ead123251a8f9f3a753c9.png)
インストールディレクトリに入り、次のコマンドを実行して、構成項目が正しく構成されていて、ネットワークの状況が良好であるかどうかを確認してください。
```shell
cd loglistener/bin && ./check
```
通常の状況では、出力は次のようになります。
 ![](https://main.qcloudimg.com/raw/e7e85f139feb14b1aaa3353b2bafd5e1.png)
 上記のコマンドが正しく実行されたら、Loglistenerを正常にインストールできます。

