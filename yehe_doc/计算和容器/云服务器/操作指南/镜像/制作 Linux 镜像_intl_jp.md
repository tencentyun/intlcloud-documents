## 概要

このドキュメントでは、ローカルまたはその他のプラットフォームのLinuxサーバーシステムディスクイメージの作成について説明します。

## 操作手順

### 準備作業

システムディスクイメージを作成してエクスポートする前に、以下の操作を行う必要があります​。
>?データディスクイメージをエクスポートする場合は、この手順をスキップしてください。
>

#### OSのパーティションと起動方法の確認
1. 以下のコマンドを実行し、OSパーティションがGPTパーティションであるかどうかを確認します。
```
sudo parted -l /dev/sda | grep 'Partition Table'
```
 - リターン結果がmsdosである場合、MBRパーティションであることを示しているので、次の手順を実行してください。
 - リターン結果がgptである場合、GPTパーティションであることを示します。現在マイグレーションサービスはGPTパーティションをサポートしていないため、[チケットを提出](https://console.intl.cloud.tencent.com/
)してフィードバックしてください。
2. 以下のコマンドを実行し、OSがEFIモードで起動するかどうかを確認します。
```
sudo ls /sys/firmware/efi
```
 - ファイルが存在する場合、現在のOSがEFIモードで起動することを示しているので、[チケットを提出](https://console.intl.cloud.tencent.com/
)してフィードバックしてください。
 - ファイルが存在しない場合、次の手順を実行してください。

#### システムキーファイルの確認
確認が必要なシステムキーファイルには、以下のファイルを含みますがこれらに限定されません。
>? 関連する公開バージョンの基準に従って、システムキーファイルの位置と権限が正しいことを保証すると、正常に読み書きできます。
>
 - /etc/grub2.cfg： kernelパラメータではuuidを使用してrootをマウントすることを推奨します。その他の方式（例えばroot=/dev/sda）では、システムが起動できない可能性があります。
 - /etc/fstab：その他のハードディスクをマウントしないでください。マイグレーション後に、ディスクが存在しないためシステムが起動できない可能性があります。
 - /etc/shadow：権限が正しいため、読み書き可能です。

#### ソフトウエアのアンインストール
競合するドライバーとソフトウェアをアンインストールします（VMwareツール、Xenツール、 Virtualbox GuestAdditionsおよび基盤となるドライバーを備える一部のソフトウェアなど）。

