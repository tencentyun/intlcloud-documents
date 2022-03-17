## ユースケース

Windowsのファイルシステムは通常NTFSまたは FAT32 形式を使用し、Linuxのファイルシステムは通常EXTシリーズの形式を使用します。Cloud Virtual MachineのOSをWindowsからLinuxに再インストールした場合、OSのタイプは変更されましたが、CVM中のデータディスクが元のシステムで使用されている形式のままです。そのため、システムを再インストールした後、CVMがデータディスクファイルシステムにアクセスできない場合があります。このドキュメントはシステムを再インストールした後、Linux CVM上の元のWindowsシステムでデータディスクデータを読み取る方法について説明します。

## 操作手順

### NTFSをサポートするようにLinuxシステムを設定する 

1. 再インストールされた Linux CVMにログインします。
2. 以下のコマンドを実行して、ntfsprogsソフトウェアをインストールし、Linux CVMが NTFS ファイルシステムにアクセスできるようにします。
>このドキュメントは CentOS システムを例として説明します。Linuxシステムのインストールコマンドの種類は異なります、対応するインストールコマンドを使用してインストールしてください。
>
```
yum install ntfsprogs
```


###  Windows CVMのデータディスクをLinux CVMにマウントする

>  Windows CVMのデータディスクがLinux CVMにマウントされた場合、この操作をスキップできます。
>
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. 左側のナビゲーションバーで、【[Cloud Block Storage](https://console.cloud.tencent.com/cvm/cbs)】をクリックして、CBS管理画面に入ります。
3. マウントするWindows データディスクを選択し、【もっと見る】>【マウント】をクリックします。
4. 表示された「インスタンスへのマウント」ウィンドウで、マウントしたい Linux CVMを選択し、【OK】をクリックします。
5. WindowsデータディスクをマウントしたLinux CVMにログインします。
6. 以下のコマンドを実行して、Windows CVMからマウントされたデータディスクを確認します。
```
parted -l
```
次のような情報が返されます：
```
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
```
mount -t ntfs-3g データディスクのパス マウントポイント
```
例えば、パスが `/dev/vdb1` のデータディスクを `/mnt` にマウントする場合、以下のコマンドを実行してください：
```
mount -t ntfs-3g /dev/vdb1 /mnt
```
現時点ではファイルシステムが識別できるため、 マウントされたデータディスクはLinuxシステムに直接読み書きできます。

