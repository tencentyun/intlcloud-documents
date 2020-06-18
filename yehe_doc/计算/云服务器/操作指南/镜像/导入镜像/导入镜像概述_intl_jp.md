Tencent Cloudは、[カスタムイメージの作成](https://intl.cloud.tencent.com/document/product/213/4942)機能を使用できる以外に、インポート機能もサポートしています。ローカルまたは他のプラットフォームのサーバーのシステムディスクにあるイメージファイルをCloud Virtual Machine（CVM）のカスタムイメージにインポートできます。イメージをインポートしたら、それを使用してCVMを作成したり、既存のCVMシステムを再インストールしたりできます。

<span id="インポートの準備"></span>
## インポートの準備

事前にインポート要件を満たすイメージファイルを準備する必要があります。
- **Linuxイメージの要件：**
<table>
<tr><th>イメージ属性</th><th>条件</th></tr>
<tr><td>OS</td><td><ul><li> CentOS、Ubuntu、Debian、CoreOS、openSUSEおよびSUSE </li><li>32ビットと64ビットの両方のOSがサポートされています。</li></ul></td></tr>
<tr><td>フォーマット</td><td><ul><li> RAW、VHD、QCOW2、およびVMDK</li><li><code>qemu-img info imageName | grep 'file format'</code>を利用してイメージのフォーマットを確認します</li></ul></td></tr>
<tr><td>サイズ</td><td><ul><li>イメージの実際のサイズはは50 GBを超えることはできません。<code>qemu-img info imageName | grep 'disk size'</code>を利用して、イメージの実際のサイズを確認します</li><li>イメージのvsizeは500 GBを超えることはできません。<code>qemu-img info imageName | grep 'virtual size'</code>を利用して、イメージのvsizeを確認します</li></ul><b>注記：</b>イメージをインポートする時のサイズはQCOW2フォーマットに変換したイメージ情報に準じます</td></tr>　　
<tr><td>ネットワーク</td><td><ul><li>Tencent Cloudはデフォルトでインスタンスに<code>eth0</code> ネットワークインターフェースを提供します</li><li>ユーザーがインスタンスのメタデータサービスを使用して、インスタンスのネットワーク設定を確認できます。詳細については、 <a href="https://intl.cloud.tencent.com/document/product/213/4934">インスタンスメタデータ</a>をご参照ください</a></li></ul></td></tr>
<tr><td>ドライバー</td><td><ul><li>イメージに仮想化プラットフォームKVMのVirtio ドライバーをインストールする必要があります。詳細について、<a href="https://intl.cloud.tencent.com/document/product/213/9929">LinuxでのVirtioドライバーの確認</a>をご参照ください</li><li>イメージにcloudinitをインストールすることをお勧めします、詳細について <a href="https://intl.cloud.tencent.com/document/product/213/12587">Linuxへのcloud-initのインストール </a>をご参照ください</li><li>他の原因で、イメージにcloudinitをインストールできない場合は、 <a href="https://intl.cloud.tencent.com/document/product/213/12849">強制的にイメージをインポートする</a> 方法に基づいて、自分でインスタンスを設定してください</li></ul></td></tr>
<tr><td>カーネル</td><td>イメージにはネイティブカーネルが推奨されます。カーネルを変更すると、イメージをCVMにインポートできなくなる場合があります。</td></tr>
</table>
- **Windowsイメージの要件：**
<table>
<tr><th>イメージ属性</th><th>条件</th></tr>
<tr><td>OS</td><td><ul><li>Windows Server 2008、Windows Server 2012、およびWindows Server 2016に関連するバージョン</li><li>32ビットと64ビットの両方のOSがサポートされています。</li></ul></td></tr>
<tr><td>フォーマット</td><td><ul><li> RAW、VHD、QCOW2、およびVMDK</li><li><code>qemu-img info imageName | grep 'file format'</code>を利用して、イメージフォーマットを確認します</li></ul></td></tr>
<tr><td>ファイルシステムタイプ</td><td><ul><li> MBRパーティションを使用するNTFSファイルシステムのみがサポートします</li><li> GPT パーティションをサポートしません</li><li>論理ボリュームマネージャ（LVM）をサポートしません</li></ul></td></tr>
<tr><td>サイズ</td><td><ul><li>イメージの実際のサイズは50 GBを超えることはできません。<code>qemu-img info imageName | grep 'disk size'</code>を利用して、イメージの実際のサイズを確認します</li><li>イメージのvsizeは500 GBを超えることはできません。<code>qemu-img info imageName | grep 'virtual size'</code>を利用して、イメージのvsizeを確認します</li></ul><b>注記：</b>イメージをインポートする時のサイズはQCOW2フォーマットに変換したイメージ情報に準じます</td></tr>
<tr><td>ネットワーク</td><td><ul><li>Tencent Cloudはデフォルトでインスタンスに<code>ローカルエリア接続</code>ネットワークインターフェースを提供します</li><li>ユーザーがインスタンスのメタデータサービスを使用して、インスタンスのネットワーク設定を確認できます。詳細については、 <a href="https://intl.cloud.tencent.com/document/product/213/4934">インスタンスメタデータ</a>をご参照ください</li></ul></td></tr>
<tr><td>ドライバー</td><td>イメージに仮想化プラットフォームKVMのVirtioドライバーをインストールする必要があります。WindowsシステムはデフォルトでVirtioドライバーがインストールされていないため、ユーザーが <a href="http://windowsvirtio-10016717.file.myqcloud.com/InstallQCloud.exe"> Windows用のVirtioドライバー</a> をインストールしてから、ローカルイメージをインポートできます</td></tr>
<tr><td>その他</td><td>インポートされたWindowsシステムイメージは</b> <a href="https://intl.cloud.tencent.com/document/product/213/2757">Windowsアクティベーション</a> サービスを提供しません</td></tr>
</table>

## インポート手順

 1. [CVM コンソール](https://console.cloud.tencent.com/cvm/) にログインします。
 2. 左側のナビゲーションメニュー中の【[イメージ](https://console.cloud.tencent.com/cvm/image)】をクリックします。
 3. 【カスタムイメージ】を選択し、【イメージのインポート】をクリックします。
 4. 操作画面の指示に従って、まず [COSを有効にする](https://console.cloud.tencent.com/cos4/index)、 [bucketバケットを作成](/doc/product/436/6232)して 、イメージファイルをbucketにアップロードしてから、 [イメージファイルのURLを取得](/doc/product/436/6260)します。
 5.【次のステップ】をクリックします。
 6. 実際の状況に応じてフォームに入力し、【インポート開始】をクリックします。
 > 入力したCOSファイルのURLが正しいことを確認してください。
 >
インポートの成功または失敗は、 [サイト内メール](https://console.cloud.tencent.com/message) で通知されます。

## インポートに失敗

コンソールにイメージをインポートできない場合があります。インポートが失敗した場合は、以下の内容に基づいてトラブルシューティングを行います。

### 注意事項

このドキュメントによって、失敗の原因をトラブルシューティングする前に、 [サイト内メールの管理画面](https://console.cloud.tencent.com/messageCenter/messageConfig) のmessage subscriptionページで製品サービスに関連する通知をサブスクライブしていることを確保します。これにより、失敗の原因を含むサイト内メッセージ、SMS、および電子メールを確実に受信することができます。
> メッセージセンターで製品サービス通知をサブスクライブしない場合、インポート成功/失敗のサイト内メッセージを受信できません。

### トラブルシューティング

詳細なエラーメッセージと説明は [エラーコード](#errorcode)をご参照ください。

#### InvalidUrl：無効なCOS URL

InvalidUrl エラーが発生し、エラーメッセージ：イメージをインポートするページに間違ったCOSリンクが記入されています、次の原因が考えられます。
* 入力したイメージリンクは[Tencent Cloud Object Storage](https://console.cloud.tencent.com/cos4/index) のイメージリンクではありません。
* COS ファイルのアクセス権限はプライベートな読み取りであり、署名の有効期限が切れています。
> 署名付きのCOSファイルは1回しかアクセスできません。
>
* 他のリージョンのCOSリンクが記入されました。
> 　イメージインポートサービスはプライベートネットワークを介してローカルリージョンのCOSサーバーにアクセスします。　　
>
* ユーザーのイメージファイルが削除されました。
COS URLが無効であることを示すエラーメッセージが表示されたら、上記の原因に基づいてトラブルシューティングを行います。

#### InvalidFormatSize：無効な形式またはサイズ

InvalidFormatSize エラーが発生し、エラーメッセージ：インポートされるイメージの形式またはサイズは、Tencent Cloudのイメージインポート機能の要件を満たしていない、要件は以下の通りです。
* イメージをインポートする場合、`qcow2`、`vhd`、`vmdk`、`raw` の4つの形式のイメージファイルをサポートします。
* イメージをインポートする場合、実際のファイルサイズは50GB（qcow2 形式に変換したイメージファイルに準じる）を超えてはいけません。
* イメージのインポート先のシステムディスクのサイズは500GBを超えてはいけません。

形式とサイズが条件を満たさないエラーメッセージを受信した場合、
- [Linux イメージの作成 ](https://intl.cloud.tencent.com/document/product/213/17814)に記載しているイメージ形式の変換内容に基づいて、イメージファイルを適切なファイル形式に変換し、イメージ内容を簡素化して、サイズの要件を満たしてからイメージを再インポートします。
- [オフラインのインスタンス移行](https://console.cloud.tencent.com/csm/importOfflineCvm) 機能を使用してインスタンスを移行することもできます。この機能は、最大500 GBのサイズのイメージファイルの移行をサポートします。

#### VirtioNotInstall： Virtio ドライバーがインストールされていない

VirtioNotInstall エラーが発生し、エラーメッセージ：インポートされるイメージは Virtio ドライバーをインストールしていません。Tencent CloudがKVM仮想化テクノロジーを利用して、ユーザーがインポートしたイメージにVirtioドライバーをインストールする必要があります。一部のユーザーがカスタマイズされたLinux OS を除き、ほとんどのLinux OS には既にVirtioドライバーがインストールされています。 Windows OSでは、ユーザーはVirtioドライバーを手動でインストールする必要があります。
* Linuxイメージのインポートについては、[LinuxでのVirtioドライバーの確認](https://intl.cloud.tencent.com/document/product/213/9929)をご参照ください。
* Windowsイメージのインポートについては、 [Windows イメージの作成](https://intl.cloud.tencent.com/document/product/213/17815) を参照して、 Virtio ドライバーをインストールしてください。

#### CloudInitNotInstalled： cloud-init プログラムがインストールされていない

CloudInitNotInstalled エラーが発生し、エラーメッセージ：インポートされるイメージは cloud-initプログラムをインストールしていません。Tencent Cloudはオープンソースプログラムcloud-initを利用してCVMの初期化を実行するため、cloud-initプログラムがインストールされていない場合、CVMの初期化は失敗になります。
* Linuxイメージのインポートについては、[Linux OSにcloud-initのインストール](https://intl.cloud.tencent.com/document/product/213/12587)をご参照ください。
* Windowsイメージのインポートについては、[Windows OSにcloudbase-initのインストール](https://intl.cloud.tencent.com/document/product/213/32364)をご参照ください。
* cloud-init/cloudbase-init をインストールした後、関連ドキュメントに従って構成ファイルを置き換えて、CVMが起動時に正しいデータソースからデータをプルできるようにします。

#### PartitionNotPresent：パーティション情報が失われた

PartitionNotPresentエラーが発生し、エラーメッセージ：インポートされたイメージは不完全です。この場合、イメージの作成時にブートパーティションが含まれていたかどうかを確認してください。

#### RootPartitionNotFound：ルートパーティションが失われた

RootPartitionNotFound エラーが発生し、エラーメッセージ：インポートされたイメージにはルートパーティションを検出できない。この場合は、イメージファイルを確認してください。考えられる原因は次のとおりです。
* インストールパッケージファイルがアップロードされました。
* データディスクイメージがアップロードされました。
* ブートパーティションイメージがアップロードされました。
* 間違ったファイルがアップロードされました。

#### InternalError：不明なエラー

InternalErrorが発生し、エラーメッセージ：イメージインポートサービスがこのエラーの原因を記録しません。この場合は、弊社カスタマーサービスまでご連絡ください、技術担当者が顧客の問題をできるだけ早く解決するお手伝いをします。

<a id="errorcode"></a>
## エラーコード
 
|エラーコード|エラーの原因|推奨される解決策|
|-----|-----|-----|
|InvalidUrl|無効なCOSリンク| COS リンクはインポートされたイメージリンクと同じかどうかを確認します |　
|InvalidFormatSize|形式またはサイズは要件を満たさない| イメージは[インポートの準備](#インポートの準備)中の`イメージ形式`と`イメージサイズ`の要件を満たす必要があります |
|VirtioNotInstall| virtio ドライバーがインストールされていない| イメージにvirtioドライバーをインストールする必要があり、[インポートの準備](#インポートの準備) 中の`ドライバー`部分をご参照ください|
|PartitionNotPresent|パーティションの情報を見つからない|不適切なイメージ作成方法が原因で、イメージが破損しています|
|CloudInitNotInstalled|cloud-init がインストールされていない|Linux イメージに cloud-initをインストールする必要があり、[インポートの準備](#インポートの準備) 中の`ドライバー`部分をご参照ください |
|RootPartitionNotFound|ルードパーティションが検出されていない|不適切なイメージ作成方法が原因で、イメージが破損しています |
|InternalError|他のエラー|カスタマサービスにお問い合わせください |

