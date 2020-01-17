CVMシステムカーネルは、Tencent Cloudで正常に実行するために、virtioドライバー（ブロックデバイスドライバー `virtio_blk` とENIドライバー`virtio_net`を含む）をサポートする必要があります。カーネルにコンパイルされていない`virtio_blk`ドライバーに対し、`initramfs(或はinitrd)`ファイルに含まれないと、CVMが正常に機能しません。このドキュメントは、イメージをインポートする前に、イメージ内のvirtioドライバーのサポートを確認及び修正する方法について説明します。

## カーネルはvirtioドライバー検査をサポートする
`Centos7`を例として、現在のカーネルが `virtio`ドライバーをサポートしているかについての確定方法を説明します。

（1）現在のカーネルが `virtio`ドライバーをサポートしているかを確認する
```
grep -i virtio /boot/config-$(uname -r)
```
下図に示すように：現在のカーネルには`virtio_blk`と`virtio_net`ドライバーが含まれて、モジュール形式でコンパイルされています（`CONFIG_VIRTIO_BLK=m`、カーネルモジュールにコンパイルされていることを示し、yだとカーネルにコンパイルされていることを示す）。このステップで`virtio_net`或は`virtio_blk`のドライバー情報が見つからない場合、このイメージはTencent Cloudにインポートすることを*サポートしません*。
![](https://mc.qcloudimg.com/static/img/4f4c1b835ccc8a344c20fdf34183b48f/image.png)

カーネルが`virtio`ドライバー（`virtio_blk`と`virtio_net`両方サポート）をサポートし、`virtio_blk`ドライバーがカーネルにコンパイルされている場合（つまり、`CONFIG_VIRTIO_BLK=y`）、このカーネルはインポートをサポートします。その後の確認は必要がありません、`virtio_blk`ドライバーがカーネルモジュールにコンパイルされている場合（つまり`CONFIG_VIRTIO_BLK=m`）、その後の確認手順を続けて、` virtio_blk`ドライバーが正確に`initramfs（或はinitrd）`ファイルに含まれていることを確認します。

（2）`initramfs`に`virtio_blk`ドライバーが含まれているかどうかを確認する
```
lsinitrd /boot/initramfs-$(uname -r).img | grep virtio
```
下図に示すように、`initramfs`に`virtio_blk`ドライバー及び（`virtio_blk`ドライバーに）依存する`virtio.ko`、`virtio_pci.ko`、`virtio_ring.ko`が含まれているため、`initramfs`がドライバーを正常とみなします。また、このイメージをインポートできます。
![](https://mc.qcloudimg.com/static/img/4bac7c12a585eea3cdbd4b27c6a8caa6/image.png)

（3）`initramfs`の中で`virtio`の関連情報が見つからない場合、`initramfs`ファイルを再作成する必要があります。

1) CentOS 7 の操作方法
```
cp /boot/initramfs-$(uname -r).img /boot/initramfs-$(uname -r).img.bak
mkinitrd -f --with=virtio_blk --with=virtio_pci /boot/initramfs-$(uname -r).img $(uname -r)
```
![](https://mc.qcloudimg.com/static/img/559c71e11c197ea620a035b0ddd443cf/image.png)

2) Redhat5/Centos5 の操作方法
a. 以下のように、ドライバー情報がinitrdファイルに含まれているかを確定する
```
mkdir -p /tmp/initrd && cd /tmp/initrd
zcat /boot/initrd-$(uname -r).img | cpio -idmv
find . -name "virtio*"
```

b. `initrd`ファイルを再作成する必要がある場合、次のコマンドを実行する
```
cp /boot/initrd-$(uname -r).img /boot/initrd-$(uname -r).img.bak
mkinitrd -f --with=virtio_blk --with=virtio_pci /boot/initrd-$(uname -r).img $(uname -r)
```

3) Debian/Ubuntu の操作方法
a. virtioドライブの状況を確認する
```
lsinitramfs /boot/initrd.img-$(uname -r) | grep virtio
```
b. initramfsに含まれていない場合、次の手順を実行して修正する
```
echo -e "virtio_pci\nvirtio_blk" >> /etc/initramfs-tools/modules
update-initramfs  -u
```
