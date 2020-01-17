
##   操作シナリオ  
このドキュメントでは、Linux [リインストール](https://intl.cloud.tencent.com/document/product/213/4933)してWindowsになった後、CVMで元のLinuxシステムのデータディスクデータを読み取る方法について説明します。 
一般的に、WindowsファイルシステムフォーマットはNTFSまたはFAT32であり、Linuxファイルシステムフォーマットは通常EXTシリーズです。 OSをLinuxからWindowsにリインストールすると、OSのタイプが変更され、データディスクは元のフォーマットのままであり、リインストールされたシステムがデータディスクにアクセスできなくなる可能性があります。 元のデータを読み取るには、フォーマット変換ソフトウェアが必要になります。

## 前提条件
- リインストールされたWindowsのCVMでDiskInternals Linux Readerソフトウェアをインストールしました。
DiskInternals Linux Reader ソフトウェアの入手方法：`http://www.diskinternals.com/download/Linux_Reader.exe `
- リインストール前にLinux CVMにマウントされたデータディスクには、vdb1とvdb2の2つのパーティションがあることが分かっています。下図に示すように：
![](https://main.qcloudimg.com/raw/ef515a31c27e5ea96993af60dfc9ab55.png)

## 操作手順
### データディスクをマウントする

> データディスクが既にマウントされている場合は、この手順をスキップできます。
>
1.  [Tencent Cloud CVMコンソール](https://console.cloud.tencent.com/cvm/)にログインします。
2. 左側ナビゲーションバーで【Cloud Block Storage】を選択して、Cloud Block Storage管理画面に入ります。
3. リインストールされたシステムのインスタンス行を選択し、右側の【詳細】>【マウント】をクリックします。下図に示すように：
![](https://main.qcloudimg.com/raw/810d9328e0b8d91ed5912b4f7183edd4.png)
4. ポップアップウィンドウで、リインストールされたCVMを選択し、【OK】をクリックします。

### データディスク情報を確認する 
1. DiskInternals Linux Readerソフトウェアを実行して、マウントしたデータディスク情報を確認できます。 `/ root / mnt`と` / root / mnt1`は、リインストール前のLinux CVMデータディスクの2つのパーティションvdb1とvdb2です。下図に示すように：
> この時、Linuxデータディスクは読取専用になってます。このデータディスクをWindowsデータディスクとして読み書きする必要がある場合は、まず必要なファイルをバックアップし、Windows OSがサポートする標準規格に再フォーマットします。詳細については、[Windowsインスタンス：データディスクの初期化](https://intl.cloud.tencent.com/document/product/213/2158)を参照してください。。
>
![](https://main.qcloudimg.com/raw/490428b0668dcd61c4c60bcb75121462.png)
2. ダブルクリックして `/ root / mnt`ディレクトリに入り、コピーしたいファイルを右クリックして、【Save】を選択し、ファイルを保存します。下図に示すように：
![](https://main.qcloudimg.com/raw/a7caf7bcfcd33162bff11c121a64a7f5.png)




