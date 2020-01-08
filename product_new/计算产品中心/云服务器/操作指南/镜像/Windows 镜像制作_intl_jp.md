## ユースケース

このドキュメントでは、Windows Server 2012 OSを例として、Windows イメージの作成方法を説明します。

## 操作手順

### 準備

システムディスクのイメージをエクスポートする場合、以下の確認を行う必要があります：
> データディスクのイメージをエクスポートする場合、この操作をスキップしてください。
>
#### OS パーティションとブートローダーの確認

1. OSのインタフェースで、<img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"> をクリックして、Windows PowerShellウインドウを開きます。
2. Windows PowerShellウィンドウで** diskmgmt.msc **を入力し、** Enter **を押して「ディスクの管理」を開きます。
3. 確認したいディスクを右クリックし、 【プロパティ】をクリックして、【ボリューム】タブを選択することにより、ディスクパーティションの形式を確認します。
2. ディスクパーティション形式がGPTパーティションかどうかを確認します。
 - はい、サービスのマイグレーションはGPTパーティションをサポートしていないため、作業依頼書を提出してフィードバックしてください。
 - いいえ、次のステップへ進んでください。
5. 管理者としてCMD を開き、次のコマンドを実行して、OSがEFIモードで起動していることを確認します。
```
bcdedit /enum {current}
```
下記の戻り結果を例として説明します:
```
Windows ブートローダー
識別子             {current}
device                  partition=C:
path                    \WINDOWS\system32\winload.exe
description             Windows 10
locale                  ja-JP
inherit                 {bootloadersettings}
recoverysequence        {f9dbeba1-1935-11e8-88dd-ff37cca2625c}
displaymessageoverride  Recovery
recoveryenabled         Yes
flightsigning           Yes
allowedinmemorysettings 0x15000075
osdevice                partition=C:
systemroot              \WINDOWS
resumeobject            {1bcd0c6f-1935-11e8-8d3e-3464a915af28}
nx                      OptIn
bootmenupolicy          Standard
```
 - `path` パラメーターに efi が含まれている場合、現在のOSはEFIモードで起動することを示します。[作業依頼書を提出](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1) してフィードバックしてください。
 - `path` パラメーターにefiが含まれていない場合、次のステップへ進めます。

#### ソフトウエアのアンインストール

競合を引き起こす可能性があるドライバーとソフトウェア（VMware tools、Xen tools、Virtualbox GuestAdditions、および基盤のドライバーを付属する一部のソフトウェアを含む）をアンインストールします。

#### cloud-base のインストール

インストールの詳細については、 [cloud-baseのインストールドキュメント](https://intl.cloud.tencent.com/document/product/213/32364) をご参照ください。

####  Virtioドライバーの確認とインストール

1. 【コントロールパネル】>【プログラムと機能】を開き、検索ボックスで Virtioを検索します。
 - 検索結果が以下のようになっている場合、Virtioドライバーが既にインストールされていることを示します。
 - Virtioドライバーがインストールされていない場合は、手動でインストールする必要があります。
    - Microsoft Windows Server 2008 R2（標準版、データセンター版、エンタープライズ版)、Microsoft Windows Server 2012 R2（標準版）の場合、[Tecent Cloudカスタマイズ版 Virtio](http://windowsvirtio-10016717.file.myqcloud.com/InstallQCloud.exe?_ga=1.44298212.1367540472.1504757536) をダウンロードしてください。
    - その他のOSバージョンについて、[コミュニティバージョン](https://www.linux-kvm.org/page/WindowsGuestDrivers/Download_Drivers) をダウンロードしてください。

#### その他ハードウェア関連の構成の確認

クラウドマイグレーションした後、ハードウエアの変更は次のものが含まれていますが、これらに限定されない場合があります。
 - グラフィックカードが Cirrus VGAに変更されています。
 - ディスクがVirtio Disk に変更されています。
 - ネットワークカードがVirtio Nic に変更され、デフォルトではローカル接続になります。

### イメージのエクスポート

実際のニーズに応じて、さまざまなツールを利用してイメージをエクスポートします。
- [プラットフォームのツールを利用してイメージをエクスポートする](#Useplatform)。
- [disk2vhd を利用してイメージをエクスポートする](#Usedisk2vhd)。

<span id="Useplatform"></span>
#### プラットフォームのツールを利用してイメージのエクスポート

VMWare vCenter Convert やCitrix XenConvert などの仮想化プラトフォームのイメージエクスポートツールを利用します。詳細について、各プラットフォームのエクスポートツールのドキュメントをご参照ください。
> 現在、Tencent Cloud サービスマイグレーションでサポートされているイメージ形式は：qcow2、vhd、raw、vmdk です。
>

<span id="Usedisk2vhd"></span>
#### disk2vhd を利用してイメージのエクスポート

物理マシンのOSをエクスポートする場合、またはプラットフォームのエクスポートツールを利用したくない場合は、disk2vhdツールを利用してイメージをエクスポートします。
1. disk2vhdツールをインストールして実行する。
[ここをクリックしてdisk2vhdツールをダウンロードする >>](https://download.sysinternals.com/files/Disk2vhd.zip)
3. エスクポートするイメージの格納パスを選択し、コピーするボリュームをチェックして、【Create】をクリックします。下図に示すように：
> 
> - disk2vhd を実行するには、予めWindowsでVSS（ボリュームシャドウコピーサービス）機能をインストールする必要があります。
> -「Use Vhdx」をチェックしないでください、現在システムはvhdx 形式のイメージをサポートしていません。
> - 「Use volume Shadow Copy」をチェックし、ボリュームシャドウコピー機能を利用して、データの整合性を確保することをお勧めします。
> 
![image](https://main.qcloudimg.com/raw/68d9c4e5e7db49c4cefdd3785ce9b68d.jpg)

### イメージの確認

> サービスを停止していない時にイメージの作成を行い、またはその他の理由で作成したイメージファイルシステムが正しくない可能性があるため、イメージ作成後にエラーの有無を確認することをお勧めします。
>
イメージの形式が現在のプラットフォームでサポートしている形式と一致している場合、イメージを開いてファイルシステムを直接確認できます。例えば、Windowsプラットフォームではvhd形式のイメージを追加でき、Linuxプラットフォームではqemu-nbd を利用してqcow2 形式のイメージをオープンでき、Xenプラットフォームではvhdファイルを直接利用できます。
Linuxプラットフォームを例にします：
```
modprobe nbd
qemu-nbd -c /dev/nbd0 xxxx.qcow2
mount /dev/nbd0p1 /mnt
```
qcow2イメージの最初のパーティションがエクスポートされた時にファイルシステムが破壊された場合、mount時にエラーが報告されます。
また、イメージをアップロードする前に、CVMを起動してイメージファイルを使用できるかどうかをテストすることもできます。
