## 概要

このドキュメントでは、ローカルまたはその他のプラットフォームのLinuxサーバーシステムディスクイメージの作成について説明します。

## 操作手順

### 準備作業

システムディスクイメージを作成してエクスポートする前に、以下の操作を行ってください：

<dx-alert infotype="explain" title="">
データディスクイメージをエクスポートする場合は、この手順をスキップしてください。
</dx-alert>



#### OSのパーティションと起動方法の確認
1. 次のコマンドを実行して、OSパーティションがGPTパーティションであるかどうかを確認します。
```
sudo parted -l /dev/sda | grep 'Partition Table'
```
 - 返された結果がmsdosである場合、MBRパーティションであることを示しているので、次の手順を実行してください。
 - 返された結果がgptである場合、GPTパーティションであることを示します。現在移行サービスはGPTパーティションをサポートしていないため、[チケットを提出](https://console.intl.cloud.tencent.com/workorder/category)することでフィードバックしてください。
2. 次のコマンドを実行して、OSがEFIモードで起動するかどうかを確認します。
```
sudo ls /sys/firmware/efi
```
 - ファイルが存在する場合、現在のOSがEFIモードで起動することを示しているので、[チケットを提出](https://console.intl.cloud.tencent.com/workorder/category)することでフィードバックしてください。
 - ファイルが存在しない場合、次の手順を実行してください。

#### システムキーファイルの確認
確認を必要とするシステムキーファイルには、以下のファイルを含みますがこれらに限定されません：
<dx-alert infotype="explain" title="">
関連するリリースバージョンの基準に従って、システムキーファイルの位置と権限が正しいことを保証して、正常に読み書きできます。
</dx-alert>

- `/etc/grub2.cfg`：kernelパラメータではuuidを使用してrootをマウントすることを推奨します。その他の方式（root=`/dev/sda`など）では、システムが起動できない可能性があります。マウントの手順は以下のとおりです：
    1. 次のコマンドを実行して、`/root`のファイルシステム名を取得します。
```
df -TH
```
返された結果は以下のとおりです。`/root`ファイルシステム名が`/dev/vda1 `であることを示します。
![](https://qcloudimg.tencent-cloud.cn/raw/aff304e37691f0f8caa7efc02d60522a.png)
    2. 次のコマンドを実行して、UUIDを取得します。
```
blkid /dev/vda1
```
<dx-alert infotype="explain" title="">
ファイルシステムのUUIDは固定されていません。定期的に確認し、更新してください。例えば、ファイルシステムを再フォーマットすると、ファイルシステムのUUIDが変更されます。
</dx-alert>
    3. 次のコマンドを実行して、VIエディタを利用して`/etc/fstab`ファイルを開きます。
```
vi /etc/fstab
```
    4. **I** を押して、編集モードに入ります。
    5. カーソルをファイルの最後に移動し、**Enter**を押して、次の内容を追加します。前の例と組み合わせて以下を追加します：
```
UUID=d489ca1c-xxxx-4536-81cb-ceb2847f9954 /data  ext4 defaults     0   0
```
    6. **Esc**を押して、**:wq**を入力し、**Enter**を押してください。設定を保存して、エディターを終了します。
- `/etc/fstab`：その他のハードディスクをマウントしないでください。移行後に、ディスクが破損するため、システムが起動できない可能性があります。
- `/etc/shadow`：権限が正常で、読み書き可能です。



#### ソフトウエアのアンインストール
競合の可能性がるドライバーとソフトウェアをアンインストールします（VMware tools、Xen tools、Virtualbox GuestAdditionsおよび基盤となるドライバーを備える一部のソフトウェアを含む）。

#### virtioドライバーの確認
操作の詳細については、[LinuxでのVirtioドライバーの確認](https://intl.cloud.tencent.com/document/product/213/9929)をご参照ください。

#### cloud-initのインストール
インストールの詳細については、[Linuxでのcloud-initのインストール](https://intl.cloud.tencent.com/document/product/213/12587)をご参照ください。

#### その他のハードウェア構成の確認
クラウド移行後のハードウェアの変更には、以下が含まれますが、これらに限定されません：
 - グラフィックカードがCirrus VGAに変更されました。
 - ディスクがVirtio Diskに変更されました。デバイス名はvda、vdbです。
 - ENIがVirtio Nicに変更されました。デフォルトではeth0のみを提供します。

### パーティションとサイズの検索
次のコマンドを実行して、現在のOSのパーティション形式を確認してコピーが必要なパーティションとサイズを決定します。
```
mount
```
以下の返された結果を例として説明します：
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
ルートパーティションは`/dev/sda1`に配置されています。`/boot`と`/home`には独立したパーティションがありません。sda1にはbootパーティションを含み、mbrがないため、sdaをすべてコピーするだけで良いということが分かります。
<dx-alert infotype="notice" title="">
- エクスポートされたイメージには少なくともルートパーティションとmbrを含む必要があります。エクスポートされたイメージにmbrがない場合、起動できません。
- 現在のOSでは、`/boot`と`/home`が独立したパーティションである場合、エクスポートされたイメージにはこの2つの独立したパーティションを更に含む必要があります。
</dx-alert>



### イメージのエクスポート
実際のニーズに応じて、それぞれの方式を選択してイメージをエクスポートします。
<dx-tabs>
::: プラットフォームツールを使用してイメージをエクスポートする[](id:Useplatform)
VMWare vCenter ConverterまたはCitrix XenConvertなどの仮想化プラットフォームのイメージエクスポートツールを使用します。詳細については、各プラットフォームのエクスポートツールドキュメントをご参照ください。

<dx-alert infotype="explain" title="">
現在、Tencent Cloudのサービス移行は、qcow2、vhd、raw、およびvmdk形式のイメージをサポートしています。
</dx-alert>


:::
::: コマンドを使用してイメージをエクスポートする[](id:ExportImageForUsingCommand)

<dx-alert infotype="notice" title="">
コマンドを使用してイメージを手動でエクスポートすると、リスクが大きいため（例えば、IOがビジーの時にファイルシステムのmetadataが輻輳する可能性があるなど）、イメージをエクスポートした後、[イメージの確認](#CheckMirror)で誤りがないことを確認することを推奨します。
</dx-alert>



[qemu-imgコマンドの使用](#qemuimg)または[ddコマンドの使用](#dd)のいずれかの方式を選択して、イメージをエクスポートできます：
- **`qemu-img`コマンドの使用** [](id:qemuimg)
 1. 次のコマンドを実行して、必要なパッケージをインストールします。このドキュメントでは、Debianを例として取り上げます。リリースバージョンが異なればパッケージも異なる可能性があります。実際の状況に応じて調整してください。例えば、CentOSのパッケージ名は`qemu-img`です。
```
apt-get install qemu-utils
```
 2. 次のコマンドを実行して、`/dev/sda`を`/mnt/sdb/test.qcow2`にエクスポートします。
```
sudo qemu-img convert -f raw -O qcow2 /dev/sda /mnt/sdb/test.qcow2
```そのうち、`/mnt/sdb`は、マウントされた新しいディスクまたはその他のネットワークストレージです。
その他の形式に変換する必要がある場合、`-O`のパラメータ値を変更してください。変更可能なパラメータ値は以下のとおりです：
[](id:OParameterValue)
<table>
	<tr><th>パラメータ値</th><th>意味</th></tr>
	<tr><td>qcow2</td><td>qcow2形式</td></tr>
	<tr><td>vpc</td><td>vhd形式</td></tr>
	<tr><td>vmdk</td><td>vmdk形式</td></tr>
	<tr><td>raw</td><td>形式なし</td></tr>
</table>
- **`dd`コマンドの使用** [](id:dd)
例えば、次のコマンドを実行して、raw形式のイメージをエクスポートします。
```
sudo dd if=/dev/sda of=/mnt/sdb/test.imag bs=1K count=$count
```そのうち、`count`パラメータはパーティションのコピーが必要な数です。`fdisk`コマンドでその数値を検出することができます。ディスクをすべてコピーする必要がある場合、`count`パラメータは無視できます。
例えば、次のコマンドを実行して、`/dev/sda`のパーティション数を確認します。
```
fdisk -lu /dev/sda
``` 以下に類似した結果が返されます：
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
``` `fdisk`コマンドの返された結果により、sda1の終了位置が41945087\*512バイトの位置である場合、`count`を20481Mに設定すれば良いことが分かります。


<dx-alert infotype="explain" title="">
`dd`コマンドでエクスポートしたイメージがraw形式です。[qcow2、vhdまたはその他のイメージ形式への変換](#ImageFormatConversion)を推奨します。
</dx-alert>


:::
</dx-tabs>




### イメージ形式の変換（オプション）[](id:ImageFormatConversion)
イメージ形式の変換を参照し、`qemu-img`を使用して、イメージファイルをサポート形式に変換します。



### イメージのチェック[](id:CheckMirror)

<dx-alert infotype="explain" title="">
サービスを停止せずにイメージを作成するか、またはその他の理由により、作成したイメージファイルシステムが破損している可能性があります。イメージ作成後にエラーの有無を確認することをお勧めします。
</dx-alert>


イメージ形式が、現在プラットフォームがサポートする形式と一致する場合、イメージチェックファイルシステムを直接開くことができます。例えば、Windowsプラットフォームではvhd形式のイメージを直接追加できます。Linuxプラットフォームではqemu-nbdを使用してqcow2形式のイメージを開くことができ、Xenプラットフォームではvhdファイルを直接開くことができます。このドキュメントでは、Linuxプラットフォームを例として以下の確認手順を説明します：
1. 次のコマンドを順番に実行して、nbdモジュールがあるかどうかを確認します。
```
modprobe nbd
```
```
lsmod | grep nbd
```
以下の結果が返された場合、nbdモジュールがあることを示しています。返された結果がNULLである場合、カーネルコンパイルオプション`CONFIG_BLK_DEV_NBD`がオンにするかどうかを確認してください。オンにしない場合、システムを変更するか、`CONFIG_BLK_DEV_NBD`コンパイルオプションをオンにしてからカーネルを再コンパイルする必要があります。
![](https://main.qcloudimg.com/raw/190bd78d60c7340fb95210f60e126105.png)
2. 次のコマンドを順番に実行し、イメージを確認します。
```
qemu-nbd -c /dev/nbd0 xxxx.qcow2
```
```
mount /dev/nbd0p1 /mnt
```
`qemu-nbd`コマンドを実行すると、`/dev/nbd0`は`xxx.qcow2`の内容にマッピングされます。また、`/dev/nbd0p1`はこの仮想ディスクの最初のパーティションであることを示し、nbd0p1が存在しないかmountに成功しない場合、イメージエラーである可能性が高いです。
また、イメージをアップロードする前に、CVMを起動してイメージファイルを使用できるかどうかをテストすることもできます。

