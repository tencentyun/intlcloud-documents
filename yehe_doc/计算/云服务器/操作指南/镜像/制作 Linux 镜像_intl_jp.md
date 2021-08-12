## 概要

このドキュメントでは、ローカルLinuxサーバーまたは他のクラウドプラットフォームにデプロイされたLinuxサーバーのシステムディスクイメージを作成する方法について説明します。

## 操作手順

### 準備

システムディスクイメージを作成してエクスポートする前に、次のことをご確認ください。
>? データディスクイメージをエクスポートする場合、この操作をスキップしてください。
>

#### OS パーティションと起動方法の確認
1. 次のコマンドを実行して、OSパーティションがGPTパーティションであるかどうかを確認します。
```
sudo parted -l /dev/sda | grep 'Partition Table'
```
 - 返された結果がmsdosである場合、MBRパーティションを意味し、次の手順に進みます。
 - 返された結果がgptである場合、GPTパーティションを意味します。現在のサービス移行ではGPTパーティションがサポートされていません。この場合、[チケットを提出して](https://console.cloud.tencent.com/workorder/category)問題を報告してください。
2. 次のコマンドを実行して、OSがEFIモードで起動するかどうかを確認します。
```
sudo ls /sys/firmware/efi
```
 - EFIファイルが存在する場合は、現在のOSがEFIモードで起動されることを意味します。この場合、[チケットを提出](https://console.cloud.tencent.com/workorder/category)して問題を報告してください。
 - EFIファイルが存在しない場合は、次の手順に進みます。

#### 重要なシステムファイルの確認
チェックを必要とする重要なシステムファイルには、次のファイルを含みますが、これらに限りません。
>? 関連するリリースバージョンの標準に従って、重要なシステムファイルのパスとアクセス許可が正しく、ファイルが正常に読み書きできることを確認します。
>
 - /etc/grub2.cfg：カーネルパラメーターにはuuidを使用してrootをマウントすることが推奨されています。他の方法（root=/dev/sdaなど）では、システムの起動エラーを引き起こす可能性があります。
 - /etc/fstab：他のハードディスクをマウントしないでください。移行後にディスクがないため、システムが起動しない可能性があります。
 - /etc/shadow：アクセス権は正常で、読み取りと書き込みが可能です。

#### ソフトウエアのアンインストール
競合を引き起こす可能性のあるドライバーとソフトウェア（VMware tools、Xen tools、Virtualbox GuestAdditions、および基盤となるドライバを搭載する一部のソフトウェアを含む）をアンインストールします。

#### virtioドライバーの確認
操作の詳細については、ドキュメント[LinuxでのVirtioドライバーの確認](https://intl.cloud.tencent.com/document/product/213/9929)をご参照ください。

#### 安cloud-initのインストール
インストールの詳細については、ドキュメント[Linux OSにcloud-initのインストール](https://intl.cloud.tencent.com/document/product/213/12587)をご参照ください。

#### その他のハードウェア構成の確認
クラウド移行後、ハードウェアの変更は次のものが含まれていますが、これらに限られない場合があります。
 - グラフィックカードはCirrus VGAに変更されます。
 - ディスクはVirtio Diskに変更されます。デバイス名はvda、vdbです。
 - ENIはVirtio Nicに変更されます。デフォルトではeth0のみが提供されます。

### パーティションとサイズの確認
次のコマンドを実行して、現在のOSのパーティション形式を確認し、コピーするパーティションとサイズを判断します。
```
mount
```
次のような結果が返されます。
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
結果によると、ルートパーティションは `/dev/sda1`にあります。`/boot` 、 `/home` には独立したパーティションがなく、sda1にはブートパーティションが含まれるが、mbrが欠けているので、sda全体をコピーするだけで済みます。
>! エクスポートされたイメージには、少なくともルートパーティションとmbrが含まれている必要があります。エクスポートされたイメージにmbrが欠けている場合、OSを起動できません。
> 現在のOSでは、`/boot`と`/home`が独立したパーティションである場合、エクスポートされたイメージにはこれら2つの独立したパーティションが含まれている必要があります。
> 

### イメージのエクスポート
必要に応じてイメージのエクスポート方法を選択してください。


<dx-tabs>
<span id="Useplatform"></span>
::: プラットフォームツールを使用してイメージをエクスポートする
VMWare vCenter ConvertまたはCitrix XenConvertなどの仮想化プラトフォームのイメージエクスポートツールを利用します。詳細について、対象プラットフォームのエクスポートツールのドキュメントをご参照ください。
<dx-alert infotype="explain">
 現在、Tencent Cloudサービス移行でサポートされているイメージ形式には、qcow2、vhd、raw、vmdkがあります。
</dx-alert>
:::
<span id="ExportImageForUsingCommand"></span>
:::コマンドを使用してイメージをエクスポートする
<dx-alert infotype="notice">
コマンドを使用して手動でイメージをエクスポートすると、（I/Oがビジーなときに、ファイルシステムのメタデータが破損する可能性があります）、リスクが高くなります。イメージをエクスポートした後は、[イメージをチェック](#CheckMirror)して完全性を確保することをお勧めします。
</dx-alert>

イメージをエクスポートするには、[qemu-imgコマンドを使用](#qemuimg)または[ddコマンドを使用](#dd)のいずれかの方法を選択します。
- **`qemu-img` コマンドを使用する**<span id="qemuimg"></span>
 1. 次のコマンドを実行して、必要なパッケージをインストールします。このドキュメントではDebianを例にします。パッケージはリリースバージョンによって異なる可能性がありますので、実際の状況に合わせて調整してください。例えば、CentOSではパッケージ名は `qemu-img`です。
```
apt-get install qemu-utils
```
 2. 次のコマンドを実行して、 `/dev/sda`ディスク全体を `/mnt/sdb/test.qcow2`にエクスポートします。
```
sudo qemu-img convert -f raw -O qcow2 /dev/sda /mnt/sdb/test.qcow2
```
ここで、`/mnt/sdb`はマウントされた新しいディスクまたは他のネットワークストレージです。
他の形式に変換する必要がある場合は、`-O`のパラメータ値を変更してください。変更可能なパラメータ値は次の通りです。
<span id="-OParameterValue"></span>
<table>
	<tr><th>パラメータ値</th><th>意味</th></tr>
	<tr><td>qcow2</td><td>qcow2形式</td></tr>
	<tr><td>vpc</td><td>vhd形式</td></tr>
	<tr><td>vmdk</td><td>vmdk形式</td></tr>
	<tr><td>raw</td><td>形式なし</td></tr>
</table>
- **`dd` コマンドを使用する**<span id="dd"></span>
例えば、次のコマンドを実行して、raw形式のイメージをエクスポートします。
```
sudo dd if=/dev/sda of=/mnt/sdb/test.imag bs=1K count=$count
```
ここで、`count` パラメータはコピーするパーティションの数であり、 `fdisk` コマンドを使用してその値を調べることができます。すべてのパーティションをコピーする必要がある場合、`count` パラメータを無視してもかまいません。　
例えば、次のコマンドを実行して、  `/dev/sda` のパーティション数を確認します。
```
fdisk -lu /dev/sda
```
以下のような結果が返されます：
```
Disk /dev/sda: 1495.0 GB, 1494996746240 bytes
255 heads, 63 sectors/track, 181756 cylinders, total 2919915520 sectors
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
`fdisk` コマンドから返された結果によると、sda1の終了位置は41945087 \*512バイトであり、`count`は20481Mに設定してください。
<dx-alert infotype="explain">
 `dd`コマンドでエクスポートされたイメージはraw形式であり、[qcow2、vhdまたはその他のイメージ形式に変換する](#ImageFormatConversion)ことをお勧めします。
</dx-alert>
:::
</dx-tabs>

<span id="ImageFormatConversion"></span>
### イメージ形式の変換
>? 現在、Tencent Cloudのサービス移行はqcow2、vpc、vmdk、rawのイメージ形式がサポートされます。転送と移行の時間を短縮するために、圧縮したイメージ形式のご利用をお勧めします。
> 
 `qemu-img`コマンドを使用してイメージ形式を変換します。
例えば、次のコマンドを実行して、raw形式のイメージをqcow2形式に変換します。
```
sudo qemu-img convert -f raw -O qcow2 test.img test.qcow2
```
- `-f`は移行元のイメージファイル形式です。
- `-O` は移行先のイメージファイル形式であり、サポートされている形式は[-Oのパラメータ値](#-OParameterValue)をご参照ください。

<span id="CheckMirror"></span>
### イメージの確認
>? サーバーがシャットダウンされていない時にイメージの作成を行い、またはその他の理由で作成したイメージファイルシステムにエラーが発生する場合がありますので、イメージ作成後にエラーの有無を確認することをお勧めします。
>
イメージの形式が現在のプラットフォームでサポートしている形式と一致している場合、イメージを直接開いてファイルシステムを直接確認できます。例えば、Windowsプラットフォームではvhd形式のイメージを直接追加でき、Linuxプラットフォームではqemu-nbdを利用してqcow2形式のイメージを開くことができ、Xenプラットフォームではvhdファイルを直接利用できます。このドキュメントでは、Linuxプラットフォームを例にして次の確認手順を実行します。
1. 次のコマンドを順番に実行して、nbdモジュールがすでに存在しているかどうかを確認します。
```
modprobe nbd
```
```
lsmod | grep nbd
```
次のような結果が返される場合は、nbdモジュールはすでに存在していることを意味します。返り値がNULLの場合は、カーネルコンパイルオプション `CONFIG_BLK_DEV_NBD`がオンになっているかどうかを確認してください。オンになっていない場合は、システムを交換するか、コンパイルオプション `CONFIG_BLK_DEV_NBD`をオンにしてカーネルを再コンパイルする必要があります。
![](https://main.qcloudimg.com/raw/190bd78d60c7340fb95210f60e126105.png)
2.次のコマンドを順に実行して、イメージを確認します。
```
qemu-nbd -c /dev/nbd0 xxxx.qcow2
```
```
mount /dev/nbd0p1 /mnt
```
`qemu-nbd` コマンドを実行すると、`/dev/nbd0`は `xxx.qcow2`の内容をマッピングします。 `/dev/nbd0p1`は仮想ディスクの最初のパーティションを表します。nbd0p1が存在しないか、マウントに失敗した場合は、イメージエラーの可能性が高くなります。
また、イメージをアップロードする前に、CVMを起動してイメージファイルを使用できるかどうかをテストすることもできます。


