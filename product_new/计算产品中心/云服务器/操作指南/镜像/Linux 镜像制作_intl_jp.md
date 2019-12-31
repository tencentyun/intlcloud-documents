## 操作シナリオ

本ドキュメントは Linux イメージを作成する方法を説明します。

## 操作手順

### 準備作業

システムディスクイメージのエクスポートを作成する時に、下記の確認作業を行う必要があります：
> データディスクイメージをエクスポートする場合は、本操作をスキップしてください。
>

####  OS パーティションと起動方式を確認する
1. 下記のコマンドを実行して、 OS パーティションは GPT パーティションであるかを確認します。
```
sudo parted -l /dev/sda | grep 'Partition Table'
```
 - 戻り値が msdos の場合は、 MBR パーティションであることを示します。次のステップを実行してください。
 - 戻り値が gpt の場合は、 GPT  パーティションであることを示します。現在のサービスマイグレーションは GPT パーティションをサポートしないため、[作業依頼書をサブミット](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1) してフィードバックしてください。
2. 下記のコマンドを実行して、 OS は EFI 方式によって起動するかどうかを確認します。
```
sudo ls /sys/firmware/efi
```
 - ファイルが存在する場合は、OS が EFI 方式によって起動することを示します。[作業依頼書をサブミット](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1)してフィードバックしてください。
 - ファイルが存在しない場合は、次のステップを実行してください。

#### システムキーファイルを確認する
確認必要なシステムキーファイルは下記のファイルを含みますが、これに限られません。
> 関連するリリースバージョンの基準を遵守してください、システムキーファイルの位置と権限が正確であることを確保して、正常に読み書きを行います。
>
 - /etc/grub/grub.cfg： kernel パラメータで uuid を利用してroot にマウントすることを推薦します。その他の方式（例えば、root=/dev/sda）はシイステムを起動できないことを引き起こす可能性があります。
 - /etc/fstab：その他のディスクをマウントしないでください。マイグレーションされた後ディスク損失によってシイステムの起動に失敗する場合があります。
 - /etc/shadow：権限正常のため、読み書きが可能です。

#### ソフトウェアをアンマウントする
アンマウントによってコンフリクトを引き起こす可能性があるドライバーとソフトウェア（ VMware tools，Xen tools，Virtualbox GuestAdditions を含み、また基本ドライバーを付属するソフトウェア）。

