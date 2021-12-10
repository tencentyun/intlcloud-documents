## CentOS TOAカーネルインストール方法
### rpmパッケージのインストール方法
下記のrpmパッケージを直接ダウンロードします。
- CentOS 6 TOAパッケージ（[クリックしてダウンロード](http://toakernel-1253438722.cossh.myqcloud.com/kernel-2.6.32-220.23.1.el6.toa.x86_64.rpm)）。
- CentOS 7 TOAパッケージ（[クリックしてダウンロード](http://toakernel-1253438722.cossh.myqcloud.com/kernel-3.10.0-693.el7.centos.toa.x86_64.rpm)）。  

ダウンロードとインストールが終わったら、システムを再起動してインストールが完成します。

以下の手順に従って独自のrpmパッケージを作成することもできます。
1. kernel-2.6.32-220.23.1.el6.src.rpmをインストールします。
```
rpm -hiv kernel-2.6.32-220.23.1.el6.src.rpm
```

2. カーネルソースディレクトリを生成します。
```
rpmbuild -bp ~/rpmbuild/SPECS/kernel.spec
```

3. ソースディレクトリをコピーします。
```
cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/
cp -a linux-2.6.32-220.23.1.el6.x86_64/ linux-2.6.32-220.23.1.el6.x86_64_new
```

4. コピーしたソースディレクトリで、次のtoaパッチを適用します。
```
cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/linux-2.6.32-220.23.1.el6.x86_64_new/
patch -p1 < /usr/local/src/linux-2.6.32-220.23.1.el6.x86_64.rs/toa-2.6.32-220.23.1.el6.patch
```

5. .configを編集してSOURCEディレクトリにコピーします。
```
sed -i 's/CONFIG_IPV6=m/CONFIG_IPV6=y/g' .config
echo -e '\n# toa\nCONFIG_TOA=m' >> .config
cp .config ~/rpmbuild/SOURCES/config-x86_64-generic
```

6. 元のソースから.configを削除します。
```
cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/linux-2.6.32-220.23.1.el6.x86_64
rm -rf .config
```

7. 最終的なpatchを生成します。
```
cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/
diff -uNr linux-2.6.32-220.23.1.el6.x86_64 linux-2.6.32-220.23.1.el6.x86_64_new/ >
~/rpmbuild/SOURCES/toa.patch
```

8. kernel.specを編集します。
`vim ~/rpmbuild/SPECS/kernel.spec`
ApplyOptionPathの下に次の2行を追加します（buildidなどのカスタムカーネルパッケージ名も変更できます）。
```
Patch999999: toa.patch
ApplyOptionalPatch toa.patch
```
9. rpmパッケージを作ります。
```
rpmbuild -bb --with baseonly --without kabichk --with firmware --without debuginfo --target=x86_64 ~/rpmbuild/SPECS/kernel.spec
```

10. カーネルrpmパッケージをインストールします。
```
rpm -hiv kernel-xxxx.rpm --force
```

11. 再起動してtoaモジュールをロードすると、インストールは完了します。

### ソースのインストール方法

必要なオペレーティングシステムのバージョンがCentOS 6以上の場合は、ソースコードをダウンロードしてコンパイルすることにより、対応するインストールパッケージを入手することもできます。その手順は以下のとおりです。
1. toaパッチが適用されているソースパッケージをダウンロードします（[クリックしてダウンロード](http://kb.linuxvirtualserver.org/images/3/34/Linux-2.6.32-220.23.1.el6.x86_64.rs.src.tar.gz)）。
2. 解凍します。
3. `.config`を編集し、`CONFIG_IPV6=M`を`CONFIG_IPV6=y`に変更します。
4. カスタム説明を追加する必要がある場合は、` Makefile`を編集できます。
5. `make -jn` (nはスレッド数)。
6. `make modules_install`を実行します。
7. `make install`を実行します。
8. `/boot/grub/menu.lst`を変更して、defaultを新しくインストールしたカーネルに変更します（titleの順序は0から始まります）。
9. `Reboot`を実行して再起動すると、toaカーネルとなります。
10. `lsmod | grep toa`を実行してtoaモジュールがロードされているかどうかを確認し、ロードされていない場合は、`modprobe toa`コマンドにより開くことができます。

## Ubuntu TOAカーネルのインストール方法
以下のリンクをクリックして、カーネルパッケージとHeadersパッケージをダウンロードします。
- カーネルパッケージ（[クリックしてダウンロード](http://toakernel-1253438722.cossh.myqcloud.com/linux-image-4.4.87.toa_1.0_amd64.deb)） 
- カーネルHeadersパッケージ（[クリックしてダウンロード](http://toakernel-1253438722.cossh.myqcloud.com/linux-headers-4.4.87.toa_1.0_amd64.deb)） 

Headersパッケージはオプションであり、関連開発が必要なときにインストールします。最初にカーネルパッケージをインストールしてください。操作手順は次のとおりです。

1. 次のコマンドを実行してカーネルパッケージをインストールします。  
```
dpkg -i linux-image-4.4.87.toa_1.0_amd64.deb
```
2. インストールが完了したら、ホストを再起動してください。

3. `lsmod | grep toa`を実行して、toaモジュールがロードされているかどうかを確認し、ロードされていない場合は、`modprobe toa`により開くことができます。実行するコマンドは以下のとおりです。
```
echo “modprobe toa” >> /etc/rc.d/rc.local
```

## Debian TOAカーネルのインストール方法
以下のリンクをクリックして、カーネルパッケージとHeadersパッケージをダウンロードします。
- カーネルパッケージ（[クリックしてダウンロード](http://toakernel-1253438722.cossh.myqcloud.com/linux-image-3.16.43.toa_1.0_amd64.deb)）
- カーネルHeadersパッケージ（[クリックしてダウンロード](http://toakernel-1253438722.cossh.myqcloud.com/linux-headers-3.16.43.toa_1.0_amd64.deb)）

Headersパッケージはオプションであり、関連開発が必要なときにインストールします。最初にカーネルパッケージをインストールしてください。操作手順は次のとおりです。

1. 次のコマンドを実行してカーネルパッケージをインストールします。  
```
dpkg -i linux-image-4.4.87.toa_1.0_amd64.deb
```
2. インストールが完了したら、ホストを再起動してください。

3. `lsmod | grep toa`を実行して、toaモジュールがロードされているかどうかを確認し、ロードされていない場合は、`modprobe toa`により開くことができます。実行するコマンドは以下のとおりです。
```
echo “modprobe toa” >> /etc/rc.d/rc.local
```
