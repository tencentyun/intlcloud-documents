## 概要

Windows Server OSでは、インスタンスのソフトシャットダウンをサポートするように、高性能の電源管理を設定する必要があります。それ以外の場合は、CVMコンソールでのみCVMインスタンスを強制的にシャットダウンできます。このドキュメントでは、Windows Server 2012のOSを例として電源管理の設定方法を説明します。

## 操作説明

電源管理を変更するには、コンピューターを再起動する必要はありません。

## 操作手順

1. [RDPファイルを使用してWindowsインスタンスにログイン（推奨）](https://intl.cloud.tencent.com/document/product/213/5435)します。または実際の操作方法により、[リモートデスクトップ接続を使用してWindowsインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32498)することもできます。
2. IEブラウザを介してTencent Cloudプライベートネットワークにアクセスし、Tencent Cloudの電源変更と設定ツールをダウンロードします。
ダウンロードアドレス：`http://mirrors.tencentyun.com/install/windows/power-set-win.bat`です
たとえば、Tencent Cloudの電源変更と設定ツール（power-set-win.bat）をC:ドライブにダウンロードします。
3. 下図に示すように、管理者コマンドラインツール（CMD）を使用してpower-set-win.batを開きます。
![](https://main.qcloudimg.com/raw/22f81122e1188fc83ed4b1100a7469bc.png)
4. 次のコマンドを実行して、現在の電源管理ポリシーを確認します。
```
powercfg -L
```
次の結果が返されます。
 ![](https://main.qcloudimg.com/raw/54ceb4faddc8745b30556621268ac318.png)

4. OS画面で、 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> >**コントロールパネル** > **システムとセキュリティ** > **電源オプション** をクリックすると、電源オプションウィンドウが表示されます。
5. 下図に示すように、電源オプションウィンドウで**プラン設定の変更**をクリックします。
![](https://main.qcloudimg.com/raw/54183c1f9d914789b986781b8a4da6ec.png)
6. 下図に示すように、表示されている「プラン設定の編集」画面でディスプレーとディスクのスリープ時間を変更します。
 ![](https://main.qcloudimg.com/raw/f0b7f447d90fe50ef829a10dab0029c6.png)

