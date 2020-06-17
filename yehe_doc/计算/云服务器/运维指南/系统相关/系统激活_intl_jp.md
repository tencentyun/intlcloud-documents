Tencent CVMはKMSを利用して、Windowsサーバーにライセンスを付与します。
> 
> - このドキュメントはTencent Cloudが提供するWindows Server パブリックイメージのみを対応し、カスタムイメージまたは外部ソースからインポートされたイメージは本文のアクティベーション方式を利用できません。
> - Windows Server 2008 と Windows Server 2012 はこの方法によるライセンス付与が必要です。Windows Server 2016 と Windows Server 2019 パブリックイメージで構成されているデフォルトのKMSアドレス（kms.tencentyun.com:1668）は正しいですので、変更する必要がありません。


## アクティベーション前の注意事項
1. WindowsのSPP通知サービスはアクティベーション関連のサービスを実行するために使用されます。下図に示すように、その正常に実行していることを保証する必要があります。
![](https://main.qcloudimg.com/raw/f84f7bd86fae0df1c2394cdc554b6a98.png)
2. 一部の最適化ソフトウェアは、サービスに関連するアプリケーションの実行権限の変更をブロックする場合があります。例えば、sppsvc.exeプロセスの実行権限が変更されると、サービスが正常に実行できなくなる可能性があります。
![](https://main.qcloudimg.com/raw/c1ad23337b0f1b6e186d0c6e50c9e1b5.png)
Windows CVMをアクティブ化する前に、このサービスおよびその他の基本機能がWindowsで正常に実行していることを確認してください。

## 自動アクティベーション
Tencent Cloudは、Windowsサーバーのアクティベーション用のスクリプトをカプセル化して、手動アクティベーションの手順を簡素化しました。
1. Windows CVM にログインします。
2. ブラウザで`http://mirrors.tencentyun.com/install/windows/activate-win.bat`にアクセスして、スクリプトをダウンロードします。
3. スクリプトを実行して、自動アクティベーションを完了します。

## 手動アクティベーション

### 注意事項
一部のシステムでは、システムクロックに問題がある場合、手動でアクティベーションする時にエラーが発生する可能性があります。この場合、最初にシステムクロックを同期する必要があります。クロック同期の操作手順は次のとおりです。
> Windows CVM のシステムクロックが正常な場合、直接 [アクティベーション手順](#ActivationStep)に進んでください。
>
1. Windows CVM にログインします。
2. OSのインターフェースで、【スタート】>【実行】をクリックし、`cmd.exe`を入力して、コンソールウィンドウを開きます。
3. コンソールウィンドウで以下のコマンドを順に実行して、システムクロックを同期します。
```
w32tm /config /syncfromflags:manual /manualpeerlist:"ntpupdate.tencentyun.com"
w32tm /resync
```

<span id="ActivationStep"></span>
### アクティベーション手順

1. Windows CVM にログインします。
2. OSのインターフェースで、【スタート】>【実行】をクリックし、`cmd.exe`を入力して、コンソールウィンドウを開きます。
3. コンソールウィンドウで以下のコマンドを順に実行して、手動アクティベーションプロセスは完了です。
 - Windows Server 2008とWindows Server 2012サーバは順に以下のコマンドを実行してください。
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```
 - Windows Server 2016サーバは順に以下のコマンドを実行してください。
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms1.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```




