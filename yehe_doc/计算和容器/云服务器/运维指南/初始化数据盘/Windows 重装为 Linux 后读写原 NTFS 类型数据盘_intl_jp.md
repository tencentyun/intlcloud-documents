## ユースケース

Windowsのファイルシステムは通常、NTFSまたは FAT32 形式を使用し、Linuxのファイルシステムは通常、EXTシリーズの形式を使用します。Cloud Virtual MachineのOSをWindowsからLinuxに再インストールした場合、OSのタイプは変更されましたが、CVM中のデータディスクが元のシステムで使用されている形式のままです。そのため、システムを再インストールした後、CVMがデータディスクファイルシステムにアクセスできない場合があります。このドキュメントはシステムを再インストールした後、Linux CVM上の元のWindowsシステムでデータディスクデータを読み取る方法について説明します。

## 操作手順

### LinuxサーバーでNTFS関連ソフトウェアをインストールする

1. 再インストールされた Linux CVMにログインします。
2. 以下のコマンドを実行して、ntfsprogsソフトウェアをインストールし、Linux CVMが NTFS ファイルシステムにアクセスできるようにします。
<dx-alert infotype="explain" title="">
このドキュメントはCentOSシステムを例として説明します。Linuxシステムのインストールコマンドは異なっています。対応するインストールコマンドを使用してインストールしてください。
</dx-alert>
```shellsession
yum install  -y ntfsprogs
```


###  Windows CVMのデータディスクをLinux CVMにマウントする



>?
>- Windows CVMのデータディスクがLinux CVMにマウントされた場合、この操作をスキップできます。
>- 再インストールされたLinux CVMに新しいデータディスクをマウントするには、[Cloud Block Storageを初期化](https://intl.cloud.tencent.com/document/product/362/31597)する必要があります。


1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. 左側のナビゲーションバーで、 **[Cloud Block Storage](https://console.cloud.tencent.com/cvm/cbs)** をクリックして、CBS管理画面に入ります。
3. マウントしたいWindowsデータディスクを選択し、**その他** > **マウント**をクリックします。以下の通りです。
![](https://qcloudimg.tencent-cloud.cn/raw/6acf53df9c1df0518502402d8bcadb6b.png)
4. 表示された「インスタンスへのマウント」ウィンドウで、マウントしたいLinux CVMを選択し、**OK**をクリックします。
5. WindowsデータディスクをマウントしたLinux CVMにログインします。
6. 以下のコマンドを実行して、Windows CVMからマウントされたデータディスクを確認します。
```shellsession
parted -l
```
次のような情報が返されます：
```shellsession
Model: Virtio Block Device (virtblk)
Disk /dev/vdb: 53.7GB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags: 
Number  Start   End     Size    File system  Name                          Flags
 1      17.4kB  134MB   134MB                Microsoft reserved partition  msftres
 2      135MB   53.7GB  53.6GB  ntfs         Basic data partition
```
7. 以下のコマンドを実行して、データディスクをマウントします。
```shellsession
mount -t ntfs-3g データディスクのパス マウントポイント
```
例えば、パスが `/dev/vdb2` のデータディスクを `/mnt` にマウントする場合、以下のコマンドを実行してください：
```shellsession
mount -t ntfs-3g /dev/vdb2 /mnt
```
現時点ではファイルシステムが識別できるため、 マウントされたデータディスクはLinuxシステムに直接読み書きできます。




