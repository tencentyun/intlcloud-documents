## ユースケース

このドキュメントでは、Windows Server 2012 R2 OSを実行するCVMを例として、Windows CVMでPHP 5.3以前のバージョンまたは5.3以降のバージョンを設定する方法について説明します。


## 前提条件

- Windows CVMにログインし、またCVMにIISロールの追加およびインストールを完了しました。詳細について、[IISのインストールと設定](https://intl.cloud.tencent.com/document/product/213/2755)をご参照ください。
- Windows CVMのパブリックIPアドレスを取得しました。詳細について、 [パブリックIPアドレスの取得](https://intl.cloud.tencent.com/document/product/213/17940) をご参照ください。

## 操作手順

<span id="jump1"></span>
### PHP 5.3および以前のバージョンのインストール

> [PHP 公式サイト](http://windows.php.net/download/) は現在、PHP 5.2より前のバージョンのインストールパッケージを提供していません。PHP 5.2より前のバージョンを利用したい場合は、お客様自らCVMで検索してダウンロードするか、またはローカルでダウンロードしてから、CVMにアップロードすることもできます。Windows CVMにファイルをアップロードする方法については、[Windows CVMへのファイルのアップロード](https://intl.cloud.tencent.com/document/product/213/2761) をご参照ください。以下の操作手順はPHP 5.2.13 バージョンを例として説明します。
> 
1. CVMでPHPのインストールパッケージを開きます。
2. インストール画面の指示に従って、【Next】をクリックします。
3. 「Web Server Setup」画面で、下図に示すように、【IIS FastCGI】を選択して、【Next】をクリックします。
![](https://main.qcloudimg.com/raw/c5fc89547b020e6ec943732d16186a7b.png)
4. プロンプトに従ってPHPのインストールを完了します。
5. `C:/inetpub/wwwroot` ディレクトリの配下で、PHPファイルを作成します。例えば、下図に示すように、`hello.php` というファイルを作成します。

6. 新しく作成された `hello.php` ファイルに、下記の内容を記入して保存します。
```
	<?php
	echo "<title>Test Page</title>";
	echo "hello world";
	?>
```
7. デスクトップでブラウザーを開き、`http://Windows CVMのパブリックIPアドレス/hello.php` にアクセスして、環境設定が成功したかどうかを確認します。
以下のような画面が表示された場合、設定が成功しました。
![](https://main.qcloudimg.com/raw/0cdefc8707c4402e9ae5f9e6fa523ae1.png)

<span id="jump"></span>
### PHP 5.3以降のバージョンのインストール

PHP 5.3以降のバージョンにはインストールパッケージがなく、zipファイルまたはdebug packを使用してインストールされます。以下の操作は、zipファイルを使用してWindows Server 2012 R2環境にPHPをインストールする方法を示しています。

#### ソフトウェアのダウンロード

1. CVMで、[PHP 公式サイト](http://windows.php.net/download/) にアクセスして、下図に示すように、PHP zipのインストールパッケージをダウンロードします。
> IISでPHPを実行するには、Non Thread Safeバージョンのx86インストールパッケージを選択する必要があります。ご利用のサーバーはWindows Server 32bit (x64)OSの場合、IISをApacheに置き換え、 Thread Safeバージョンのx64インストールパッケージを選択する必要があります。
>
![](https://main.qcloudimg.com/raw/b54dcb237ae24673cd592561ffc91bc0.png)
2. ダウンロードしたPHPインストールパッケージの名前に基づいて、Visual C++ Redistributableインストールパッケージをダウンロードしてインストールします。
次の表に、PHPインストールパッケージ用にダウンロードしてインストールする必要があるVisual C++ Redistributableインストールパッケージを示します。
<table>
<tr><th>PHPインストールパッケージ名</th><th>Visual C++ Redistributable インストールパッケージのダウンロードアドレス</th></tr>
<tr><td>php-x.x.x-nts-Win32-VC16-x86.zip</td><td><a href="https://visualstudio.microsoft.com/zh-hans/downloads/">Microsoft Visual C++ Redistributable for Visual Studio 2019</a></td></tr>
<tr><td>php-x.x.x-nts-Win32-VC15-x86.zip</td><td><a href="https://visualstudio.microsoft.com/zh-hans/vs/older-downloads/">Microsoft Visual C++ Redistributable for Visual Studio 2017</a></td></tr>
<tr><td>php-x.x.x-nts-Win32-VC14-x86.zip</td><td><a href="https://www.microsoft.com/zh-cn/download/details.aspx?id=48145">Microsoft Visual C++ Redistributable for Visual Studio 2015</a></td></tr>
</table>
 例えば、ダウンロードしたPHPインストールパッケージの名前が<code>PHP-7.1.30-nts-Win32-VC14-x86.zip</code> の場合、Microsoft Visual C++ Redistributable for Visual Studio 2015のインストールパッケージをダウンロードしてインストールする必要があります。

#### インストールと設定
1. ダウンロードしたPHPインストールパッケージをC：\ PHPディレクトリに解凍します。
2. 下図に示すように、`C:\PHP` ディレクトリの配下に `php.ini-production` ファイルをコピーして、またそのファイルの拡張子を`.ini`（すなわち`ファイル名をphp.iniに変更）に変更します。
![](https://main.qcloudimg.com/raw/52d9a2098fe73c8ddb41366b9732a000.png)
3. OS画面で、<img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> をクリックして、サーバーマネージャーを開きます。
4. 左側のナビゲーションバーで、【IIS】をクリックします。
5. 右側のIIS管理ウィンドウで、下図に示すように、【サーバー】欄のサーバー名を右クリックして、【インターネットインフォメーション サービス(IIS) マネージャー】を選択します。
![](https://main.qcloudimg.com/raw/55e0b4c86de284050e5d810e92650337.png)
6. 開かれた「インターネットインフォメーションサービス(IIS) マネージャー」ウィンドウで、下図に示すように、左側のナビゲーションバーにあるサーバー名をクリックして、サーバーのホームページにアクセスします。
例えば、10_141_9_72サーバー名をクリックして、10_141_9_72ホームページにアクセスします。
![](https://main.qcloudimg.com/raw/ab0f2306624452d4a3ab9fd5389d5b1d.png)
7. 【10_141_9_72 ホームページ】で、下図に示すように、【ハンドラマッピング】をダブルクリックして、「ハンドラマッピング」管理画面にアクセスします。
![](https://main.qcloudimg.com/raw/916a9cc9ce1270dbbfe6ddbb58f937e7.png)
8. 右側の【操作】パネルの【モジュールマップの追加】をクリックして、「モジュールマップの追加」ウィンドウを開きます。
9. 開かれた「モジュールマップの追加」画面で、下図に示すように、下記の情報を記入して、【OK】をクリックします。
![](https://main.qcloudimg.com/raw/a4d139682fc14204acd77ac3d1ea10eb.png)
主なパラメータ情報下記の通りです。
 - リクエストパス：`*.php` を記入します。
 - モジュール：「FastCgiModule」を選択します。
 - 実行可能ファイル：PHPインストールパッケージのphp-cgi.exeファイル、つまりC：\ PHP \ php-cgi.exeを選択します。
 - 名称：FastCGIなどのカスタム名を入力します。
10. 表示されたダイアログボックスで、【OK】をクリックします。 
11. 左側のナビゲーションバーにある10_141_9_72サーバー名をクリックして、10_141_9_72のホームページに戻ります。
12. 【10_141_9_72 ホームページ】で、下図に示すように、【既定のドキュメント】をダブルクリックして、「既定のドキュメント」管理画面に入ります。
![](https://main.qcloudimg.com/raw/6a896eeb929ae0104b1792e08bd895a6.png)
13. 既定のドキュメントの設定画面が表示されます。ウィンドウ右側のエリアの【追加】リンクをクリックをクリックして、「既定のドキュメントを追加」ウィンドウを開きます。
14. 　[既定のドキュメントを追加]ダイアログが表示されますので、既定のドキュメントに追加したいファイル名を指定します。今回は"index.php"を追加します。テキストボックスに入力ができたらダイアログの【OK】ボタンをクリックします。下図に示すように、
![](https://main.qcloudimg.com/raw/2d09af5d86755dd481b13efb0b3619a2.png)
15. 左側ナビゲーションバーにある10_141_9_72サーバー名をクリックして、10_141_9_72ホームページに戻ります。
16.【10_141_9_72 ホームページ】で、下図に示すように、【FastCGI 設定】をダブルクリックして、「FastCGI 設定」管理画面に入ります。
![](https://main.qcloudimg.com/raw/2a0693d3b837804b546fc690b4fb5cee.png)
17. 「FastCGI 設定」管理画面で、下図に示すように、FastCGI アプリケーションを選択して、【編集】をクリックします。
![](https://main.qcloudimg.com/raw/2038fa0df5c08820dc028fb3635fcda4.png)
18. 開かれた「FastCGI アプリケーションの編集」画面で、下図に示すように、【ファイルへの変更の監視】を`php.ini`ファイルパスに設定します。
![](https://main.qcloudimg.com/raw/b1aa458607934a5331b51e22762d0dec.png)
19. `C:\inetpub\wwwroot` ディレクトリの配下に、下図に示すように、`index.php` などのPHPファイルを作成します。
20. 新規作成された`index.php`ファイルに、以下の内容を入力して保存します。
```
<?php
phpinfo();
?>
```
21.デスクトップでブラウザーを開き、 `http://localhost/index.php`にアクセスして、環境設定が成功したかどうかを確認します。
以下のような画面が表示された場合、設定が成功しました。
![](https://main.qcloudimg.com/raw/ccd08fd9af6afe4ee2c3bf38f9e581b9.png)

