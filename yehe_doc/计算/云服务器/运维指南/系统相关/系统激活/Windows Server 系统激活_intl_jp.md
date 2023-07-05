Tencent Cloud CVMはKMSを利用して、Windowsサーバーのライセンス認証を行います。

<dx-alert infotype="notice" title="">

- このドキュメントに記載されているアクティベーション方式は、Tencent Cloudが提供するWindows Serverパブリックイメージのみ対応し、カスタムイメージまたは外部ソースからインポートされたイメージには適用されません。
- Windows Server 2008とWindows Server 2012はこの方法によるライセンス付与が必要です。Windows Server 2016とWindows Server 2019のパブリックイメージのデフォルト設定のKMSアドレス（kms.tencentyun.com:1668）は正しく、これ以上変更することなく使用できます。
  </dx-alert>



## アクティベーション前の注意事項

1. 下図に示すように、**Windows Server 2008**のSPP Notification Serviceはアクティベーション関連サービスの実行に利用されるため、正常に実行していることを保証する必要があります：
   ![](https://qcloudimg.tencent-cloud.cn/raw/40c2d2a0895902917c5ca419e43905fc.png)
2. 一部の最適化ソフトウェアはサービスに関連するアプリケーションの実行権限の変更をブロックする場合があります。例えば、下図に示すように、sppsvc.exeプロセスの実行権限を変更すると、サービスが正常に実行できなくなる場合があります。
   ![](https://qcloudimg.tencent-cloud.cn/raw/b45ca678ce7615c53a053d1d36ef78bc.png)
   Windows CVMをアクティブにする前に、WindowsCVMのサービスおよびその他の重要な機能が正常に実行していることを確認してください。

## 自動アクティベーション

Tencent Cloudは、Windowsサーバーをアクティブ化するためのスクリプトをカプセル化し、手動アクティベーションの手順を簡素化しました。次の手順でスクリプトを使用してアクティベーションを実行してください：

1. Windows CVMにログインします。
2. [スクリプト](https://iso-1251783334.cos.ap-guangzhou.myqcloud.com/scripts/activate-win.bat )をダウンロードして実行すると、自動アクティベーションが完了します。

## 手動アクティベーション

### 注意事項

一部のシステムでは、システムクロックに問題がある場合、手動アクティベーション中にエラーが発生する可能性があります。この場合、最初にシステムクロックを同期してください。クロック同期の操作手順は次のとおりです：
<dx-alert infotype="explain" title="">
Windows CVMのシステムクロックが正常な場合、直接 [アクティベーション手順](#ActivationStep)に進んでください。
</dx-alert>

1. Windows CVMにログインします。
2. OSのインターフェースで、**スタート**>**実行**をクリックし、`cmd.exe`を入力して、コンソールウィンドウを開きます。
3. コンソールウィンドウで以下のコマンドを順番に実行して、システムクロックを同期します。
```
w32tm /config /syncfromflags:manual /manualpeerlist:"ntpupdate.tencentyun.com"
w32tm /resync
```

### アクティベーション手順[](id:ActivationStep)

1. Windows CVMにログインします。
2. OSのインターフェースで、**スタート**>**実行**をクリックし、`cmd.exe`を入力して、コンソールウィンドウを開きます。
3. コンソールウィンドウで以下のコマンドを順番に実行して、手動アクティベーショが完了します。
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```
