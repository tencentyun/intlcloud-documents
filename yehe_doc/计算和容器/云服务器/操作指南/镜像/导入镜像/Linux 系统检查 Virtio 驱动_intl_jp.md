## ユースケース
CVMシステムカーネルがTencent Cloudで正常に動作するために、Virtioドライバー（ブロックデバイスドライバー`virtio_blk`とNICドライバー`virtio_net`を含む)をサポートする必要があります。カスタマイズイメージで作成されたCVMインスタンスが起動できないことを避けるためには、イメージをインポートする前に、イメージがソースサーバーでvirtioドライバーをサポートしているかを確認してください。サポートしていない場合、Virtioドライバーに対するイメージのサポートを修正する必要があります。本書では、CentOSを例として、イメージをインポートする前に、イメージがvirtioドライバーをサポートしているかを確認する方法、およびVirtioドライバーに対するイメージのサポートを修正する方法を説明します。　

## 操作手順


### 手順1：カーネルがVirtioドライバーをサポートしているかの確認[](id:CheckVirtioForKernel)
次のコマンドを実行して、現在のカーネルがVirtioドライバーをサポートしているかを確認します。
```shellsession
grep -i virtio /boot/config-$(uname -r)
```
以下のような結果が返されます：
![](https://main.qcloudimg.com/raw/8c32c3dd554700a0c17ff0c7e5675090.png)
 - 返された結果にパラメータ`CONFIG_VIRTIO_BLK`とパラメータ`CONFIG_VIRTIO_NET`の値が`m`である場合、[手順2](#CheckVirtioForInitramfs)を実行してください。
 - 返された結果にパラメータ`CONFIG_VIRTIO_BLK`とパラメータ`CONFIG_VIRTIO_NET`の値が`y`である場合、このOSにVirtioドライバーが含まれているため、カスタマイズイメージをTencent Cloudに直接インポートできます。詳細については、[イメージのインポートの概要](https://intl.cloud.tencent.com/document/product/213/4945)をご参照ください。
 - 返された結果にパラメータ`CONFIG_VIRTIO_BLK`とパラメータ`CONFIG_VIRTIO_NET`の情報がない場合、このOSではイメージをTencent Cloudに**インポートできない**ため、[カーネルをダウンロードしてコンパイル](#DownloadCompileKernel)してください。


### 手順2：一時ファイルシステムにVirtioドライバーが含まれているかの確認[](id:CheckVirtioForInitramfs)
[手順1](#CheckVirtioForKernel)の実行結果にパラメータの値が`m`である場合、一時ファイルシステム`initramfs`または`initrd`に`virtio`ドライバーが含まれているかを確認する必要があります。OSによって、コマンドを実行してください：
- CentOS 6/CentOS 7/CentOS 8/RedHat 6/RedHat 7の場合
```shellsession
lsinitrd /boot/initramfs-$(uname -r).img | grep virtio
```
- RedHat 5/CentOS 5の場合
```shellsession
mkdir -p /tmp/initrd && cd /tmp/initrd
zcat /boot/initrd-$(uname -r).img | cpio -idmv
find . -name "virtio*"
```
- Debian/Ubuntu の場合
```shellsession
lsinitramfs /boot/initrd.img-$(uname -r) | grep virtio
```

以下のような結果が返されます：
<img src="https://main.qcloudimg.com/raw/a5e22f75f48ce26a6b03f65588a52877.png" />
つまり、<code>Initramfs</code>には、<code>virtio_blk</code>ドライバーと、それに依存する<code>virtio.ko</code>、<code>virtio_pci.ko</code>および<code>virtio_ring.ko</code>が含まれているため、カスタマイズイメージをTencent Cloudに直接インポートできます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/4945">イメージのインポートの概要</a>をご参照ください。
<code>Initramfs</code>または<code>initrd</code>に<code>virtio</code>ドライバーが含まれていない場合、[手順3](#ReconfigureInitramfs)を実行してください。


### 手順3：一時ファイルシステムの再設定[](id:ReconfigureInitramfs)
[手順2](#CheckVirtioForInitramfs)の実行結果により、一時ファイルシステム`initramfs`または`initrd`に`virtio`ドライバーが含まれていない場合、一時ファイルシステム`initramfs`または`initrd`を再設定して`virtio`ドライバーを含めるようにする必要があります。OSによって対応する操作を選択してください。
 - CentOS 8/RedHat 8の場合
```shellsession
mkinitrd -f --allow-missing --with=virtio_blk --preload=virtio_blk --with=virtio_net --preload=virtio_net --with=virtio_console --preload=virtio_console /boot/initramfs-$(uname -r).img $(uname -r)
```
 - CentOS 6/CentOS 7/RedHat 6/RedHat 7の場合
```shellsession
mkinitrd -f --allow-missing --with=xen-blkfront --preload=xen-blkfront --with=virtio_blk --preload=virtio_blk --with=virtio_pci --preload=virtio_pci --with=virtio_console --preload=virtio_console /boot/initramfs-$(uname -r).img $(uname -r)
```
 - RedHat 5/CentOS 5の場合
```shellsession
mkinitrd -f --allow-missing --with=xen-vbd  --preload=xen-vbd --with=xen-platform-pci --preload=xen-platform-pci --with=virtio_blk --preload=virtio_blk --with=virtio_pci --preload=virtio_pci --with=virtio_console --preload=virtio_console /boot/initrd-$(uname -r).img $(uname -r)
```
 - Debian/Ubuntu の場合
```shellsession
echo -e 'xen-blkfront\nvirtio_blk\nvirtio_pci\nvirtio_console' >> /etc/initramfs-tools/modules
mkinitramfs -o /boot/initrd.img-$(uname -r)
```

## 付録
### カーネルのダウンロードとコンパイル[](id:DownloadCompileKernel)

#### カーネルのインストールパッケージのダウンロード
1. 次のコマンドを実行して、カーネルのコンパイルに必要なコンポーネントをインストールします。
```shellsession
yum install -y ncurses-devel gcc make wget
```
2. 次のコマンドを実行して、現在のシステムで使用されているカーネルのバージョンを確認します。
```shellsession
uname -r
```
以下のような結果が返された場合、現在のシステムで使用されているカーネルのバージョンは`2.6.32-642.6.2.el 6.x 86_64`です。
![](https://main.qcloudimg.com/raw/739b19fc7af96d6de7872df0a498b7b6.png)
3. [Linuxカーネルのダウンロードページ](https://www.kernel.org/pub/linux/kernel/?spm=a2c4g.11186623.2.26.7e4179b4zo5WVJ)に進み、対応するカーネルバージョンまたは一番近いカーネルバージョンのソースコードをダウンロードします。
例えば、カーネルのバージョンが`2.6.32-642.6.2.el 6.x 86_64`の場合、`linux-2.6.32.tar.gz`インストールパッケージをダウンロードします。ダウンロード先は`https://mirrors.edge.kernel.org/pub/linux/kernel/v2.6/linux-2.6.32.tar.gz`です。
4. 次のコマンドを実行して、ディレクトリを切り替えます。
```shellsession
cd /usr/src/
```
5. 次のコマンドを実行して、インストールパッケージをダウンロードします。
```shellsession
wget https://mirrors.edge.kernel.org/pub/linux/kernel/v2.6/linux-2.6.32.tar.gz
```
6. 次のコマンドを実行して、インストールパッケージを解凍します。
```shellsession
tar -xzf linux-2.6.32.tar.gz
```
7. 次のコマンドを実行して、接続を確立します。
```shellsession
ln -s linux-2.6.32 linux
```
8. 次のコマンドを実行して、ディレクトリを切り替えます。
```shellsession
cd /usr/src/linux
```

#### カーネルのコンパイル

1. 次のコマンドを順次実行して、カーネルをコンパイルします。
```shellsession
make mrproper
cp /boot/config-$(uname -r) ./.config
make menuconfig
```
下図に示すように、「Linux Kernel vX.X.XX Configuration」画面に入ります。
![](https://main.qcloudimg.com/raw/72c3bea10627aaef022f1a72b72ac79a.png)
<dx-alert infotype="explain" title="">
 「Linux Kernel vX.X.XX Configuration」」画面に入っていない場合、[手順18](#OptionalStep)を実行してください。
「Linux Kernel vX.X.XX Configuration」画面に入ります。
 - 「Tab」または「↑」、「↓」方向キーを押してカーソルを移動します。
 - 「Enter」キーを押して、カーソルで選択された項目を選択または実行します。
 - スペースキーを押して、カーソルで選択された項目を選択します。「\*」はカーネルにコンパイルすること、「M」はモジュールとしてコンパイルすることを意味します。 
</dx-alert>
2. 「↓」キーを押してカーソルを「Virtualization」に移動し、スペースキーを押して「Virtualization」を選択します。
3. 「Enter」を押してVirtualization詳細画面に入ります。
4. 下図に示すように、Virtualization詳細画面で、Kernel-based Virtual Machine(KVM)supportオプションにチェックを入れているかを確認します。
![](https://main.qcloudimg.com/raw/d5614d31ebaed0f0b270dc1046b9ff2e.png)
チェックを入れていない場合、スペースキーを押して「Kernel-based Virtual Machine(KVM)support」オプションを選択してください。
5. 「Esc」を押して「Linux Kernel vX.X.XX Configuration」メイン画面に戻ります。
6. 「↓」キーを押してカーソルを「Processor type and features」に移動し、「Enter」キーを押してProcessor type and features詳細画面に入ります。
7. 「↓」キーを押してカーソルを「Paravirtualized guest support」に移動し、「Enter」キーを押してParavirtualized guest support詳細画面に入ります。
8. 下図に示すように、Paravirtualized guest support詳細画面で、「KVM paravirtualized clock」と「KVM Guest support」にチェックを入れているかを確認します。
![](https://main.qcloudimg.com/raw/2e49f9b46ecb9f9d272db36dffbade07.png)
チェックを入れていない場合、スペースキーを押して「KVM paravirtualized clock」と「KVM Guest support」オプションを選択してください。
9. 「Esc」を押して「Linux Kernel vX.X.XX Configuration」メイン画面に戻ります。
10. 「↓」キーを押してカーソルを「Device Drivers」に移動し、「Enter」キーを押してDevice Drivers詳細画面に入ります。
11. 「↓」キーを押してカーソルを「Block devices」に移動し、「Enter」キーを押してBlock devices詳細画面に入ります。
12. 下図に示すように、Block devices詳細画面で、「Virtio block driver(EXPERIMENTAL)」にチェックを入れているかを確認します。
![](https://main.qcloudimg.com/raw/79f3e29a6d77224a164c6c716e41fa84.png)
チェックされていない場合は、スペースキーを押して「Virtio block driver(EXPERIMENTAL)」オプションにチェックを入れてください。
13. 「Esc」を押してDevice Drivers詳細画面に戻ります。
14. 「↓」キーを押してカーソルを「Network device support」に移動し、「Enter」キーを押してNetwork device support詳細画面に入ります。
15. Network device support詳細画面では、「Virtio network driver(EXPERIMENTAL)」がチェックされているかどうかを確認します。以下の図の通りです：
![](https://main.qcloudimg.com/raw/811388c89393882ea83bceb7a00bc1b7.png)
チェックを入れていない場合、スペースキーを押して「Virtio network driver(EXPERIMENTAL)」オプションを選択してください。
16. 「Esc」を押してカーネル設定画面を終了し、ポップアップしたメッセージに従って、「YES」を選択し、`.config`ファイルを保存します。
17. [手順1：カーネルがVirtioドライバーをサポートしているかの確認](#CheckVirtioForKernel)に従って、Virtioドライバーが正しく設定されているかを確認します。
18. [](id:OptionalStep)（オプション）次のコマンドを実行し、`.config`ファイルを手動で編集します。
<dx-alert infotype="explain" title="">
 以下のいずれかの条件を満たしている場合、次の操作をお勧めします：
 - チェックした結果、カーネルにVirtioドライバーに関する設定情報がありません。
 - カーネルをコンパイルする時、カーネルの設定画面に入ることができない、または`.config`ファイルを保存できません。
</dx-alert>
```shellsession
make oldconfig
make prepare
make scripts
make
make install
```
19. 次のコマンドを順次実行して、Virtioドライバーのインストール状態を確認します。
```shellsession
find /lib/modules/"$(uname -r)"/ -name "virtio.*" | grep -E "virtio.*"
grep -E "virtio.*" < /lib/modules/"$(uname -r)"/modules.builtin
```
任意のコマンドの実行結果に`virtio_blk`、`virtio_pci.virtio_console`などのファイルリストが出力された場合、Virtioドライバーが正しくインストールされています。




