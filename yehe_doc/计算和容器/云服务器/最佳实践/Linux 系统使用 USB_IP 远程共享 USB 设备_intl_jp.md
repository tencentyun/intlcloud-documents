## ユースケース

[USB/IP](http://usbip.sourceforge.net/) はオープンソースプロジェクトであり、カーネルに組み込まれています。Linux環境ではUSB/IPを介してUSBデバイスをリモートで共有できます。このドキュメントでは、次の環境バージョンを例に、USB/IPを使用してUSBデバイスをリモートで共有する方法について説明します。
USB Client：CentOS 7.6 OSのCVM
USB Server：Debian OSのローカルPC

## 注意事項
USB/IPのインストール方法とカーネルモジュール名は、Linux OSのディストリビューションによって異なります。現在のLinux OSがUSB/IP機能をサポートしているかどうかを確認してください。　　


## 操作手順

### USBサーバーの設定

1. ローカルPCで次のコマンドを順に実行して、USB/IPをインストールし、関連するカーネルモジュールをロードします。
```
sudo apt-get install usbip
sudo modprobe usbip-core
sudo modprobe vhci-hcd
sudo modprobe usbip_host
```
2. USBデバイスを挿入し、次のコマンドを実行して、利用可能なUSBデバイスを確認します。
```
usbip list --local
```
たとえば、Feitian USBキーがローカルPCに挿入されると、次の結果が返されます。
```
busid 1-1.3(096e:031b)
Feitian Technologies, Inc.: unknown product(096e:031b)
```
3. busid値を記録し、以下のコマンドを順に実行して、リスニングサービスを有効にし、USB/IPポート番号を指定して、USBデバイスを共有します。
```
sudo usbipd -D [--tcp-port PORT]
sudo usbip bind -b [busid]
```
たとえば、指定されたUSB/IPポート番号が3240（つまり、USB/IPのデフォルトポート）で、busidが`1-1.3`の場合、次のコマンドを実行します。
```
sudo usbipd -D
sudo usbip bind -b 1-1.3
```
4.（オプション）次のコマンドを実行してSSHトンネルを作成し、ポートでリスニングします。
> パブリックIPのないローカルPCは、この手順を実行してください。ローカルPCにパブリックIPがある場合は、この手順をスキップしてください。
>
```
ssh -Nf -R <Specified USB/IP port>:localhost:<Specified USB/IP port> root@your_host
```
`your_host` はCVMのIPアドレスを示します。
たとえば、USB/IPのポート番号がポート3240で、CVMのIPアドレスが192.168.15.24の場合、次のコマンドを実行します。
```
ssh -Nf -R 3240:localhost:3240 root@192.168.15.24
```


### USBクライアントの設定

> 以下の手順では、パブリックIPアドレスのないローカルPCを例に説明します。ローカルPCにパブリックIPアドレスがある場合は、次の手順の`127.0.0.1`をローカルPCのパブリックIPアドレスに置き換えます。
>

1. [標準のログイン方法を使用してLinuxインスタンスにログインする（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)。
2. 次のコマンドを順に実行して、USB/IPソースをダウンロードします。
```
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
rpm -ivh http://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm
```
3. 次のコマンドを順に実行して、USB/IPをインストールします。
```
yum -y install kmod-usbip usbip-utils
modprobe usbip-core
modprobe vhci-hcd
modprobe usbip-host
```
4. 次のコマンドを実行して、CVMの利用可能なUSBデバイスを確認します。
```
usbip list --remote 127.0.0.1
```
たとえば、Feitian USBキーの情報を見つけて、次の結果が返されます。
```
Exportable USB devices
======================
-127.0.0.1 1-1.3: Feitian Technologies, Inc.: unknown product(096e:031b):/sys/devices/platform/scb/fd500000.pcie/pci0000:00/0000:00:00.0/0000:01:00.0/usb1/1-1/1-1.3:(Defined at Interface level)(00/00/00)
```
5.次のコマンドを実行して、USBデバイスをCVMにバインドします。
```
usbip attach --remote=127.0.0.1 --busid=1-1.3
```
6. 次のコマンドを実行して、現在のUSBデバイスリストをクエリーします。
```
lsusb
```
下記のような情報が返された場合は、共有が成功したことを示しています。
```
Bus 002 Device 002:ID096e:031b Feitian Technologies, Inc.
Bus 002 Device 001:ID1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 001:ID1d6b:0001 Linux Foundation 1.1 root hub
```