#### virtioドライバーの確認
操作の詳細については、[LinuxでのVirtioドライバーの確認](https://intl.cloud.tencent.com/document/product/213/9929)をご参照ください。

#### cloud-initのインストール
インストールの詳細については、[Linuxでのcloud-initのインストール](https://intl.cloud.tencent.com/document/product/213/12587)をご参照ください。

#### その他のハードウェア構成の確認
クラウドへの移行後のハードウェアの変更には、以下が含まれますが、これらに限定されません。
 - グラフィックカードが Cirrus VGAに変更されました。
 - ディスクがVirtio Diskに変更されました。デバイス名はvda、vdbです。
 - ネットワークカードがVirtio Nicに変更されました。デフォルトではeth0のみ提供します。

### パーティションとサイズの検索
以下のコマンドを実行し、現在のOSのパーティション形式を確認してコピーが必要なパーティションとサイズを判断します。
```
mount
```
以下のリターン結果を例として説明します。
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
ルートパーティションは`/dev/sda1`において、`/boot`と`/home`に独立したパーティションがなく、sda1にはbootパーティションを含み、mbrがないため、sdaをすべてコピーするだけで良いということが分かります。
>! エクスポートしたイメージには少なくともルートパーティションとmbrを含む必要があります。エクスポートしたイメージにmbrがない場合、起動できません。
> 現在のOSにおいて、`/boot`と`/home`が独立したパーティションである場合、エクスポートしたイメージにもこの2つの独立したパーティションが必要です。
> 

### イメージのエクスポート
実際のニーズに応じて、それぞれの方式を選択してイメージをエクスポートします。
<dx-tabs>
::: プラットフォームツールを使用してイメージをエクスポートする[](id:Useplatform)
VMWare vCenter ConverterやCitrix XenConvertなどの仮想化プラットフォームのイメージエクスポートツールを使用します。詳細は各プラットフォームのエクスポートツールドキュメントをご参照ください。
>? 現在、Tencent Cloudのサービス移行は、qcow2、vhd、raw、およびvmdk形式のイメージをサポートします。
>
:::
::: コマンドを使用してイメージをエクスポートする[](id:ExportImageForUsingCommand)
>! コマンドを使用してイメージを手動エクスポートするとリスクが大きいです（例えば、IOがビジーの時にファイルシステムのmetadataが輻輳する可能性があるなど）。イメージをエクスポートした後、[イメージの確認](#CheckMirror) で誤りがないことを確認することを推奨します。
>

[qemu-imgコマンドの使用](#qemuimg)または[ddコマンドの使用](#dd)のうちどちらかの方式を選択して、イメージをエクスポートすることができます。
- **`qemu-img`コマンドを使用**<span id="qemuimg"></span>
 1. 以下のコマンドを実行し、必要なパッケージをインストールします。このドキュメントはDebianを例としており、公開バージョンが異なればパッケージも異なる可能性があります。実際の状況に応じて調整してください。例えば、CentOSのパッケージ名は`qemu-img`です。
```
apt-get install qemu-utils
```
 2. 以下のコマンドを実行し、`/dev/sda`を`/mnt/sdb/test.qcow2`にエクスポートします。
```
sudo qemu-img convert -f raw -O qcow2 /dev/sda /mnt/sdb/test.qcow2
``` このうち、`/mnt/sdb`は、マウントされた新しいディスクまたはその他のネットワークストレージです。
その他の形式に変換する必要がある場合、`-O`のパラメータ値を変更してください。変更可能なパラメータ値は以下のとおりです。
<span id="-OParameterValue"></span>
<table>
	<tr><th>パラメータ値</th><th>意味</th></tr>
	<tr><td>qcow2</td><td>qcow2 形式</td></tr>
	<tr><td>vpc</td><td>vhd 形式</td></tr>
	<tr><td>vmdk</td><td>vmdk 形式</td></tr>
	<tr><td>raw</td><td>形式なし</td></tr>
</table>
- **`dd`コマンドを使用**<span id="dd"></span>
例えば、以下のコマンドを実行し、raw形式のイメージをエクスポートします。
```
sudo dd if=/dev/sda of=/mnt/sdb/test.imag bs=1K count=$count
``` このうち、`count`パラメータはパーティションのコピーが必要な数であり、`fdisk`コマンドでその数値を検出することができます。ディスクすべてをコピーする必要がある場合、`count`パラメータは無視できます。
例えば、以下のコマンドを実行し、`/dev/sda` のパーティション数を確認します。
```
fdisk -lu /dev/sda
``` 以下に類似した結果が返されます。
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
``` `fdisk`コマンドのリターン結果により、sda1の終了位置が41945087 \* 512バイトの位置であるため、`count`を20481Mに設定すれば良いことが分かります。
>? `dd`コマンドでエクスポートしたイメージがraw形式であるため、[qcow2，vhdまたはその他のイメージ形式への変換](#ImageFormatConversion)を推奨します。
>
:::
</dx-tabs>




### イメージ形式の変換（任意）[](id:ImageFormatConversion)
変換イメージ形式を参照し、`qemu-img` を使用して、イメージファイルをサポート形式に変換します。


<span id="CheckMirror"></span>
### イメージの確認
>? 「サービスを停止せずにイメージを作成した」などの理由により、作成したイメージファイルシステムが破損している可能性があります。イメージ作成後にエラーの有無を確認することをお勧めします。
>
イメージ形式が、現在プラットフォームがサポートする形式と一致する場合、イメージ確認ファイルシステムを直接開くことができます。例えば、Windowsプラットフォームはvhd形式のイメージを直接追加することができます。Linuxプラットフォームではqemu-nbdを使用してqcow2形式のイメージを開くことができ、Xenプラットフォームはvhdファイルを直接開くことができます。このドキュメントではLinuxプラットフォームを例として以下の確認手順を説明します。
1. 以下のコマンドを順番に実行し、nbdモジュールがあるかどうかを確認します。
```
modprobe nbd
```
```
lsmod | grep nbd
```
リターン結果は以下のとおりで、nbdモジュールがあることを示しています。リターン結果が何も出なかった場合、カーネルコンパイルオプション`CONFIG_BLK_DEV_NBD`がオンかどうかを確認してください。オンでない場合、システムを変更するか、`CONFIG_BLK_DEV_NBD`コンパイルオプションをオンにしてから再度カーネルをコンパイルする必要があります。
![](https://main.qcloudimg.com/raw/190bd78d60c7340fb95210f60e126105.png)
2. 以下のコマンドを順番に実行し、イメージを確認します。
```
qemu-nbd -c /dev/nbd0 xxxx.qcow2
```
```
mount /dev/nbd0p1 /mnt
```
`qemu-nbd`コマンドを実行すると、`/dev/nbd0`は`xxx.qcow2` 内のコンテンツにマッピングされます。また、`/dev/nbd0p1`はこの仮想ディスクの最初のパーティションであることを示し、nbd0p1が存在しないかmountが完了しない場合、イメージエラーである可能性が高いです。
また、イメージをアップロードする前に、CVMを起動してイメージファイルを使用できるかどうかをテストすることもできます。

