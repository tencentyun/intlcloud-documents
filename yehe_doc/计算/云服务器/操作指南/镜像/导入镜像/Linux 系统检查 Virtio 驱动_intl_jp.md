## 概要
CVMシステムカーネルは、Tencent Cloud上で正常に動作するために、Virtioドライバー（ブロックデバイスドライバー`virtio_blk`とNICドライバー`virtio_net`を含む)をサポートする必要があります。カスタムイメージで作成されたCVMインスタンスが起動しない不具合を未然に防ぐには、イメージをインポートする前に、イメージがソースサーバーでVirtioドライバーをサポートしているかどうかを確認してください。このドキュメントでは、CentOSを例に、イメージをインポートする前に、イメージがVirtioドライバーをサポートしているかどうかを確認する方法を説明します。
## 操作手順

<span id="CheckVirtioForKernel"></span>
### ステップ1：カーネルがVirtioドライバーをサポートしているかどうかの確認
次のコマンドを実行して、現在カーネルがVirtioドライバーをサポートしているかどうかを確認します。
```
grep -i virtio /boot/config-$(uname -r)
```
以下のような結果が返されます：
![](https://main.qcloudimg.com/raw/8c32c3dd554700a0c17ff0c7e5675090.png)
 - 返された結果にパラメータ`CONFIG_VIRTIO_BLK`とパラメータ`CONFIG_VIRTIO_NET`の値が`m`である場合、[ステップ2](#CheckVirtioForInitramfs)を実行してください。
 - 返された結果にパラメータ`CONFIG_VIRTIO_BLK`とパラメータ`CONFIG_VIRTIO_NET`の値が`y`である場合、このOSにVirtioドライバーが含まれていることを示し、カスタムイメージをTencent Cloudに直接インポートすることができます。操作の詳細については[イメージのインポートの概要](https://intl.cloud.tencent.com/document/product/213/4945)をご参照ください。
 - 返された結果にパラメータ`CONFIG_VIRTIO_BLK`とパラメータ`CONFIG_VIRTIO_NET`の情報がない場合、このOSのイメージをTencent Cloudに**インポートできない**ことを意味します。[カーネルをダウンロードしてコンパイル](#DownloadCompileKernel)してください。

<span id="CheckVirtioForInitramfs"></span>
### ステップ2：一時ファイルシステムにVirtioドライバーが含まれているかどうかの確認
[ステップ1](#CheckVirtioForKernel)でパラメーターの値がmである場合、さらに一時ファイルシステム`initramfs`またはinitrdに`virtio`ドライバーが含まれているかどうかを確認する必要があります。OSによって、対応するコマンドを実行してください。
- CentOS 6/CentOS 7/CentOS 8/RedHat 6/RedHat 7の場合：
```
lsinitrd /boot/initramfs-$(uname -r).img | grep virtio
```
- RedHat 5/CentOS 5の場合：
```
mkdir -p /tmp/initrd && cd /tmp/initrd
zcat /boot/initrd-$(uname -r).img | cpio -idmv
find . -name "virtio*"
```
- Debian/Ubuntu の場合：
```
lsinitramfs /boot/initrd.img-$(uname -r) | grep virtio
```

以下のような結果が返されます：
<img src="https://main.qcloudimg.com/raw/a5e22f75f48ce26a6b03f65588a52877.png" />
つまり、<code>Initramfs</code>には、<code>virtio_blk</code>ドライバーと、それに依存する<code>virtio.ko</code>、<code>virtio_pci.ko</code>および<code>virtio_ring.ko</code>が含まれていることが分かり、カスタムイメージをTencent Cloudに直接インポートすることができます。操作の詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/4945">イメージのインポートの概要</a>をご参照ください。
<code>Initramfs</code>または<code>initrd</code>に<code>virtio</code>ドライバーが含まれていない場合、[ステップ3](#ReconfigureInitramfs)を実行してください。

<span id="ReconfigureInitramfs"></span>
### ステップ3：一時ファイルシステムの再構成
[ステップ2](#CheckVirtioForInitramfs)で一時ファイルシステム`initramfs`または`initrd`に`virtio`ドライバーが含まれていないことが判明した場合は、一時ファイルシステム`initramfs`または`initrd`を再構成して`virtio`ドライバーを含むようにする必要があります。OSによって、対応する操作を選択してください。
 - CentOS 8/RedHat 8 の場合：
```shellsession
mkinitrd -f --allow-missing --with=virtio_blk --preload=virtio_blk --with=virtio_net --preload=virtio_net --with=virtio_console --preload=virtio_console /boot/initramfs-$(uname -r).img $(uname -r)
```
 - CentOS 6/CentOS 7/RedHat 6/RedHat 7の場合：
```
cp /boot/initramfs-$(uname -r).img /boot/initramfs-$(uname -r).img.bak
mkinitrd -f --with=virtio_blk --with=virtio_pci /boot/initramfs-$(uname -r).img $(uname -r)
```
 - RedHat 5/CentOS 5の場合：
```
cp /boot/initrd-$(uname -r).img /boot/initrd-$(uname -r).img.bak
mkinitrd -f --with=virtio_blk --with=virtio_pci /boot/initrd-$(uname -r).img $(uname -r)
```
 - Debian/Ubuntu の場合：
```
echo -e "virtio_pci\nvirtio_blk" >> /etc/initramfs-tools/modules
update-initramfs  -u
```

## 付録
<span id="DownloadCompileKernel"></span>
### カーネルのダウンロードとコンパイル

#### カーネルのインストールパッケージのダウンロード
1. 次のコマンドを実行して、カーネルのコンパイルに必要なコンポーネントをインストールします。
```
yum install -y ncurses-devel gcc make wget
```
2. 次のコマンドを実行して、現在システムで使用されているカーネルバージョンを確認します。
```
uname -r
```
以下のような結果が返され、現在システムで使用されているカーネルバージョンが`2.6.32-642.6.2.el 6.x 86_64`であることを示します。
![](https://main.qcloudimg.com/raw/739b19fc7af96d6de7872df0a498b7b6.png)
3. [Linuxカーネルのダウンロードページ](https://www.kernel.org/pub/linux/kernel/?spm=a2c4g.11186623.2.26.7e4179b4zo5WVJ)に進み、対応するカーネルバージョンのソースコードをダウンロードします。
例えば、`2.6.32-642.6.2.el 6.x 86_64`バージョンのカーネルは、`linux-2.6.32.tar.gz`のインストールパッケージをダウンロードし、そのダウンロードパスは`https://mirrors.edge.kernel.org/pub/linux/kernel/v2.6/linux-2.6.32.tar.gz`です。
4. 次のコマンドを実行して、ディレクトリを切り替えます。
```
cd /usr/src/
```
5. 次のコマンドを実行して、インストールパッケージをダウンロードします。
```
wget https://mirrors.edge.kernel.org/pub/linux/kernel/v2.6/linux-2.6.32.tar.gz
```
6. 次のコマンドを実行して、インストールパッケージを解凍します。
```
tar -xzf linux-2.6.32.tar.gz
```
7. 次のコマンドを実行して、接続を確立します。
```
ln -s linux-2.6.32 linux
```
8. 次のコマンドを実行して、ディレクトリを切り替えます。
```
cd /usr/src/linux
```

#### カーネルのコンパイル

1. 次のコマンドを順次実行して、カーネルをコンパイルします。
```
make mrproper
symvers_path=$(find /usr/src/ -name "Module.symvers")
test -f $symvers_path && cp $symvers_path .
cp /boot/config-$(uname -r) ./.config
make menuconfig
```
「Linux Kernel vX.X.XX Configuration」画面に入ります。以下の通りです。
![](https://main.qcloudimg.com/raw/72c3bea10627aaef022f1a72b72ac79a.png)
> 「Linux Kernel vX.X.XX Configuration」画面が表示されない場合は、[ステップ18](#OptionalStep)を実行してください。
> 「Linux Kernel vX.X.XX Configuration」画面に入ります。
> - 「Tab」または「↑」、「↓」方向キーを押してカーソルを移動します。
> - 「Enter」キーを押して、カーソルで選択された項目を選択または実行します。
> - スペースキーを押して、カーソルで選択された項目を選択し、「\*」はカーネルにコンパイルすることを表し、「M」はモジュールとしてコンパイルすることを表します。 
> 
2. 「↓」キーを押してカーソルを「Virtualization」に移動し、スペースキーを押して「Virtualization」を選択します。
3. 「Enter」を押してVirtualization詳細画面に入ります。
4. Virtualization詳細画面では、Kernel-based Virtual Machine(KVM)supportオプションがチェックされているかどうかを確認します。以下の通りです。
![](https://main.qcloudimg.com/raw/d5614d31ebaed0f0b270dc1046b9ff2e.png)
チェックされていない場合は、スペースキーを押して「Kernel-based Virtual Machine(KVM)support」オプションにチェックを入れてください。
5. 「Esc」を押して「Linux Kernel vX.X.XX Configuration」主画面に戻ります。
6. 「↓」キーを押してカーソルを「Processor type and features」に移動し、「Enter」キーを押してProcessor type and features詳細画面に入ります。
7. 「↓」キーを押してカーソルを「Paravirtualized guest support」に移動し、「Enter」キーを押してParavirtualized guest support詳細画面に入ります。
8. Paravirtualized guest support詳細画面では、「KVM paravirtualized clock」と「KVM Guest support」がチェックされているかどうかを確認します。以下の通りです。
![](https://main.qcloudimg.com/raw/2e49f9b46ecb9f9d272db36dffbade07.png)
チェックされていない場合は、スペースキーを押して「KVM paravirtualized clock」と「KVM Guest support」オプションにチェックを入れてください。
9. 「Esc」を押して「Linux Kernel vX.X.XX Configuration」主画面に戻ります。
10. 「↓」キーを押してカーソルを「Device Drivers」に移動し、「Enter」キーを押してDevice Drivers詳細画面に入ります。
11. 「↓」キーを押してカーソルを「Block devices」に移動し、「Enter」キーを押してBlock devices詳細画面に入ります。
12. Block devices詳細画面では、「Virtio block driver(EXPERIMENTAL)」がチェックされているかどうかを確認します。以下の通りです。
![](https://main.qcloudimg.com/raw/79f3e29a6d77224a164c6c716e41fa84.png)
チェックされていない場合は、スペースキーを押して「Virtio block driver(EXPERIMENTAL)」オプションにチェックを入れてください。
13. 「Esc」を押してDevice Drivers詳細画面に戻ります。
14. 「↓」キーを押してカーソルを「Network device support」に移動し、「Enter」キーを押してNetwork device support詳細画面に入ります。
15. Network device support詳細画面では、「Virtio network driver(EXPERIMENTAL)」がチェックされているかどうかを確認します。以下の通りです。
![](https://main.qcloudimg.com/raw/811388c89393882ea83bceb7a00bc1b7.png)
チェックされていない場合は、スペースキーを押して「Virtio network driver(EXPERIMENTAL)」オプションにチェックを入れてください。
16. 「Esc」キーを押してカーネル設定画面を終了し、「YES」を選択して.`config`ファイルを保存します。
17. [ステップ1：カーネルがVirtioドライバーをサポートしているかどうかの確認](#CheckVirtioForKernel)をご参照し、Virtioドライバーが正しく設定されているかどうかを検証します。
18. <span id="OptionalStep"></span>（オプション）次のコマンドを実行し、`.config`ファイルを手動で編集します。
> 次のいずれかの条件を満たしている場合は、次の操作を実行することをお勧めします。
> - チェック後、カーネルにはVirtioドライバーに関する設定情報がないことが発見された場合。
> - カーネルをコンパイルする際に、カーネル設定画面に入ることができないか、`.config`ファイルが保存されていない場合。
> 
```
make oldconfig
make prepare
make scripts
make
make install
```
19. 次のコマンドを順次実行して、Virtioドライバーのインストール状況を確認します。
```
find /lib/modules/"$(uname -r)"/ -name "virtio.*" | grep -E "virtio.*"
grep -E "virtio.*" < /lib/modules/"$(uname -r)"/modules.builtin
```
任意のコマンドの戻り結果が`virtio_blk`、`virtio_pci.virtio_console`などのファイルリストを出力した場合、Virtioドライバーが正しくインストールされていることを示します。



