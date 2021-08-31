本ドキュメントはWindows 2012 R2 バージョンOSとWindows 2008 バージョンOSでのIISの追加とインストールするプロセスについて説明します。
## Windows 2012 R2 バージョン
 1. Windows CVMにログインし、左下の【スタート(Start)】をクリックして、【サーバーマネージャー(Server Manager)】を選択して、サーバー管理画面を開きます。下図に示すように：
![](//mc.qcloudimg.com/static/img/7b433cabe3d7349b5a38b359639e4c7c/image.png)

 2.【役割と機能の追加】を選択し、「役割と機能の追加ウィザード」の「開始する前に」画面で【次へ(N)>】ボタンをクリックします。「インストールの種類」画面で、【役割ベースまたは機能ベースのインストール】を選択して、【次へ(N)>】ボタンをクリックします。　　
![](//mc.qcloudimg.com/static/img/b0f5ffb889f4d23213f0811bd945b170/image.png)
![](//mc.qcloudimg.com/static/img/027fe90a3c882520662783bdcda97b94/image.png)
![](//mc.qcloudimg.com/static/img/919430e0493d9580c33eab871ffee557/image.png)

 3. ウィンドウの左側で「サーバーの役割」タブを選択し、【Web サーバー (IIS)】をチェックして、ポップアップダイアログで【機能の追加】ボタンをクリックして、【次へ(N)>】ボタンをクリックします。
![](//mc.qcloudimg.com/static/img/0d69cbfd04d9a614eeb00559f34bafba/image.png)
![](//mc.qcloudimg.com/static/img/a254c87a59392801a4bf23521c9c1535/image.png)

 4. 「機能」タブで「.Net3.5」をチェックして、【次へ(N)>】ボタンをクリックした後、「Webサーバーの役割(IIS)」タブを選択して、 【次へ(N)>】ボタンをクリックします。
![](//mc.qcloudimg.com/static/img/703cda6d11a5cfc3a26f471f0535dc17/image.png)
![](//mc.qcloudimg.com/static/img/5d84575332b4c9c425bcdf0baa80f7e6/image.png)

 5. 「役割サービス」タブで【CGI】オプションをチェックして、【次へ(N)>】ボタンをクリックします。
![](//mc.qcloudimg.com/static/img/958f0c466a633ea6c58de651a4ad7982/image.png)

 6. インストールを確認し、インストールが完了するまで待ちます。
![](//mc.qcloudimg.com/static/img/045b132f13b06c6e499b85ecb34a3f43/image.png)

 7. インストールが完了したら、CVMのブラウザーで```http://localhost/``` にアクセスして、インストールが成功したかどうかを確認します。 以下の画面が表示されたら、インストールが正常に完了したことを示しています。
![](//mc.qcloudimg.com/static/img/e064cc1f765d68edf3dcfb0051d5dbfa/image.png)

## Windows 2008 バージョン
 1. Windows CVMにログインし、左下にある【スタート(Start)】メニュー中の【管理ツール】中の【サーバーマネージャー】ボタンをクリックして、サーバー管理画面を開きます。
![](//mc.qcloudimg.com/static/img/787983bdedb15a6d496119c953d35e1a/image.png)

 2. 【役割と機能の追加(Add Roles)】をクリックして、サーバーの役割を追加します。「Web Server(IIS)」オプションをチェックして、【次へ(N)>】をクリックします。
![](//mccdn.qcloud.com/img56b1bb12831b3.png)
![](//mccdn.qcloud.com/img56b1bcee2d9e8.png)

 3. 「役割サービス(Role Services」)を選択する時に、「CGI」オプションをチェックします。
![](//mccdn.qcloud.com/img56b1bd1b8f220.png)

 4. 設定が完了したら、【インストール(install)】をクリックして、インストールを続行します。
![](//mccdn.qcloud.com/img56b1bd4f18f1a.png)

 5. ブラウザーを介してWindows CVMのパブリックネットワークIPにアクセスして、IISサービスが正常に実行しているかどうかを確認します。下記のように表示されたら、IISのインストールと設定が成功したことを示しています。
![](//mccdn.qcloud.com/img56b1bd7c5b0be.png)

