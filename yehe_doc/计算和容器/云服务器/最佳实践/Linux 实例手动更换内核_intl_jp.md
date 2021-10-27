## 概要
Bottleneck Bandwidth and Round-trip propagation time（BBR）は、Googleが2016年に開発したTCP輻輳制御アルゴリズムであり、Linuxサーバーのスループットを大きく引き上げ、TCP接続のディレイを低減させることができます。BBRの有効化には、4.10以上のバージョンのLinuxカーネルが必要となりますが、Linuxサーバーのカーネルが4.10より低い場合は、本文を参照して操作することが可能です。

ここでは、CentOS 7.5 OSのCVMを例に、Linuxシステムでカーネルを手動で変更し、BBRを有効化する方法をご説明します。

## 操作手順

### カーネルパッケージの更新
1. 次のコマンドを実行し、現在のKernelバージョンを表示します。
```
uname -r
```
2. 次のコマンドを実行し、ソフトウェアパッケージを更新します。
```
yum update -y
```
3. 次のコマンドを実行し、ELRepoの公開鍵をインポートします。
```
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
```
4. 次のコマンドを実行し、ELRepoのyumリポジトリをインストールします。
```
yum install https://www.elrepo.org/elrepo-release-7.0-4.el7.elrepo.noarch.rpm
```


### 新しいカーネルのインストール
1. 次のコマンドを実行し、ELRepoリポジトリで現在システムがサポートしているカーネルパッケージを表示します。
```
yum --disablerepo="*" --enablerepo="elrepo-kernel" list available
```
2. 次のコマンドを実行し、最新のメインライン・安定版のカーネルをインストールします。
```
yum --enablerepo=elrepo-kernel install kernel-ml
```

### grub設定の変更
1. 以下のコマンドを実行して、 `/etc/default/grub` ファイルを開きます。
```
vim /etc/default/grub
```
2. **i**を押して編集モードに切り替え、`GRUB_DEFAULT=saved`を`GRUB_DEFAULT=0`に変更します。
![](https://main.qcloudimg.com/raw/484e7a6e818dc44c2d4debb9230e0b46.png)
3. **Esc**を押し、**:wq**を入力して、ファイルを保存して戻ります。
4. 次のコマンドを実行して、Kernel設定をあらためて生成します。
```
grub2-mkconfig -o /boot/grub2/grub.cfg
```
5. 次のコマンドを実行して、マシンを再起動します。
```
reboot
```
6. 次のコマンドを実行して、変更が成功したかどうかをチェックします。
```
uname -r
```

### 余分なカーネルの削除
1. 次のコマンドを実行して、すべてのKernelを表示します。
```
rpm -qa | grep kernel
```
2. 次のコマンドを実行して、旧バージョンのカーネルを削除します。
```
yum remove kernel-old_kernel_version
```
例：
```
yum remove kernel-3.10.0-957.el7.x86_64
```

### BBRの有効化
1. 次のコマンドを実行して、`/etc/sysctl.conf`ファイルを編集します。
```
vim /etc/sysctl.conf
```
2. **i**を押して編集モードに切り替え、次の内容を追加します。
```
net.core.default_qdisc=fq
net.ipv4.tcp_congestion_control=bbr
```
3. **Esc**を押し、**:wq**を入力して、ファイルを保存して戻ります。
4. 次のコマンドを実行して、`/etc/sysctl.conf`設定ファイルからカーネルパラメータ設定をロードします。
```
sysctl -p
```
5. 次のコマンドを順次実行して、BBRの有効化が成功したかどうか検証します。
```
sysctl net.ipv4.tcp_congestion_control
# 次の内容が表示されればOKです。
# net.ipv4.tcp_congestion_control = bbr
```
```
sysctl net.ipv4.tcp_available_congestion_control
# 次の内容が表示されればOKです。
# net.ipv4.tcp_available_congestion_control = reno cubic bbr
```
6. 次のコマンドを実行して、カーネルモジュールがロードされたかどうか確認します。
```
lsmod | grep bbr
```
次の情報が返ってきた場合、有効化が成功したことを意味します。
![](https://main.qcloudimg.com/raw/7d736afd8ce22f421315e149a86527e5.png)



