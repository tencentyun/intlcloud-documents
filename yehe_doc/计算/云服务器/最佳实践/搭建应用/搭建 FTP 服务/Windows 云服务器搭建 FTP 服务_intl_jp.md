## 概要
このドキュメントでは、IISを使用してWindows CVMインスタンスにFTPサイトを構築する方法について説明します。

## ソフトウェアバージョン
このドキュメントでは、構築したFTPサービスのソフトウェアバージョンは次のとおりです。
 - Windows OS、このドキュメントでは Windows Server 2012 を例として説明します。
 - IIS：Web サーバー、このドキュメントでは IIS 8.5 を例として説明します。

## 操作手順
### 手順１：CVMにログインする
[RDP ファイルを使用してWindows インスタンスにログインする（推奨）](https://intl.cloud.tencent.com/document/product/213/5435)。
[リモートデスクトップを使用してWindows インスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32498)。

### 手順2：IIS にFTPサービスをインストールする
1. OSインターフェースで、 <img src="https://main.qcloudimg.com/raw/446c1e8cb7da2ce280d710c6a46b693d.png" style="margin:-3px 0px">をクリックして、サーバーマネージャーを開きます。
2. 「サーバーマネージャー」画面で、次の図に示すように、【役割と​機能の追加】をクリックします。
![](https://main.qcloudimg.com/raw/1d941b3c877a420513e494971a834f37.png)
3.「役割と​機能の追加ウィザード」で、【次へ】をクリックして、「インストールの種類の選択」画面に入ります。
4. 「インストールの種類の選択」画面で、【役割ベースまたは機能ベースのインストール】を選択して、【次へ】をクリックします。
5. 「対象サーバーの選択」画面で、デフォルト設定を保持して、【次へ】をクリックします。次の図に示すように：
![](https://main.qcloudimg.com/raw/41f775ccbcd8e984b72bc096efa668d4.png)
6. 「サーバーの役割の選択」画面で、【Web サーバー(IIS)】をチェックし、ポップアップウィンドウで【機能の追加】をクリックします。次の図に示すように：
![](https://main.qcloudimg.com/raw/f23fe1b8415c0f75c54309b652781aa4.png)
7. 【次へ】を連続して3回押す、「役割サービスの選択」画面に入ります。
8. 「役割サービスの選択」画面で、【FTP サービス】と【FTP拡張】をチェックし、【次へ】をクリックします。次の図に示すように：
![](https://main.qcloudimg.com/raw/1fa84c69d96c16f2ea0f10e51b0607bb.png)
9. 【インストール】をクリックして、 FTP サービスのインストールを開始します。
10. インストールが完了したら、【閉じる】をクリックします。

<span id="user"></span>

### 手順3： FTP ユーザー名とパスワードを作成する

>?以下の手順に従ってFTPユーザー名とパスワードを設定してください。匿名ユーザーとしてFTP サービスにアクセスする必要がある場合は、この手順をスキップできます。
>
1. 「サーバーマネージャー」ウィンドウで、右上隅のナビゲーションバーにある【管理ツール】>【コンピューターの管理】を選択して、コンピューター管理ウィンドウを開きます。
2. 「コンピューターの管理」画面で、【システムツール】>【ローカルユーザーとグループ】>【ユーザー】を選択します。
3. 【ユーザー】画面の右側で、空白スペースを右クリックして、【新しいユーザー】を選択します。次の図に示すように：
![](https://main.qcloudimg.com/raw/60bad9ff725b8fe4386c2eed9c5ff63a.png)
4. 「新しいユーザー」画面で、以下のプロンプトに従ってユーザー名とパスワードを設定し、【作成】をクリックします。次の図に示すように：
![](https://main.qcloudimg.com/raw/1bc9cb2c2000361f6699c155e25d7630.png)
主なパラメータは次の通り：
  - ユーザー名：カスタム。このドキュメントでは、 `ftpuser` を例として説明します。
  - パスワードと確認パスワード：カスタム。パスワードには大文字と小文字、数字を全て含める必要があります。このドキュメントでは、 `tf7295TFY` を例として説明します。
  - 【ユーザは次回ログオン時にパスワードの変更が必要】のチェックを外し、【パスワードを無制限にする】にチェックを入れます。 
    実際のニーズに応じてチェックしてください。このドキュメントでは【パスワードを無制限にする】ことを例として説明します。
5.【閉じる】をクリックし、「新しいユーザー」ウィンドウを閉じた後に、リストに作成された`ftpuser` ユーザーを確認できます。
	
### 手順4：共有フォルダーのアクセス権限を設定する
>? ここでは`C:\test`ファイルを例として、FTPサイトの共有フォルダを設定します。このフォルダには共有する必要のあるファイル`test.txt`が含まれています。この例を参照して、新しいフォルダ`C:\test`とファイル`test.txt`を作成することができます。また実際のニーズに応じて、他のフォルダをFTPサイトの共有フォルダとして設定することもできます。
>
1.  OSインターフェースで、<img src="https://main.qcloudimg.com/raw/863967bab67b6cd83ce5f0924e1b19c8.png" style="margin:-3px 0px"> をクリックして、「PC」を開きます。
2. Cドライブで、 `test` フォルダーを選択して右クリックし、【プロパティ】を選択します。
3. 「test プロパティ」ウィンドウで、【セキュリティ】タグを選択します。
4.  `Everyone` ユーザーを選択し、【編集】をクリックします。次の図に示すように：
「グループまたはユーザー名」に `Everyone`が含まれていない場合は、[Everyone Userの追加](#add) を参考してユーザーを追加してください。
![](https://main.qcloudimg.com/raw/aec3d0557deef26ca3ff8005da86603f.png)
5. <span id="step5"></span>「test の権限」画面で、必要に応じて`Everyone` ユーザーの権限を設定し、【OK】をクリックします。次の図に示すように：
このドキュメントでは、 `Everyone`ユーザーにすべての権限を付与することを例として説明します。 
![](https://main.qcloudimg.com/raw/ccdfda072d8a476a08773b7fcf979ec7.png)
6. 「test プロパティ」ウィンドウで、【OK】をクリックして設定を完了します。


### 手順5： FTPサイトを追加する
1. 「サーバーマネージャー」ウィンドウで、右上隅のナビゲーションバーにある【管理ツール】>【インターネット インフォメーション サービス (IIS) マネージャ】を選択します。
2. 表示される「インターネット インフォメーション サービス (IIS) マネージャ」ウィンドウで、左側ナビゲーションバーのサーバー名を展開し、【ウェブサイト】を右クリックして、【FTP サイトの追加】を選択します。次の図に示すように：
![](https://main.qcloudimg.com/raw/3d2c1a2708939cd5a8d7bf3bdf9aa1ff.png)
3. 「サイト情報」画面で、以下の情報を参考して設定し、【次へ】をクリックします。次の図に示すように：
![](https://main.qcloudimg.com/raw/76761e667657b80bfdd2d2403d64ba3c.png)
    -  **FTP サイト名**： FTP サイト名を記入し、このドキュメントでは `ftp` を例としています。
    - **物理パス**：権限が設定された共有フォルダーのパスを選択し、このドキュメントでは、`C:\test` を例としています。
4. 「バインドと SSL の設定」画面で、以下の情報を参考して設定し、【次へ】をクリックします。次の図に示すように：
![](https://main.qcloudimg.com/raw/355c3de0e19d7e1c161c51156bf0965f.png)  
主な構成パラメータ情報は下記の通り：
     - **バインド**：IP アドレスのデフォルト選択は【すべて未割り当て】で、デフォルトのポート番号は21（FTP のデフォルトのポート番号）であり、カスタムポート番号を設定できます。
     - **SSL**：必要に応じて選択してください、このドキュメントでは【SSL 無し】を例としています。
       -  **SSL  無し**：SSL暗号化は必要ありません。
       - **SSL の許可**：FTPサーバーによるクライアントとの非SSLおよびSSL接続のサポートを許可します。
      -  *SSL が必要**： FTPサーバーとクライアント間の通信にはSSL暗号化が必要です。
   【許可】あるいは【必要】を選択した場合、「SSL証明書」で既存のSSL証明書を選択するか、[サーバー証明書の作成](#ssl) を参考してSSL証明書を作成することもできます。
5. 「認証および承認の情報」画面で、以下の情報を参考して設定し、【次へ】をクリックします。次の図に示すように：
![](https://main.qcloudimg.com/raw/0f3be2c7ba449240cdac3f3c767e668c.png)
 - **認証**：認証方法を選択します。このドキュメントでは、【基本】を例として説明します。
    - **匿名**：匿名またはFTPユーザー名を提供するユーザーがコンテンツにアクセスできるようにします。
	 - **基本**：ユーザーは、コンテンツにアクセスするために有効なユーザー名とパスワードを提供する必要があります。基本モードでは、暗号化されていないパスワードをネットワーク経由で送信するため、クライアントと FTP サーバー間の接続が安全であることが分っている場合（たとえば、Secure Sockets Layer を使用する場合）にのみ、この認証方法を使用します。
 - **認可**：「アクセス許可」ドロップダウンリストから方式を選択して、このドキュメントでは、指定されたユーザー`ftpuser` を例として説明します。
	    - **すべてのユーザー**： 匿名ユーザーまたは識別されたユーザーに関係なく、すべてのユーザーがコンテンツにアクセスできます。
	        - **匿名ユーザー**：匿名ユーザーはコンテンツにアクセスできます。
	        - **指定されたロール或はユーザーグループ**：特定のロール或はユーザーグループのメンバーのみがコンテンツにアクセスできます。このオプションを選択する場合は、ロールまたはユーザーグループを指定する必要があります。
	        - **指定されたユーザー**：指定されたユーザーのみがコンテンツにアクセスできます。このオプションを選択する場合は、ユーザー名を指定する必要があります。
 - **権限**：必要に応じて権限を設定してください。本文では【読み取り】と【書き込み】権限の設定を例として説明します。
    - **読み取り**：許可されたユーザーがディレクトリからコンテンツを読み取ることができます。
    - **書き込み**：許可されたユーザーがディレクトリに書き込むことができます。
7. 【完了】をクリックして、 FTP サイトを作成できます。

### 手順6：セキュリティグループとファイアウォールを設定する
1. FTPサイトの構築が完了したら、FTPアクセスモードに対応して、FTPサイトを追加するときに、ポートをバインドするためのインバウンドルールを許可してください。
 - **アクティブモード**：ポート20と21を開きます。
 - **パッシブモード**：ポート21および 1024 ~ 65535（たとえば、ポート5000~6000）の間のポートを開きます。
対応するインバウンドルールを追加する方法については、[セキュリティグループルールの追加](https://intl.cloud.tencent.com/document/product/213/34272)をご参照ください。
2. （オプション）[Microsoft公式ドキュメント](https://docs.microsoft.com/en-us/previous-versions/orphan-topics/ws.11/hh831655(v=ws.11))を参考して FTP サイトのファイアウォールサポートを設定することにより、 FTP サーバーはファイアウォールからのパッシブ接続を受け入れることができるようにします。

### 手順7：FTP サイトをテストする
 FTP クライアントソフトウェア、ブラウザー或はファイルエクスプローラーなどのツールを利用してFTP サービスをテストできます。本文ではクライアント側のファイルエクスプローラーを例として説明します。
1. 実際の使用状況に応じて、 IE ブラウザを設定してください：
 - FTPサイトファイアウォールが構成されています（アクティブモード）：
  **クライアント**の IEブラウザを開き、【ツール】>【インターネットオプション】>【詳細設定】を選択し、【パッシブFTP(ファイアウォールおよびDSLモデム互換用)を使用する】のチェックを外して、【OK】ボタンをクリックします。
 - FTPサイトファイアウォールが構成されていません（パッシブモード）：
    1.  **FTP サーバー**の IE ブラウザを開き、【ツール】> 【インターネットオプション】>【詳細設定】を選択し、【パッシブFTP(ファイアウォールおよびDSLモデム互換用)を使用する】のチェックを外して、【OK】ボタンをクリックします。
    2.  **クライアント**の IEブラウザを開き、【ツール】>【インターネットオプション】>【詳細設定】を選択し、【パッシブFTP(ファイアウォールおよびDSLモデム互換用)を使用する】のチェックを外して、【OK】ボタンをクリックします。
2. 次の図に示すように、クライアントでWindowsエクスプローラーを開き、アドレスボックスに次のアドレスを入力して、Enterキーを押します。
```
ftp://CVMパブリックIP:21
```
![](https://main.qcloudimg.com/raw/d3d5a93170bb990f47ecd9f24c3e89ab.png)
3. ポップアップされた「ログイン」ウィンドウで、[ FTP ユーザー名とパスワードの作成](#user)で設定されたユーザー名とパスワードを入力します。
このドキュメントで使用されるユーザー名は `ftpuser` で、パスワードは `tf7295TFY`です。
4. ログインが成功したら、ファイルをアップロード及びダウンロードできます。

## 付録
<span id="add"></span>

###  Everyone ユーザーを追加する

1. 「test プロパティ」ウィンドウで、【セキュリティ】タグを選択し、【編集】をクリックします。次の図に示すように：
![](https://main.qcloudimg.com/raw/f3f056e833fc63c97f23eef646ea8a10.png)
2. 「権限テスト」画面で、【追加】をクリックします。
3. 「ユーザーまたはグループの選択」画面で、【詳細設定】をクリックします。
4. 表示される「ユーザーまたはグループの選択」画面で、【今すぐ検索】をクリックします。
5. 検索結果に `Everyone` を選択し、【OK】をクリックします。次の図に示すように：
![](https://main.qcloudimg.com/raw/32a9d44822ed4db0e82167d0cfb94835.png)
6. 「ユーザーまたはグループの選択」画面で、【OK】をクリックしてEveryoneユーザー追加できます。次の図に示すように：
![](https://main.qcloudimg.com/raw/1245acedba4be051cf234423460a4345.png)
[手順5](#step5) に進み 、`Everyone` ユーザーの権限を設定します。

<span id="ssl"></span>

### サーバー証明書の作成

1. 「サーバーマネージャー」ウィンドウで、右上隅のナビゲーションバーにある【管理ツール】>【インターネット インフォメーションサービス(IIS) マネージャ】を選択します。
2. 表示される「インターネット インフォメーションサービス (IIS) マネージャ 」ウィンドウで、左側のナビゲーションバーでサーバーを選択し、右側の画面にある【サーバー証明書】をダブルクリックします。次の図に示すように：
![](https://main.qcloudimg.com/raw/8fc9f67a26475b891f4c50d9c670c08c.png)
3. 画面右側の【自己署名証明書の作成】を選択します。
4. 表示される「自己署名証明書の作成」ウィンドウで、証明書名とストレージタイプを設定します。次の図に示すように：
このドキュメントでは個人用ストレージタイプのSSL証明書の作成を例として説明します。
![](https://main.qcloudimg.com/raw/0db81917b5b1e20af19d4d687d0d7fda.png)
5. 【OK】をクリックして、サーバー証明書を作成します。
