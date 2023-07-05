## ユースケース
CVMでのソフトウェアインストールの効率を向上させ、ソフトウェアのダウンロードとインストールのコストを削減するために、Tencent Cloudはzypper ダウンロードソースを提供します。openSUSE OSと一部 SLES CVMのユーザーはzypperを利用してソフトウェアをインストールできます。本ドキュメントは openSUSE OS を例に、zypper を利用して迅速なソフトウェアをインストールする方法を説明します。

## 操作手順
### ソフトウェアソースの確認

1. root アカウントを利用して、openSUSE OSのCVM にログインします。
2. `zypper service-list` または `zypper sl` コマンドを実行して、ソフトウェアソースの一覧を表示します。
例えば、 `zypper sl` コマンドを実行して、以下のような情報が返されます：
![](https://main.qcloudimg.com/raw/ee336605784eca333f10777ccb7cf5ed.png)
 - ソフトウェアソースに利用可能なソースが追加された場合、 [ソフトウェアパッケージをインストール](#SearchPackage)してください。
 - ソフトウェアソースに利用可能なソースが追加されていない場合、 [ソフトウェアソースを追加](#AddSoftwareSource)してください。

<spam id="AddSoftwareSource"></span>
### ソフトウェアソースの追加

`zypper service-add` または `zypper sa` コマンドを実行して、手動でソフトウェアソースを追加します。
例えば、`zypper sa` コマンドを実行して、例は以下の通り：
```
zypper sa -t YaST http://mirrors.cloud.tencent.com/opensuse opensuse
zypper sa -t YaST http://mirrors.cloud.tencent.com/opensuse/update update
```

<span id="SearchPackage"></span>
### ソフトウェアパッケージのインストール

1. `zypper search` または `zypper se` コマンドを実行して、ソフトウェアパッケージを検索します。
例、ソフトウェアパッケージ「Nginx 」を検索する場合、実行するコマンドは以下の通り：
```
zypper se nginx
```
以下のような結果が返されます：
![](https://main.qcloudimg.com/raw/292106a01b048171007247cb9cdf00c0.png)
2. 検索されたソフトウェアパッケージの名に従って、`zypper install` または `zypper in` コマンドを実行して、ソフトウェアをインストールします。
> 複数のソフトウェアをインストールする必要がある場合、ソフトウェアパッケージ名をスペースで区切ってください。
> ソフトウェアをインストールする時に、依存パッケージが必要な場合、自動でダウンロードしてインストールし、手動で依存パッケージをインストールする必要がありません。
> 
例えば、Nginxをインストールするには、実行するコマンドは以下の通り：
```
zypper install nginx
```
例えば：PHP と PHP-FPM等のソフトウェアをインストールすると、実行するコマンドは以下の通り：
```
zypper install MySQL-server-community php5-mysql php5 php5-fpm
```


### インストールされたソフトウェア情報の確認

1. ソフトウェアインストールが完了した後、以下のコマンドを実行して、ソフトウェアパッケージのインストールディレクトリの詳細を確認します。
```
rpm -ql
```
例えば、ソフトウェアパッケージ「Nginx」のインストールディレクトリの詳細を確認するには、実行するコマンドは以下の通り：
```
rpm -ql nginx
```
以下のような情報が返されます：
![](https://main.qcloudimg.com/raw/b4ad19a8735041bf78942f5ea351dc2e.png)
2. 以下のコマンドを実行して、ソフトウェアパッケージのバージョン情報を確認します。
```
rpm -q
```
例えば、ソフトウェアパッケージ「Nginx」のバージョン情報を確認するには、実行するコマンドは以下の通り：
```
rpm -q nginx
```
以下のような情報が返されます：
![](https://main.qcloudimg.com/raw/9950192d2cf51c7ab30c2109b3e52d14.png)
