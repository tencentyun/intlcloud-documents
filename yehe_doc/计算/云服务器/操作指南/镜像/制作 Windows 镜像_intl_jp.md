##  ユースケース

このドキュメントでは、Windows Server 2012 OSを例として、Windows イメージの作成方法を説明します。

## 操作手順

### 準備

システムディスクのイメージを作成してエクスポートする場合、以下の確認を行う必要があります。
> データディスクのイメージをエクスポートする場合、この操作をスキップしてください。
>
#### OS パーティションと起動方法の確認

1. OS画面で、<img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"> をクリックして、Windows PowerShellウインドウを開きます。
2. Windows PowerShellウィンドウで**diskmgmt.msc**を入力し、**Enter**キーを押して「ディスクの管理」を開きます。
3. 確認するディスクを右クリックし、【プロパティ】をクリックして、【ボリューム】タブを選択して、ディスクパーティションの形式を確認します。
2. ディスクパーティション形式がGPTであるかどうかを確認します。
 - GPTパーティションの場合、サービスの移行は現在GPTパーティションをサポートしていないため、[チケットを送信] (https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1) してフィードバックしてください。
 - GPTパーティションではい場合、次のステップに進んでください。
5. 管理者アカウントでCMDを開き、次のコマンドを実行して、OSがEFIモードで起動するかどうかを確認します。
```
bcdedit /enum {current}
```
下記の戻り結果を例に説明します。
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
 - `path` パラメータに efi が含まれている場合、現在のOSはEFIモードで起動することを示します。この場合、[チケットを送信] (https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1) してフィードバックしてください。
 - `path` パラメータにefiが含まれていない場合、次のステップに進んでください。

#### ソフトウエアのアンインストール

競合を引き起こす可能性があるドライバーとソフトウェア（VMware tools、Xen tools、Virtualbox GuestAdditions、および下位層のドライバーを搭載する一部のソフトウェアを含む）をアンインストールします。

#### cloud-base のインストール

インストールの詳細については、 [cloud-baseのインストールドキュメント](https://intl.cloud.tencent.com/document/product/213/32364) をご参照ください。

####  Virtioドライバーの確認またはインストール

1. 【コントロールパネル】>【プログラムと機能】を開き、索ボックスにVirtioと入力します。
 - 検索結果が以下のようになっている場合、Virtioドライバーがインストールされていることを示します。
![image](https://main.qcloudimg.com/raw/87808940ddd5317dd8c67a699e3dc5c0.png)
 - Virtioドライバーがインストールされていない場合は、手動でインストールする必要があります。
    - Microsoft Windows Server 2012 R2（標準版）の場合、[Tencent Cloudカスタム版 Virtio](http://windowsvirtio-10016717.file.myqcloud.com/InstallQCloud.exe?_ga=1.44298212.1367540472.1504757536)をダウンロードしてください。
    - その他のOSバージョンの場合、[コミュニティ版virtio](https://www.linux-kvm.org/page/WindowsGuestDrivers/Download_Drivers) をダウンロードしてください。

#### その他ハードウェア関連の構成の確認

クラウドマイグレーションした後、ハードウエアの変更には次のものが含まれていますが、これらに限られない場合があります。
 - グラフィックカードが Cirrus VGAに変更されました。
 - ディスクがVirtio Disk に変更されました。
 - ENIがVirtio Nic に変更され、デフォルトではローカルエリア接続になります。

### イメージのエクスポート

実際の要件に応じて、対応するツールを選択してイメージをエクスポートします。
- [プラットフォームツールを利用してイメージをエクスポートする](#Useplatform)。
- [disk2vhd を利用してイメージをエクスポートする](#Usedisk2vhd)。

<span id="Useplatform"></span>
#### プラットフォームツールを利用してイメージをエクスポートする

VMWare vCenter ConvertまたはCitrix XenConvert などの仮想化プラトフォームのイメージエクスポートツールを利用します。詳細について、対象プラットフォームのエクスポートツールのドキュメントをご参照ください。
> 現在、Tencent Cloud サービスマイグレーションでサポートされているイメージ形式に、qcow2、vhd、raw、vmdkがあります。
>

<span id="Usedisk2vhd"></span>
#### disk2vhd を利用してイメージをエクスポートする

物理マシンのシステムをエクスポートする場合、またはプラットフォームのエクスポートツールを利用しない場合は、disk2vhdツールを利用してイメージをエクスポートします。
1. disk2vhdツールをインストールして実行します。
[ここをクリックしてdisk2vhdツールをダウンロードする >>](https://download.sysinternals.com/files/Disk2vhd.zip)
3.エクスポートするイメージのストレージパスを選択し、コピーするボリュームをチェックして、【Create】をクリックします。次の図に示すように：
> 
> - Disk2vhdは、Windowsシステムにボリュームシャドウコピーサービス（VSS）がインストールされた後にのみ起動できます。 VSS機能の詳細については、[ボリュームシャドウコピーサービス](https://docs.microsoft.com/en-us/windows/win32/vss/volume-shadow-copy-service-portal?redirectedfrom=MSDN)をご参照ください。
> -「Use Vhdx」をチェックしないでください、現在システムは、vhdx 形式のイメージをサポートしていません。
> - 「Use volume Shadow Copy」をチェックし、ボリュームシャドウコピー機能を利用することをお勧めし、データの整合性を確保することができます。
> 
![image](https://main.qcloudimg.com/raw/68d9c4e5e7db49c4cefdd3785ce9b68d.jpg)

### イメージの確認

> サービスを停止していない時にイメージの作成を行い、またはその他の理由で作成したイメージファイルシステムに問題が発生する可能性があるため、イメージ作成後にエラーがないかどうかを確認することをお勧めします。
>
現在のプラットフォームでイメージ形式がサポートされている場合は、イメージを開いてファイルシステムを直接確認できます。例えば、Windowsプラットフォームではvhd形式のイメージを追加でき、Linuxプラットフォームではqemu-nbd を利用してqcow2 形式のイメージをオープンでき、Xenプラットフォームではvhdファイルを直接利用できます。　　
Linuxプラットフォームを例にします。
```
modprobe nbd
qemu-nbd -c /dev/nbd0 xxxx.qcow2
mount /dev/nbd0p1 /mnt
```
qcow2イメージの最初のパーティションがエクスポートされた時にファイルシステムが破壊された場合、mountコマンドを実行するとエラーが発生します。
また、イメージをアップロードする前に、CVMを起動してイメージファイルを使用できるかどうかをテストすることもできます。
