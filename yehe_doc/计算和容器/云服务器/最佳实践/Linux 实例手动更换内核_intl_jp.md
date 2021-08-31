## 概要
Bottleneck Bandwidth and Round-trip propagation time（BBR）は、2016年にGoogleによって開発されたTCPの輻輳制御アルゴリズムであり、TCPのスループットとレイテンシを大幅に改善するのに役立ちます。ただし、BBR機能を有効にするには、Linuxカーネルバージョンの4.10以降が必要です。以前のバージョンを使用している場合は、カーネルをアップグレードする必要があります。このドキュメントでは、Linuxシステムでカーネルを手動で更新してBBR機能を有効にする方法について説明します。

##　操作手順

### カーネルパッケージの更新
1.次のコマンドを実行して、現在のカーネルバージョンを確認します。
```
uname -r
```
2.次のコマンドを実行して、ソフトウェアパッケージを更新します。
```
yum update -y
```
3. 次のコマンドを実行して、ELRepoの公開鍵をインポートします。
```
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
```
4.次のコマンドを実行して、ELRepoのyumリポジトリをインストールします。
```
yum install https://www.elrepo.org/elrepo-release-7.0-4.el7.elrepo.noarch.rpm
```


### 新しいカーネルのインストール
1.次のコマンドを実行して、ELRepoリポジトリでサポートされているカーネルパッケージを確認します。
```
yum --disablerepo="*" --enablerepo="elrepo-kernel" list available
```
2. 次のコマンドを実行して、最新のメインラインの安定したカーネルをインストールします。
```
yum --enablerepo=elrepo-kernel install kernel-ml
```

### grub構成の変更
1. 次のコマンドを実行して、 `/etc/default/grub` ファイルを開きます。
```
vi /etc/default/grub
```
2. **i**を押して編集モードに切り替え、`GRUB_DEFAULT=saved`を`GRUB_DEFAULT=0`に変更します。
![](https://main.qcloudimg.com/raw/484e7a6e818dc44c2d4debb9230e0b46.png)
3. **Esc**キーを押し、**:wq**を入力して、ファイルを保存して閉じます。
4. 次のコマンドを実行して、カーネル構成を再度生成します。
```
grub2-mkconfig -o /boot/grub2/grub.cfg
```
5. 次のコマンドを実行して、サーバーを再起動します。
```
reboot
```
6. 次のコマンドを実行して、変更が成功したかどうかを確認します。
```
uname -r
```

### 不要なカーネルの削除
1. 次のコマンドを実行して、すべてのカーネルを表示します。
```
rpm -qa | grep kernel
```
2. 次のコマンドを実行して、古いカーネルを削除します。
```
yum remove kernel-old_kernel_version
```
例えば：
```
yum remove kernel-3.10.0-957.el7.x86_64
```

### BBRの有効化
1. 次のコマンドを実行して、 `/etc/sysctl.conf` ファイルを編集します。
```
vim /etc/sysctl.conf
```
2. **i**を押して編集モードに切り替え、次のように入力します。
```
net.core.default_qdisc=fq
net.ipv4.tcp_congestion_control=bbr
```
3. **Esc**キーを押し、**:wq**を入力して、ファイルを保存して閉じます。
4. 次のコマンドを実行して、`/etc/sysctl.conf`構成ファイルからカーネルパラメーター設定をロードします。
```
sysctl -p
```
5. 次のコマンドを実行して、BBRが有効になっているかどうかを確認します。
```
sysctl net.ipv4.tcp_congestion_control
# 構成が成功すると、次のように表示されます：
# net.ipv4.tcp_congestion_control = bbr
```
```
sysctl net.ipv4.tcp_available_congestion_control
# 構成が成功すると、次のように表示されます：
# net.ipv4.tcp_available_congestion_control = reno cubic bbr
```
6. 次のコマンドを実行して、カーネルモジュールがロードされているかどうかを確認します。
```
lsmod | grep bbr
```
次の情報が返された場合、BBRの有効化に成功したことを示します。
![](https://main.qcloudimg.com/raw/7d736afd8ce22f421315e149a86527e5.png)