####  virtio ドライバーを確認する
操作の詳細情報は [Linux システムのVirtio ドライバーの確認](https://intl.cloud.tencent.com/document/product/213/9929)をご参照ください。

####  cloud-initをインストールする
インストール詳細情報は  [Linux システムの cloud-initのインストール](https://intl.cloud.tencent.com/document/product/213/12587)をご参照ください。

#### その他のハードウェア関連の設定を確認する
クラウドにロックインした後、ハードウェアの変化は下記を含むが、それに限らません：
 - グラフィックスカードは Cirrus VGAに変更されました。
 - ディスクは Virtio Disk に変更され、デバイス名称は vda、vdb に変更されました。
 - ENIは Virtio Nic に変更されました、デフォルトは eth0 だけ提供します。

### パーティションと容量サイズを検索する
下記のコマンドを実行し、現在OSのパーティション形式を確認して、コピーする必要なパーティション及び容量サイズを判断します。
```
mount
```
下記の戻り値を事例として：
```
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
sys on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)
dev on /dev type devtmpfs (rw,nosuid,relatime,size=4080220k,nr_inodes=1020055,mode=755)
run on /run type tmpfs (rw,nosuid,nodev,relatime,mode=755)
/dev/sda1 on / type ext4 (rw,relatime,data=ordered)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,mode=755)
cgroup on /sys/fs/cgroup/unified type cgroup2 (rw,nosuid,nodev,noexec,relatime,nsdelegate)
cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,nodev,noexec,relatime,xattr,name=systemd)
pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)
cgroup on /sys/fs/cgroup/cpu,cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,cpu,cpuacct)
cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,nodev,noexec,relatime,cpuset)
cgroup on /sys/fs/cgroup/rdma type cgroup (rw,nosuid,nodev,noexec,relatime,rdma)
cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,blkio)
cgroup on /sys/fs/cgroup/hugetlb type cgroup (rw,nosuid,nodev,noexec,relatime,hugetlb)
cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,memory)
cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,devices)
cgroup on /sys/fs/cgroup/pids type cgroup (rw,nosuid,nodev,noexec,relatime,pids)
cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,freezer)
cgroup on /sys/fs/cgroup/net_cls,net_prio type cgroup (rw,nosuid,nodev,noexec,relatime,net_cls,net_prio)
cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,perf_event)
systemd-1 on /home/libin/work_doc type autofs (rw,relatime,fd=33,pgrp=1,timeout=0,minproto=5,maxproto=5,direct,pipe_ino=12692)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=39,pgrp=1,timeout=0,minproto=5,maxproto=5,direct,pipe_ino=12709)
debugfs on /sys/kernel/debug type debugfs (rw,relatime)
mqueue on /dev/mqueue type mqueue (rw,relatime)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,pagesize=2M)
tmpfs on /tmp type tmpfs (rw,nosuid,nodev)
configfs on /sys/kernel/config type configfs (rw,relatime)
tmpfs on /run/user/1000 type tmpfs (rw,nosuid,nodev,relatime,size=817176k,mode=700,uid=1000,gid=100)
gvfsd-fuse on /run/user/1000/gvfs type fuse.gvfsd-fuse (rw,nosuid,nodev,relatime,user_id=1000,group_id=100)
```
従って、ルートパーティションが`/dev/sda1` にあり、`/boot` と `/home` が独立したパーティションがなく，sda1 が boot パーティションを含み、 mbrがないことにより、sda全体をコピーすれば良いです。
> エクスポートしたイメージには、少なくてもルートパーティション及び mbrが含まれている必要があります。エクスポートしたイメージに対して mbr がないと、起動することはできません。
> 現在のOSの中、`/boot`と`/home`は独立したパーティションである場合、エクスポートしたイメージはこの二つの独立したパーティションを含む必要があります。
> 

### イメージをエクスポートする
実際の要件に応じて、異なる方式を選択してイメージをエクスポートします。
- [ツールを利用してエクスポートする](#Useplatform)
- [コマンドを利用してイメージをエクスポートする](#ExportImageForUsingCommand)

<span id="Useplatform"></span>
#### プラットフォームツールを利用してイメージをエクスポートする
 VMWare vCenter Convert またはCitrix XenConvert などの仮想化プラットフォームのイメージエクスポートツールを利用します。詳細情報は各プラットフォームのエクスポートツールのドキュメントをご参照ください。
> 現在Tencent Cloudクラウドサービスのマイグレーションにサポートするイメージ形式は：qcow2、vhd、raw、vmdkです。
>

<span id="ExportImageForUsingCommand"></span>
#### コマンドを利用してイメージをエクスポートする
> コマンドを利用して手動でイメージをエクスポートするのはリスクがより大きいため（ 例えば、IO がビジーの場合、ファイルシステムの metadata が混乱になる可能性があるなど）。イメージをエクスポートした後、[イメージの確認](#CheckMirror)することによって完全で正確であることを推薦します。
>

下記のコマンドを実行してイメージをエクスポートする
- ** `qemu-img` コマンドを利用する**
例えば、下記のコマンドを実行し、`/dev/sda`を`/mnt/sdb/test.qcow2`にエクスポートします。
```
sudo qemu-img convert -f raw -O qcow2 /dev/sda /mnt/sdb/test.qcow2
```
その中、`/mnt/sdb`はマウントされた新しいディスク或いはその他のネットワークストレージです。
ほかの形式に変換する必要がある場合、`-O`のパラメータ値を修正してください。修正できるパラメータ値は下記の通り：
<span id="-OParameterValue"></span>
<table>
	<tr><th>パラメータ値</th><th>意味</th></tr>
	<tr><td>qcow2</td><td>qcow2 形式</td></tr>
	<tr><td>vpc</td><td>vhd 形式</td></tr>
	<tr><td>vmdk</td><td>vmdk 形式</td></tr>
	<tr><td>raw</td><td>形式なし</td></tr>
</table>
- ** `dd` コマンドを利用する**
例えば、下記のコマンドを実行し、 raw 形式のイメージをエクスポートします。
```
sudo dd if=/dev/sda of=/mnt/sdb/test.imag bs=1K count=$count
```
その中、`count` パラメータはコピーに必要なパーティション数量です、 `fdisk` コマンドによってこの数量値を検索できます。デスク全体をコピーする場合、`count`パラメータを無視して良いです。
例えば、下記コマンドを実行し、 `/dev/sda`のパーティションの数量を確認します。
```
fdisk -lu /dev/sda
```
下記のような結果が返されます：
```
Disk /dev/sda: 1495.0 GB、 1494996746240 bytes
255 heads、 63 sectors/track、 181756 cylinders、 total 2919915520 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disk identifier: 0x0008f290

   Device Boot      Start         End      Blocks   Id  System
/dev/sda1   *        2048    41945087    20971520   83  Linux
/dev/sda2        41945088    46123007     2088960   82  Linux swap / Solaris
/dev/sda3        46123008    88066047    20971520   83  Linux
/dev/sda4        88066048  2919910139  1415922046   8e  Linux LVM
```
`fdisk` コマンドの戻り値によってsda1 の終了位置は41945087 \* 512バイトのところにあります、`count`を20481Mに設定されていることがわかります。
>  `dd` コマンドによってエクスポートしたイメージは raw 形式であり、[ qcow2、vhd 或いはその他のイメージ形式に変換すること](#ImageFormatConversion)を推薦します。
>

<span id="ImageFormatConversion"></span>
### イメージ形式を変換する
> 現在Tencent Cloudのサービスマイグレーションはサポートするイメージ形式は：qcow2，vhd，vmdk，raw があります。圧縮のイメージ形式を利用してトランスミッションとマイグレーションの時間を節約するのを推薦します。
> 
 `qemu-img` コマンドを利用してイメージ形式を変換します
例えば、下記のコマンドを実行し、 raw 形式のイメージを qcow2 形式に変換します。
```
sudo qemu-img convert -f raw -O qcow2 test.img test.qcow2
```
- `-f`はソースイメージファイル形式です。
- `-O` はターゲットイメージファイル形式であり、サポートする形式は [`-O`のパラメータ値](#-OParameterValue)をご参照ください。

<span id="CheckMirror"></span>
### イメージを確認する
> クラウドサービスを停止していない時に直接イメージを作成すること或いはその他の原因により、作成したイメージファイルシステムが正しくない可能性がありますので、作成したイメージが正しいかを確認することを推薦します。
>
イメージ形式は現在のプラットフォームがサポートする形式と一致の場合、直接イメージを開いてファイルシステムを確認できます。例えば、Windows プラットフォームは直接 vhd 形式のイメージを添付でき、Linux プラットフォームはqemu-nbd を利用して qcow2 形式のイメージを開くことができ、Xen プラットフォームは直接 vhd ファイルを起動できます。
 Linux プラットフォームを事例として：
```
modprobe nbd
qemu-nbd -c /dev/nbd0 xxxx.qcow2
mount /dev/nbd0p1 /mnt
```
 qcow2 イメージの最初のパーティションをエクスポートする時にファイルシステムが破壊された場合、mount するときにエラーが発生します。
また、イメージをアップロードする前に、先にCVMを起動してイメージファイルを利用できるかをテストします。
