## ユースケース

本ドキュメントはWindows Server 2012 R2 OS CVMを例として、Windows CVMでPHP 7.0及び以前のバージョン、またPHP 7.0以降のバージョンの設定方法をご紹介します。


## 前提条件

- Windows CVMにログインし、またCVMにIIS ロールの追加及びインストールしました。詳細について、[IISのインストールと設定](https://intl.cloud.tencent.com/document/product/213/2755)をご参照ください。
- Windows CVMのパブリックIPアドレスを取得済みです。詳細について、 [パブリックIPアドレスの取得](https://intl.cloud.tencent.com/document/product/213/17940) をご参照ください。

## 操作手順

<span id="jump1"></span>
### PHP 7.0及び以前のバージョンをインストールする

> [PHP 公式サイト](http://windows.php.net/download/) はすでにPHP 7.0及び以前のバージョンのインストールパッケージのダウンロードサービスをご提供していません。PHP 7.0及び以前のバージョンを利用したい場合は、お客様自らCVMで検索してダウンロードするか、またはローカルでダウンロードしてから、CVMにアップロードすることもできます。どのように Windows CVMにファイルをアップロードするかについては、[Windows CVMへのファイルアップロード](https://intl.cloud.tencent.com/document/product/213/2761) をご参照ください。以下の操作手順はPHP 5.2.13 バージョンを例として説明します。
> 
1. CVMでPHPのインストールパッケージを開きます。
2. インストールインターフェースの指示により、【Next】をクリックします。
3. 「Web Server Setup」インターフェースで、【IIS FastCGI】を選択して、【Next】をクリックします。下図に示すように：
![](https://main.qcloudimg.com/raw/c5fc89547b020e6ec943732d16186a7b.png)
4. インストールインターフェースの指示により、PHPをインストールします。
5. `C:/inetpub/wwwroot` ディレクトリの配下で、PHPファイルを作成します。例えば、`hello.php` のようなファイルを作成します。
6. 新しく作成された `hello.php` ファイルに、下記の内容を記入して保存します。
```
	<?php
	echo "<title>Test Page</title>";
	echo "hello world";
	?>
```
7. OSインターフェースで、ブラウザを開いて`http://Windows CVMのパブリックIPアドレス/hello.php` にアクセスして、環境設定が成功したかどうかを確認します。
以下のような画面が表示された場合、設定が成功しました：
![](https://main.qcloudimg.com/raw/0cdefc8707c4402e9ae5f9e6fa523ae1.png)

<span id="jump"></span>
### PHP 7.0以降のバージョンをインストールする

PHP 7.0以降のバージョンはzipファイルとdebug packの二種類の方式を通してインストールできます。以下の操作は、zip ファイル方式により、Windows Server 2012 R2環境でPHPのインストールを例として説明します。

#### ソフトウェアのダウンロード

1. CVMで、[PHP 公式サイト](http://windows.php.net/download/) にアクセスして、PHP zipのインストールパッケージをダウンロードします。下図に示すように：
> IISでPHPを実行する際に、Non Thread Safeバージョンのx86インストールパッケージを選択する必要があります。お客様がWindows Server 32bit (x64)OSでPHPをインストールしたい場合は、IISをApacheに置き換え、Non Thread Safeバージョンのx64インストールパッケージを選択する必要があります。
>
![](https://main.qcloudimg.com/raw/b54dcb237ae24673cd592561ffc91bc0.png)
2. ダウンロードしたPHPのインストールパッケージの名前により、 Visual C++ Redistributableのインストールパッケージをダウンロードしてインストールします。
PHPのインストールパッケージは、該当するVisual C++ Redistributableのインストールパッケージをダウンロードしてインストールします。下表に示すように：
<table>
<tr><th>PHPのインストールパッケージ名</th><th>Visual C++ Redistributable インストールパッケージのダウンロードURL</th></tr>
<tr><td>php-x.x.x-nts-Win32-VC16-x86.zip</td><td><a href="https://visualstudio.microsoft.com/zh-hans/downloads/">Microsoft Visual C++ Redistributable for Visual Studio 2019</a></td></tr>
<tr><td>php-x.x.x-nts-Win32-VC15-x86.zip</td><td><a href="https://visualstudio.microsoft.com/zh-hans/vs/older-downloads/">Microsoft Visual C++ Redistributable for Visual Studio 2017</a></td></tr>
<tr><td>php-x.x.x-nts-Win32-VC14-x86.zip</td><td><a href="https://www.microsoft.com/zh-cn/download/details.aspx?id=48145">Microsoft Visual C++ Redistributable for Visual Studio 2015</a></td></tr>
</table>
 仮にダウンロードしたPHPのインストールパッケージの名前は <code>PHP-7.0.6-nts-Win32-VC14-x86.zip</code> とする場合は、Microsoft Visual C++ Redistributable for Visual Studio 2015のインストールパッケージをダウンロードして、インストールする必要があります。

#### インストールと設定
1. ダウンロードしたPHP zipのインストールパッケージを解凍します。例えば、`C:\PHP` ディレクトリの配下で解凍します。
2. `C:\PHP` ディレクトリの配下に `php.ini-production` ファイルをコピーして、またそのファイルの拡張子を `.ini`（ `php.ini` にリネームする）に変更します。
3. OSインターフェースで、<img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> をクリックして、サーバーマネージャーを開きます。
4. サーバーマネージャーの左側のナビゲーションバーで、【IIS】をクリックします。
5. 右側のIIS管理ウィンドウで、【サーバー】欄のサーバー名を右クリックして、【Internet Information Sevices (IIS)マネージャー】を選択します。
6. 開いた「Internet Information Sevices (IIS)マネージャー」ウィンドウで、左側のナビゲーションバーにあるサーバー名をクリックして、サーバーのホームページにアクセスします。下図に示すように：
例えば、10_141_9_72のサーバー名をクリックして、10_141_9_72のホームページにアクセスします。
7. 【10_141_9_72 ホームページ】で、【ハンドラマッピング】をダブルクリックして、「ハンドラマッピング」管理インターフェースにアクセスします。
8. 右側の【操作】欄で、【マッピングモジュールの追加】をクリックして、「マッピングモジュールの追加」 ウィンドウを開きます。
9. 開いた「マッピングモジュールの追加」ウィンドウで、下記の情報を記入して、【OK】をクリックします。
主なパラメータ情報下記の通り：
 - リクエストパス：`*.php` を記入します。
 - モジュール：「FastCgiModule」を選択します。
 - 実行可能ファイル：PHP zipインストールパッケージの中に、php-cgi.exeファイルを選択します。すなわち `C:\PHP\php-cgi.exe`です。
 - 名称：カスタマイズです。例えば、FastCGIを入力します。
10. 表示されるダイアログボックスで、【はい】をクリックします。 
11. 左側のナビゲーションバーにある10_141_9_72サーバー名をクリックして、10_141_9_72ホームページに戻ります。
12. 【10_141_9_72 ホームページ】で、【デフォルトドキュメント】をダブルクリックして、「デフォルトドキュメント」管理インターフェースにアクセスします。
13. 右側の【操作】欄で、【追加】をクリックして、「デフォルトドキュメントの追加」ウィンドウを開きます。
14. 開いた「デフォルトドキュメントの追加」ウィンドウで、【名称】に `index.php` を記入して、【OK】をクリックします。
15. 左側のナビゲーションバーにある10_141_9_72サーバー名をクリックして、10_141_9_72ホームページに戻ります。
16.【10_141_9_72 ホームページ】で、【FastCGI 設定】をダブルクリックして、「FastCGI 設定」管理インターフェースにアクセスします。
16. 「FastCGI 設定」管理インターフェースで、FastCGI アプリケーションを選択して、【編集】をクリックします。
17. 開いた「FastCGI アプリケーションの編集」ウィンドウで、【ファイルの変更を監視する】を `php.ini` ファイルのパスとして設定します。
19. `C:\inetpub\wwwroot` ディレクトリの配下に、、PHPファイルを作成します。例えば、 `index.php` のようなファイルを作成します。下図に示すように：
20. 新しく作成された `index.php` ファイルに、以下の内容を記入して保存します。
```
<?php
phpinfo();
?>
```
21. OSインターフェースで、ブラウザを開いて `http://localhost/index.php` にアクセスして、環境設定が成功したかどうかを確認します。
以下のような画面が表示された場合、設定が成功しました：
![](https://main.qcloudimg.com/raw/ccd08fd9af6afe4ee2c3bf38f9e581b9.png)

