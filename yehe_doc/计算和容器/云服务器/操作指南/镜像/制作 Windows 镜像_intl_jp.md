## 概要
このドキュメントでは、Windows Server 2012 OSを例として、Windows イメージを作成する方法について説明します。別のバージョンのWindows Server OSを使用する場合は、このドキュメントを参照することもできます。

## 操作手順

### 準備作業

システムディスクイメージを作成してエクスポートする前に、以下の操作を行う必要があります​。
>?データディスクイメージをエクスポートする場合は、この手順をスキップしてください。
>

#### OSのパーティションと起動方法の確認

1. OS画面で、<img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"> をクリックして、Windows PowerShellウインドウを開きます。
2. Windows PowerShellウィンドウで、**diskmgmt.msc**を入力し、**Enter**キーを押して「ディスクの管理」ウィンドウを開きます。
3. チェックするディスクを右クリックし、 【プロパティ】をクリックして、【ボリューム】タブを選択することにより、ディスクのパーティション形式を確認できます。
2. ディスクのパーティション形式がGPTパーティションかどうかを確認します。
 - GPTパーティションである場合、マイグレーションサービスは現在GPTパーティションをサポートしていないため、[チケットを提出](https://console.intl.cloud.tencent.com/workorder
)してフィードバックしてください。
 - そうでない場合は、次の手順に進みます。
3. 管理者としてコマンドプロンプト（CMD）を開き、次のコマンドを実行して、現在のOSがEFIモードで起動するかどうかを確認します。
```
bcdedit /enum {current}
```
次のような結果が返されます。
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
 - `path`パラメータに「efi」が含まれている場合、現在のOSがEFIモードで起動することを示すため、[チケットを提出](https://console.intl.cloud.tencent.com/workorder
)してフィードバックしてください。
 - `path` パラメータに「efi」が含まれていない場合、次の手順に進みます。

#### ソフトウエアのアンインストール

競合を引き起こす可能性があるドライバーとソフトウェア（VMware tools、Xen tools、Virtualbox GuestAdditions、および基盤となるドライバーを搭載する一部のソフトウェアを含む）をアンインストールします。

#### cloud-base のインストール

インストールの詳細については、 [cloud-baseのインストール](https://intl.cloud.tencent.com/document/product/213/32364)ドキュメントをご参照ください。

#### Virtioドライバーの確認またはインストール

1. 【コントロールパネル】>【プログラムと機能】を開き、検索ボックスに「Virtio」と入力します。
 - 次の図に示すように、Virtioドライバーがすでにインストールされていることを示します。
![](https://main.qcloudimg.com/raw/ff1dffb01a7f77d515061bce184e033b.png)
 - Virtioドライバーがインストールされていない場合は、手動でインストールする必要があります。
    - Microsoft Windows Server 2008 R2（Standard、Datacenter、Enterprise）、Microsoft Windows Server 2012 R2（Standard）、Microsoft Windows Server 2016（Datacenter）、Microsoft Windows Server 2019（Datacenter）の場合は、Tencent Cloudのカスタマイズ版Virtioをダウンロードしてください。ダウンロードアドレスは以下のとおりです。実際のネットワーク環境に合わせてダウンロードしてください。
      -  パブリックネットワークのダウンロードアドレス：`http://mirrors.tencent.com/install/windows/virtio_64_1.0.9.exe`
      - プライベートネットワークのダウンロードアドレス：：`http://mirrors.tencentyun.com/install/windows/virtio_64_1.0.9.exe`
    - 他のシステムバージョンについて、[Virtio for Community Edition](https://www.linux-kvm.org/page/WindowsGuestDrivers/Download_Drivers) をダウンロードしてください。

#### その他のハードウェア構成の確認

クラウドへの移行後のハードウェアの変更には、以下が含まれますが、これらに限定されません。
 - グラフィックカードが Cirrus VGAに変更されました。
 - ディスクがVirtio Disk に変更されました。
 - ENIがVirtio Nic に変更され、ローカルエリア接続がデフォルトで使用されます。

### イメージのエクスポート
実際のニーズに応じて、対応するツールを選択してイメージをエクスポートします。
<dx-tabs>
::: プラットフォームツールを使用してイメージをエクスポートする[](id:Useplatform)
VMWare vCenter ConvertまたはCitrix XenConvert などの仮想化プラトフォームのイメージエクスポートツールを使用できます。詳細について、対象プラットフォームのエクスポートツールのドキュメントをご参照ください。
>? 現在、Tencent Cloudのサービス移行は、qcow2、vhd、raw、およびvmdk形式のイメージをサポートします。
>
:::
::: disk2vhd を使用してイメージをエクスポートする[](id:Usedisk2vhd)
物理マシンのシステムをエクスポートする場合、またはプラットフォームツールを使用してイメージをエクスポートしたくない場合は、disk2vhdツールを使用してイメージをエクスポートします。
1. disk2vhdツールをインストールして実行します。
[ここをクリックしてdisk2vhdツールをダウンロードする >>](https://download.sysinternals.com/files/Disk2vhd.zip)
3. エスクポートするイメージの保存場所を選択し、コピーするボリュームをチェックして、【作成】をクリックします。次の図に示すように：
>! 
> - disk2vhdは、Windowsシステムにボリュームシャドウコピーサービス（VSS）がインストールされた後にのみ起動できます。VSS機能の詳細については、 [Volume Shadow Copy Service](https://docs.microsoft.com/zh-cn/windows/win32/vss/volume-shadow-copy-service-portal?redirectedfrom=MSDN)をご参照ください。
> - 「Use Vhdx」をチェックしないでください。システムは現在vhdx 形式のイメージをサポートしていません。
> - データの整合性を確保するために、「Use volume Shadow Copy」を選択することをお勧めします。
> 
![image](https://main.qcloudimg.com/raw/68d9c4e5e7db49c4cefdd3785ce9b68d.jpg)
:::
</dx-tabs>


### イメージ形式の変換（任意）
変換イメージ形式を参照し、`qemu-img` を使用して、イメージファイルをサポート形式に変換します。

### イメージの確認

>? 「サービスを停止せずにイメージを作成した」などの理由により、作成したイメージファイルシステムが破損している可能性があります。イメージ作成後にエラーの有無を確認することをお勧めします。
>
イメージの形式が現在のプラットフォームでサポートしている形式と一致している場合は、イメージを直接開いてファイルシステムを確認できます。例えば、Windowsプラットフォームではvhd形式のイメージを追加でき、Linuxプラットフォームではqemu-nbd を利用してqcow2 形式のイメージを開くことができ、Xenプラットフォームではvhdファイルを直接開くことができます。

このドキュメントでは、Windowsプラットフォームを例として、「ディスクの管理」中の「VHDの接続」を通じて、vhd形式のイメージを表示する方法について説明します。
1. OSインターフェースで、 <img src="https://main.qcloudimg.com/raw/3d815ac1c196b47b2eea7c3a516c3d88.png" style="margin:-4px 0px">を右クリックし、ポップアップメニューから【コンピュータの管理】を選択します。
2. 【ストレージ】>【ディスクの管理】を選択して、ディスク管理インターフェイスに入ります。
3. 画面上部にある【アクション】>【VHDの接続】を選択します。次の図に示すように：
![](https://main.qcloudimg.com/raw/90a6ce24b78ca128ade5018833011708.png)
次図のような結果が表示された場合、イメージの作成が成功したことを示します。
![](https://main.qcloudimg.com/raw/41eac48fe77d3773dcf1ac9121b251ce.png)
