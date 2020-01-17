## 問題の説明
新しいネットワークネームスペース（Network Namespace）を構築するコマンドを実行する時に、実行されるコマンドがフリーズし、続けることができません。Dmesg のメッセージプロンプト：“unregister_netdevice: waiting for lo to become free. Usage count = 1”

## 問題の原因
当該問題はカーネルbugです。現在、下記のカーネルバージョンには当該bugが存在しています。
- Ubuntu 16.04 x86_64のカーネルバージョンが4.4.0-91-genericです
- Ubuntu 16.04 x86_32のカーネルバージョンが4.4.0-92-genericです

## ソリューション

カーネルバージョンを4.4.0-98-genericにアップグレードすること。当該バージョンでこのbugが解決されています。

## 処理手順
1. 下記のコマンドを実行し、現在のカーネルバージョンを確認します。
```
uname -r
```
2. 下記のコマンドを実行し、 4.4.0-98-genericのアップグレードバージョンがあるかを確認します。
```
sudo apt-get update
sudo apt-cache search linux-image-4.4.0-98-generic
```
下記の情報が表示された場合は、ソースに当該バージョンがあり、アップグレードすることが可能であることを示します。
```
linux-image-4.4.0-98-generic - Linux kernel image for version 4.4.0 on 64 bit x86 SMP
```
3. 下記のコマンドを実行し、新しいバージョンのカーネルとそれに対応するHeaderパッケージをインストールします。
```
sudo apt-get install linux-image-4.4.0-98-generic linux-headers-4.4.0-98-generic
```
4. 下記のコマンドを実行し、システムを再起動します。
```
sudo reboot
```
5. 下記のコマンドを実行し、システムに入り、カーネルバージョンを確認します。
```
uname -r
```
下記のような結果が表示された場合は、バージョン更新に成功したことを示しています。
```
4.4.0-98-generic
```
