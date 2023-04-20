
##  ユースケース
一般的に、Windowsファイルシステム形式はNTFSまたはFAT32であり、Linuxファイルシステムの形式はEXTシリーズです。OSをLinuxからWindowsに再インストールすると、OSタイプが変わりましたが、データディスクは元の形式のままです。再インストールされたシステムはデータディスクのファイルシステムにアクセスできなくなる可能性があります。元のデータを読み取るには、フォーマット変換ソフトウェアが必要になります。

このドキュメントでは、LinuxをWindowsに[再インストール]（https://intl.cloud.tencent.com/document/product/213/4933）した場合、CVMで元のLinuxシステムのデータディスクのデータを読み取る方法について説明します。 


## 前提条件
- Windowsに再インストールされたCVMにDiskInternals Linux Readerソフトウェアがインストールされています。
DiskInternals Linux Reader ソフトウェアのダウンロードリンク：`http://www.diskinternals.com/download/Linux_Reader.exe `
- 再インストール前にLinux CVMにマウントされたデータディスクには、vdb1とvdb2の2つのパーティションがあることが分かっています。下図に示すように、
![](https://main.qcloudimg.com/raw/ef515a31c27e5ea96993af60dfc9ab55.png)

## 操作手順
### データディスクをマウントする

>! データディスクがすでにマウントされている場合は、この手順をスキップできます。
>
1.  [Tencent Cloud CVMコンソール](https://console.cloud.tencent.com/cvm/)にログインします。
2. 左側のナビゲーションバーで**クラウドディスク**を選択して、Cloud Block Storage管理画面に入ります。
3. 下図に示すように、システムが再インストールされたインスタンスを見つけ、右側の** More**>**Mount**をクリックします。
![](https://main.qcloudimg.com/raw/a3100055adb58330591e277c4e7f72eb.png)
4. ポップアップウィンドウで、再インストールされたCVMを選択し、**Submit**をクリックします。

### データディスク情報を確認する 
1. DiskInternals Linux Readerソフトウェアを実行して、新しくマウントされたデータディスク情報を確認できます。下図に示すように、`/root/mnt`と`/root/mnt1`は、再インストール前のLinux CVMデータディスクの2つのパーティションvdb1とvdb2です。
>! 現時点では、Linuxデータディスクは読み取り専用です。このデータディスクをWindowsデータディスクとして読み書きする必要がある場合は、まず必要なファイルをバックアップし、Windows OSがサポートする標準タイプに再フォーマットします。詳細については、[Windowsインスタンス：データディスクの初期化](https://intl.cloud.tencent.com/document/product/213/2158)をご参照ください。
>
![](https://main.qcloudimg.com/raw/490428b0668dcd61c4c60bcb75121462.png)
2. ダブルクリックして `/root/mnt`ディレクトリに入り、コピーするファイルを右クリックし、**Save**を選択してファイルを保存します。下図に示すように、
![](https://main.qcloudimg.com/raw/f36cbf32a7b423b8800e1fda6ba1c038.png)




