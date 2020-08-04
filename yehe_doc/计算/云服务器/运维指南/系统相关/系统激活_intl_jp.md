Tencent Cloud CVMはKMSを利用して、Windowsサーバーのライセンス認証を行います。
> 
> - このドキュメントは、Tencent Cloudが提供するWindows Server パブリックイメージにのみ対応し、カスタムイメージまたは外部ソースからインポートされたイメージには適用されません。
> - Windows Server 2008 と Windows Server 2012 はこの方法によるライセンス付与が必要です。Windows Server 2016 とWindows Server 2019パブリックイメージのデフォルト設定のKMSアドレス（kms.tencentyun.com:1668）は、これ以上変更することなく使用できます。


## アクティベーション前の注意事項
1. 下図に示すように、Windows上のSPP Notification Service はアクティベーション関連サービスの実行に利用されるため、正常に実行していることを保証する必要があります。
![](https://main.qcloudimg.com/raw/f84f7bd86fae0df1c2394cdc554b6a98.png)
2. 一部の最適化ソフトウェアはサービスに関連するアプリケーションの実行権限の変更をブロックする場合があります。例えば、 sppsvc.exe プロセスの実行権限を変更すると、サービスが正常に実行されない可能性があります。
![](https://mc.qcloudimg.com/static/img/685fe41ef992f11ba305dfb570cb916c/21.png)
Windows CVMをアクティブ化する前に、Windowsのサービスおよびその他の重要な機能が正常に実行していることを確認してください。
 
## 自動アクティベーション
Tencent Cloudは、Windowsサーバーのアクティベーション用のスクリプトをカプセル化して、手動アクティベーションの手順を簡素化しました。
1. Windows CVM にログインします。
CVMのブラウザーから `http://mirrors.tencentyun.com/install/windows/activate-win.bat`アドレスにアクセスし、スクリプトをダウンロードします。
3. スクリプトを実行して、自動アクティベーションを完了します。

## 手動アクティベーション

### 注意事項
一部のシステムでは、システムクロックに問題がある場合、手動アクティベーション中にエラーが発生します。この場合、以下の手順に従って、最初にシステムクロックを同期する必要があります。
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
3. コンソールウィンドウで以下のコマンドを順番に実行すると、手動アクティベーションが完了します。
 - Windows Server 2008、Windows Server 2012、Windows Server 2019サーバに対して次のコマンドを順番に実行します。
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```
 - Windows Server 2016サーバで次のコマンドを順番に実行します。
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms1.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```




