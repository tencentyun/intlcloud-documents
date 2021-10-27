## 概要

本ドキュメントはWindows Server 2012 R2 OS CVMを例として、Windows CVMでPHP 5.3および以前のバージョン、またPHP 5.3以降のバージョンの設定方法を説明します。


## 前提条件

- Windows CVMにログイン済みであり、かつそのCVMでIISロールの追加とインストールが完了していること。 詳細については[IISサービスのインストール](https://cloud.tencent.com/document/product/213/2755)をご参照ください。
- Windows CVMのパブリックIPを取得済みであること。詳細については、[パブリックIPアドレスの取得](https://cloud.tencent.com/document/product/213/17940)をご参照ください。

## 操作手順


### PHP 5.3およびそれ以前のバージョンのインストール[](id:jump1)

>! [PHP公式サイト](http://windows.php.net/download/)でのPHP 5.2以前のバージョンのインストールパッケージダウンロードの提供は終了しています。PHP 5.2以前のバージョンを使用する必要がある場合は、CVMで検索してダウンロードするか、あるいはローカルでダウンロードし、そのインストールパッケージをCVMにアップロードすることができます。ファイルをWindows CVMにアップロードする方法については、[Windows CVMにファイルをアップロード](https://cloud.tencent.com/document/product/213/2761)をご参照ください。次の操作手順はPHP 5.2.13バージョンを例としたものです。
> 
1. CVMでPHPのインストールパッケージを開きます。
2. インストール画面の指示に従って、【Next】をクリックします。
3. 「Web Server Setup」画面で、下図に示すように、【IIS FastCGI】を選択して、【Next】をクリックします。
![](https://main.qcloudimg.com/raw/c5fc89547b020e6ec943732d16186a7b.png)
4. インストールインターフェースの指示により、PHPをインストールします。
4. `C:/inetpub/wwwroot` ディレクトリの配下で、PHPファイルを作成します。例えば、下図に示すように、`hello.php` というファイルを作成します。
6. 新しく作成された `hello.php` ファイルに、下記の内容を記入して保存します。
```
	<?php
	echo "<title>Test Page</title>";
	echo "hello world";
	?>
```
7. OS画面で、ブラウザを開いて`http://Windows CVMのパブリックIPアドレス/hello.php` にアクセスして、環境設定が成功したかどうかを確認します。
以下のような画面が表示された場合、設定が成功しました。
![](https://main.qcloudimg.com/raw/0cdefc8707c4402e9ae5f9e6fa523ae1.png)


### PHP 5.3以降のバージョンのインストール[](id:jump)

PHP 5.3バージョンではインストールパッケージでインストールできなくなりました。zipファイルとdebug packの2種類の方法でをインストールできます。以下の操作は、zip ファイル方式により、Windows Server 2012 R2環境でPHPのインストールを例として説明します。

#### ソフトウェアのダウンロード

1. CVMで、[PHP 公式サイト](http://windows.php.net/download/) にアクセスして、下図に示すように、PHP zipのインストールパッケージをダウンロードします。
>! 
>- サーバーのOSがWindows Server 64bit (x64)の場合は、IISでPHPを実行する際、Non Thread Safeバージョンのx86インストールパッケージを選択する必要があります。
>- サーバーのOSがWindows Server 32bit (x86)の場合は、IISをApacheに変更し、Thread Safeバージョンのx86インストールパッケージを選択する必要があります。
>
![](https://main.qcloudimg.com/raw/b54dcb237ae24673cd592561ffc91bc0.png)
2. ダウンロードしたPHPのインストールパッケージの名前により、Visual C++ Redistributableのインストールパッケージをダウンロードしてインストールします。
PHPのインストールパッケージは、下表に示すように、該当するVisual C++ Redistributableのインストールパッケージをダウンロードしてインストールします。
<table>
<tr><th>PHPのインストールパッケージ名</th><th>Visual C++ Redistributable インストールパッケージのダウンロードURL</th></tr>
<tr><td>php-x.x.x-nts-Win32-VC16-x86.zip</td><td><a href="https://visualstudio.microsoft.com/zh-hans/downloads/">Microsoft Visual C++ Redistributable for Visual Studio 2019</a> x86バージョン</td></tr>
<tr><td>php-x.x.x-nts-Win32-VC15-x86.zip</td><td><a href="https://visualstudio.microsoft.com/zh-hans/vs/older-downloads/">Microsoft Visual C++ Redistributable for Visual Studio 2017</a> x86バージョン</td></tr>
<tr><td>php-x.x.x-nts-Win32-VC14-x86.zip</td><td><a href="https://www.microsoft.com/zh-cn/download/details.aspx?id=48145">Microsoft Visual C++ Redistributable for Visual Studio 2015</a> x86バージョン</td></tr>
</table>
 例えば、ダウンロードしたPHPインストールパッケージの名前が<code>PHP-7.1.30-nts-Win32-VC14-x86.zip</code>の場合は、Microsoft Visual C++ Redistributable for Visual Studio 2015 x86バージョンのインストールパッケージをダウンロードしてインストールする必要があります。

#### インストールと設定
1. ダウンロードしたPHP zipのインストールパッケージを解凍します。例えば、`C:\PHP` ディレクトリの配下で解凍します。
2. 下図に示すように、`C:\PHP` ディレクトリの配下に `php.ini-production` ファイルをコピーして、またそのファイルの拡張子を`.ini`（すなわち`php.ini`に名前を変更）に変更します。
![](https://main.qcloudimg.com/raw/52d9a2098fe73c8ddb41366b9732a000.png)
3. OS画面で、<img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> をクリックして、サーバーマネージャーを開きます。
4. サーバーマネージャーの左側のナビゲーションバーで、【IIS】をクリックします。
5. 右側のIIS管理画面で、下図に示すように、【サーバー】欄のサーバー名を右クリックして、【Internet Information Sevices (IIS)マネージャー】を選択します。
![](https://main.qcloudimg.com/raw/55e0b4c86de284050e5d810e92650337.png)
6. 開かれた「Internet Information Sevices (IIS)マネージャー」画面で、下図に示すように、左側のナビゲーションバーにあるサーバー名をクリックして、サーバーのホームページにアクセスします。
例えば、10_141_9_72のサーバー名をクリックして、10_141_9_72のホームページにアクセスします。
![](https://main.qcloudimg.com/raw/ab0f2306624452d4a3ab9fd5389d5b1d.png)
7. 【10_141_9_72 ホームページ】で、下図に示すように、【ハンドラマッピング】をダブルクリックして、「ハンドラマッピング」管理画面にアクセスします。
![](https://main.qcloudimg.com/raw/916a9cc9ce1270dbbfe6ddbb58f937e7.png)
8. 右側の【操作】欄で、【マッピングモジュールの追加】をクリックして、「マッピングモジュールの追加」画面を開きます。
9. 開かれた「マッピングモジュールの追加」画面で、下図に示すように、下記の情報を記入して、【OK】をクリックします。
![](https://main.qcloudimg.com/raw/a4d139682fc14204acd77ac3d1ea10eb.png)
主なパラメータ情報下記の通りです。
 - リクエストパス：`*.php` を記入します。
 - モジュール：「FastCgiModule」を選択します。
 - 実行可能ファイル：PHP zipインストールパッケージの中からphp-cgi.exeファイルを選択します。すなわち`C:\PHP\php-cgi.exe`です。
 - 名称：カスタマイズ可能。例えば、FastCGIを入力します。
10. 表示されたダイアログボックスで、【はい】をクリックします。 
11. 左側のナビゲーションバーにある10_141_9_72サーバー名をクリックして、10_141_9_72のホームページに戻ります。
12. 【10_141_9_72 ホームページ】で、下図に示すように、【デフォルトドキュメント】をダブルクリックして、「デフォルトドキュメント」管理画面に入ります。
![](https://main.qcloudimg.com/raw/6a896eeb929ae0104b1792e08bd895a6.png)
13. 右側の【操作】欄で、【追加】をクリックして、「デフォルトドキュメントの追加」画面を開きます。
14. 開かれた「デフォルトドキュメントの追加」画面で、下図に示すように、【名称】に`index.php`を記入して、【OK】をクリックします。
![](https://main.qcloudimg.com/raw/2d09af5d86755dd481b13efb0b3619a2.png)
15. 左側ナビゲーションバーにある10_141_9_72サーバー名をクリックして、10_141_9_72ホームページに戻ります。
16.【10_141_9_72 ホームページ】で、下図に示すように、【FastCGI 設定】をダブルクリックして、「FastCGI 設定」管理画面に入ります。
![](https://main.qcloudimg.com/raw/2a0693d3b837804b546fc690b4fb5cee.png)
17. 「FastCGI 設定」管理画面で、下図に示すように、FastCGI アプリケーションを選択して、【編集】をクリックします。
![](https://main.qcloudimg.com/raw/2038fa0df5c08820dc028fb3635fcda4.png)
18. 開かれた「FastCGI アプリケーションの編集」画面で、下図に示すように、【ファイルの変更を監視する】を`php.ini`ファイルのパスとして設定します。
![](https://main.qcloudimg.com/raw/b1aa458607934a5331b51e22762d0dec.png)
19. `C:\inetpub\wwwroot` ディレクトリの配下に、下図に示すように、PHPファイルを作成します。例えば、`index.php` ファイルを作成します。
20. 新規作成された`index.php`ファイルに、以下の内容を入力して保存します。
```
<?php
phpinfo();
?>
```
21. OS画面で、ブラウザを開いて `http://localhost/index.php` にアクセスして、環境設定が成功したかどうかを確認します。
以下のような画面が表示された場合、設定が成功しました。
![](https://main.qcloudimg.com/raw/ccd08fd9af6afe4ee2c3bf38f9e581b9.png)

