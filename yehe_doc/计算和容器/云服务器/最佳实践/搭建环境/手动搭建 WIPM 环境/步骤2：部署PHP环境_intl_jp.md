本ドキュメントでは、Windows CVMのPHP設定について説明します。詳細については、必要に応じて、[PHP 5.3 以降のバージョンのインストール](#jump)および[PHP 5.3以前のバージョンのインストール](#jump1) をご参照ください。
## 前提条件
Windows CVMでPHPを設定するには、IISロールの追加とインストールを完了する必要があります。詳細については、ドキュメント[IISのインストールと設定](/doc/product/213/2755)をご参照ください。
/doc/product/213/2755) 。

## PHP 5.3 以降のバージョンのインストール
<span id="jump">  </span>
PHPバージョン5.3以上の場合、インストールパッケージモードはキャンセルされ、インストールはzipファイルまたはdebug pack を介してのみ実行されます。 次の例は、 Windows Server 2012 R2 環境でのzipインストールを示しています。

### ソフトウェアのダウンロード

 1. CVMからPHP zipのインストールパッケージをダウンロードします。(ダウンロードリンク：http://windows.php.net/download/ ）
>注意事項：
>IISで実行する場合、Non Thread Safe（NTS）x86パッケージを選択する必要があります。Windows Server 32ビット（x64）でPHPのx64パッケージを選択する必要がある場合は、IISを選択できません。 この場合、代替オプションとしてApacheを使用できます。

	次のようなインストールパッケージを選択します：
  ![](//mc.qcloudimg.com/static/img/d02eb264ae4d5fbaaf8fd01a08433c61/image.png)
  ![](//mc.qcloudimg.com/static/img/f719e6893f1addd0b260d0c740e4e0ba/image.png)
  ![](//mc.qcloudimg.com/static/img/24ca3df57de6195ad45adabad1c5dc13/image.png)

 2. PHP 5.3以上のバージョンのインストールは、Visual C++ Redistributable Updateに依存しています。次の表に示すような対応関係を参照して、ダウンロードしたPHPインストールパッケージ名に従って、VC Updateのインストーラーをダウンロードしてインストールします。

| PHPインストールパッケージ名 | Visual C++ Redistributableインストールパッケージのダウンロードアドレス |
|---------|---------|---------|
| php-x.x.x-nts-Win32-VC14-x86.zip | [Visual C++ Redistributable for Visual Studio 2015](https://www.microsoft.com/zh-cn/download/details.aspx?id=48145) |
| php-x.x.x-nts-Win32-VC11-x86.zip | [Visual C++ Redistributable for Visual Studio 2012 Update 4](https://www.microsoft.com/zh-cn/download/details.aspx?id=30679) |
| php-x.x.x-nts-Win32-VC9-x86.zip | [Microsoft Visual C++ 2008 SP1 Redistributable Package (x86)](https://www.microsoft.com/zh-cn/download/details.aspx?id=5582) |

  ダウンロードしたPHPインストールパッケージが下図に示すような場合：
![](//mccdn.qcloud.com/static/img/974ac7192d8f10236fcc27bfd54b8aed/image.png)

表の1行目に示されている対応関係に従ってVS 2015バージョンのインストールパッケージをダウンロードし、次の2つの`.exe`形式のファイルをダウンロードしてインストールします。
![](//mc.qcloudimg.com/static/img/7128c0b621f2534cecddd23b6f3efdb9/image.png)


### インストールと設定
 1. PHP zipインストールパッケージを解凍し（この例では、`C:\PHP`に解凍します）、`php.ini-production`をコピーして、名前を `php.ini`に変更します。下記の図に示すように：
![](//mc.qcloudimg.com/static/img/1be9b1771a93852aff909b08159a5b79/image.png)

 2. 【サーバーマネージャー】-【IIS】をクリックし、ローカルIISで、を右クリックしてIISマネージャーを選択します。
![](//mc.qcloudimg.com/static/img/f0387eeb456b7d60e8a5b601cbd3c6b0/image.png)

	左側のホスト名（IP）をクリックしてホームページに移動し、【ハンドラーマッピング】をダブルクリックします：
![](//mc.qcloudimg.com/static/img/898aa0d2f61c467d333601b75c57704c/image.png)

	右側の【モジュールマッピングの追加】ボタンをクリックし、ポップアップボックスに次の情報を記入して、【OK】をクリックして保存します：
![](//mc.qcloudimg.com/static/img/6f0fd95475a7c00a5779592d15a7753e/image.png)

	>**注意事項：**
	>php-cgi.exeを実行可能ファイルとして選択できない場合は、選択したファイルの拡張子を.exe：![](//mc.qcloudimg.com/static/img/d749a9fe4c77f6ea7b55afd8fd37e808/image.png)に変更してください

 3. 左側のホスト名（IP）をクリックしてホームページに移動し、【デフォルトドキュメント】をダブルクリックします：
![](//mc.qcloudimg.com/static/img/b5861a95bf6aafd8f4bcaf1c12e9f9be/image.png)

	右側の【追加】ボタンをクリックして、`index.php`という名称のデフォルトドキュメントを追加します：
![](//mc.qcloudimg.com/static/img/6b2543227fec95d1b9bed5f4260a86bb/image.png)

 4. 左側のホスト名（IP）をクリックしてホームページに移動し、【 FastCGI 設定】をダブルクリックします：
![](//mc.qcloudimg.com/static/img/aa23422c038b1024354f01ed0cb3ab73/image.png)

	右側の【編集】ボタンをクリックし、【ファイルの変更を監視】で `php.ini` パスを選択します：
![](//mc.qcloudimg.com/static/img/b4f1ec7d39519dc7d2e89d52ed8a1a87/image.png)
![](//mc.qcloudimg.com/static/img/a2acbed50587552c6ef7ed796b82eb36/image.png)

 5.  `C:\inetpub\wwwroot` ディレクトリにPHPファイル `index.php` を作成し、以下の内容を記入します：
```
<?php
phpinfo();
?>
```

 6. CVMのブラウザーで `http://localhost/index.php`  にアクセスして、環境が正常に構成されているかどうかを確認します。 画面が次のように表示される場合、構成が正常に完了したことを示しています。
![](//mc.qcloudimg.com/static/img/46eec848975e77e770569eb5d8849d37/image.png)



## PHP 5.3以前のバージョンのインストール
<span id="jump1">  </span>
>注意事項：
> PHP 5.3以前のバージョンは、公式のダウンロードアドレスhttp://windows.php.net/download/から入手できなくなりました。PHP5.3以前のバージョンが引き続き必要な場合は、ローカルにダウンロードしてCVMにファイルをアップロードするか、CVMネットワークで検索してください。ファイルのアップロードの詳細については、[こちら](https://cloud.tencent.com/document/product/213/2761) をご覧ください。

 1. CVMでPHPのインストールパッケージを開きます。

 2. Webサービス (Web Server Setup) を選択する場合、「IIS FastCGI」を選択し、下記の図に示すように：
![](//mc.qcloudimg.com/static/img/ef2f5959779cd733934d11ecbcb4a7f5/image.png)

 3. インストールインターフェースの指示に従って、PHPをインストールします。

 4. `C:/inetpub/wwwroot`ディレクトリで、PHPファイル `hello.php`を作成します。下記の図に示すように：
![](//mc.qcloudimg.com/static/img/31d992849b04c1bc76c0d4ca61ab8a4b/image.png)

	次の内容が`hello.php` ファイルに書き込まれます。

	```
	<?php
	echo "<title>Test Page</title>";
	echo "hello world";
	?>
	```

 5.ブラウザを介してWindows CVMのパブリックネットワークIPにアクセスして、環境が正常に構成されているかどうかを確認します。画面が次のように表示される場合、構成が正常に完了したことを示しています。
![](//mc.qcloudimg.com/static/img/89cebc1127f5c76790c2a9bf3be9fd1f/image.png)


