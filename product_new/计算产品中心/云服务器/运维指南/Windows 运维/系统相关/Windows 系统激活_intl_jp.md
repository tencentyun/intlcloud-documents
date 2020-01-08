Tencent Cloud CVMはKMSを利用して、Windowsサーバーのライセンス認証を行います。
> 
> - このドキュメントはTencent Cloudが提供するWindows Server パブリックイメージのみを対応し、カスタマイズイメージまたは外部インポートイメージは本文のアクティベーション方式を利用できません。
> - Windows Server 2008 と Windows Server 2012 はこの方式のライセンス認証が必要です。Windows Server 2016 パブリックイメージのデフォルトKMSアドレス設定（kms.tencentyun.com:1668）が正しいので、修正する必要がありません。


## アクティベーション前の注意事項
1. WindowsのPP Notification Service はアクティベーション関連サービスの実行に利用されるため、正常に実行していることを保証する必要があります。下図に示すように：
2. 一部の最適化ソフトウェアはサービスに関連するアプリケーションの実行権限の変更をブロックする場合があります。例えば、 sppsvc.exe プロセスの実行権限を変更すると、サービスの実行が異常になる可能性があります。
Windows CVM のアクティベーションを試みる前に、このサービス及びその他の基本機能がWindowsで正常に実行していることを確認してください。

## 自動アクティベーション
Tencent Cloudは、Windowsサーバーのアクティベーション用のスクリプトをカプセル化して、手動アクティベーションの手順を簡素化しました。
1. Windows CVM にログインします。
2. ブラウザで`http://mirrors.tencentyun.com/install/windows/activate-win.bat`にアクセスして、スクリプトをダウンロードします。
3. スクリプトを実行して、自動アクティベーションを完了します。

## 手動アクティベーション

### 注意事項
一部のシステムでは、システムクロックに問題がある場合、手動アクティベーションの時にエラーが発生します。この場合、最初にシステムクロックを同期する必要があります。クロック同期の操作手順は以下の通り：
> Windows CVM のシステムクロックが正常な場合、直接 [アクティベーション手順](#ActivationStep)に進んでください。
>
1. Windows CVM にログインします。
2. OSのインターフェースで、【スタート】>【実行】をクリックし、`cmd.exe`を入力して、コンソールウィンドウを開きます。
3. コンソールウィンドウで以下のコマンドを順番に実行して、システムクロックを同期します。
```
w32tm /config /syncfromflags:manual /manualpeerlist:"ntpupdate.tencentyun.com"
w32tm /resync
```

<span id="ActivationStep"></span>
### アクティベーション手順

1. Windows CVM にログインします。
2. OSのインターフェースで、【スタート】>【実行】をクリックし、`cmd.exe`を入力して、コンソールウィンドウを開きます。
3. コンソールウィンドウで以下のコマンドを順番に実行して、手動アクティベーションを完了します。
 - Windows Server 2008とWindows Server 2012サーバが順番に実行するコマンドは以下の通り：
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```
 - Windows Server 2016サーバが順番に実行するコマンドは以下の通り：
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms1.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```




