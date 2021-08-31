[カスタムイメージの作成](https://intl.cloud.tencent.com/document/product/213/4942)機能を使用できる以外に、Tencent Cloudはインポート機能もサポートしています。ローカルまたは他のプラットフォームのサーバーのシステムディスクにあるイメージファイルをCloud Virtual Machine（CVM）のカスタムイメージにインポートできます。イメージをインポートした後、それを使用してCVMを作成したり、既存のCVMシステムを再インストールしたりできます。

<span id="インポートの準備"></span>
## インポートの準備

事前にインポート要件を満たすイメージファイルを準備する必要があります。
- **Linuxイメージの要件：**
<table>
<tr><th style="width:16%">イメージ属性</th><th>条件</th></tr>
<tr><td>OS</td><td><ul><li> CentOS、Ubuntu、Debian、CoreOS、openSUSE、SUSE リリースバージョンに基づくイメージ。</li><li>32ビットと64ビットの両方のOSがサポートされています。</li></ul></td></tr>
<tr><td>イメージ形式</td><td><ul><li> RAW、VHD、QCOW2、VMDK 形式をサポートします。</li><li><code>qemu-img info imageName | grep 'file format'を利用して</code>イメージ形式を確認します。</li></ul></td></tr>
<tr><td>ファイルシステムの種類</td><td>GPTパーティションはサポートされていません。</td></tr>
<tr><td>イメージのサイズ</td><td><ul><li>イメージの実際のサイズは50 GBを超えることはできません。<code>qemu-img info imageName | grep 'disk size'</code>を利用して、イメージの実際のサイズを確認します。</li><li>イメージのvsizeは500 GBを超えることはできません。<code>qemu-img info imageName | grep 'virtual size'</code>を利用して、 イメージのvsizeを確認します。</li></ul><b>注記：</b>イメージをインポートする時のサイズはQCOW2フォーマットに変換したイメージ情報に準じます。</td></tr>
<tr><td>ネットワーク</td><td><ul><li>デフォルトでは、Tencent Cloudはインスタンスに<code>eth0</code> ネットワークインターフェースを提供します。</li><li>ユーザーがインスタンスのメタデータサービスを使用して、インスタンスのネットワーク設定を確認できます。詳細については、 <a href="https://cloud.tencent.com/document/product/213/4934"> インスタンスメタデータ</a>をご参照ください。</a></li></ul></td></tr>
<tr><td>ドライバー</td><td><ul><li>イメージに仮想化プラットフォームKVMのVirtio ドライバーをインストールする必要があります。詳細について、<a href="https://intl.cloud.tencent.com/document/product/213/9929">LinuxでのVirtioドライバーの確認</a>をご参照ください。</li><li>イメージにcloudinitをインストールすることをお勧めします。詳細について <a href="https://intl.cloud.tencent.com/document/product/213/12587"> Linuxへのcloud-initのインストール </a>をご参照ください。</li><li>他の原因で、イメージにcloudinitをインストールできない場合は、<a href="https://intl.cloud.tencent.com/document/product/213/12849">イメージの強制インポート</a> を参照して、自分でインスタンスを設定してください。</li></ul></td></tr>
<tr><td>カーネルの制限</td><td>イメージにはネイティブカーネルが推奨されます。カーネルを変更すると、イメージをCVMにインポートできなくなる場合があります。</td></tr>
<tr><td>リージョン制限</td><td>現在、上海ファイナンスと深センファイナンスは、他のリージョンのCOSサービスからのイメージのインポートをサポートしていません。</td></tr>
</table>
- **Windowsイメージの要件：**
<table>
<tr><th style="width: 25%;">メトリック</th><th>説明</th></tr>
<tr><td>OS</td><td><ul><li>Windows Server 2008 関連バージョン、Windows Server 2012 関連バージョン、Windows Server 2016 関連バージョン</li><li>32ビットと64ビットの両方のOSがサポートされています。</li></ul></td></tr>
<tr><td>イメージ形式</td><td><ul><li> RAW、VHD、QCOW2、VMDK のイメージ形式をサポートします。</li><li><code>qemu-img info imageName | grep 'file format'</code>を利用して、イメージの形式を確認します。</li></ul></td></tr>
<tr><td>ファイルシステムの種類</td><td><ul><li> MBRパーティションを使用するNTFSファイルシステムのみサポートします。</li><li>GPT パーティションをサポートしません。</li><li>論理ボリュームマネージャ（LVM）をサポートしません。</li></ul></td></tr>
<tr><td>イメージのサイズ</td><td><ul><li>イメージの実際のサイズは50 GBを超えることはできません。<code>qemu-img info imageName | grep 'disk size'</code>を利用して、イメージの実際のサイズを確認します。</li><li>イメージのvsizeは500 GBを超えることはできません。<code>qemu-img info imageName | grep 'virtual size'</code>を利用して、イメージのvsizeを確認します。</li></ul><b>注記：</b>イメージをインポートする時のサイズはQCOW2フォーマットに変換したイメージ情報に準じます。</td></tr>
<tr><td>ネットワーク</td><td><ul><li>Tencent Cloudはデフォルトでインスタンスに<code>ローカルエリア接続</code>ネットワークインターフェースを提供します。</li><li>ユーザーがインスタンスのメタデータサービスを使用して、インスタンスのネットワーク設定を確認できます。詳細については、 <a href="https://cloud.tencent.com/document/product/213/4934"> インスタンスメタデータ</a>をご参照ください。</li></ul></td></tr>
<tr><td>ドライバー</td><td>イメージに仮想化プラットフォームKVMのVirtio ドライバーをインストールする必要があります。 WindowsシステムにはデフォルトでVirtioドライバーが付属していないため、ローカルイメージをエクスポートする前に、まずWindows Virtioドライバーをインストールしてください。 ネットワーク環境に基づいてダウンロードアドレスを選択します。<ul><li>インターネットダウンロードアドレス：<code>http://mirrors.tencent.com/install/windows/virtio_64_1.0.9.exe</code></li><li>プライベートネットワークダウンロードアドレス：：<code>http://mirrors.tencentyun.com/install/windows/virtio_64_1.0.9.exe</code></li></ul></td></tr>
<tr><td>リージョン制限</td><td>現在、上海ファイナンスと深センファイナンスは、他のリージョンのCOSサービスからのイメージのインポートをサポートしていません。</td></tr>
<tr><td>その他</td><td>インポートされたWindowsシステムイメージは<a href="https://intl.cloud.tencent.com/document/product/213/2757"> Windowsアクティベーション </a>サービス<b>を提供しません。</b></td></tr>
</table>

## インポート手順

 1. [CVM コンソール](https://console.cloud.tencent.com/cvm/) にログインします。
 2. 左側ナビゲーションバー中の【[イメージ](https://console.cloud.tencent.com/cvm/image)】をクリックします。
 3. 【カスタムイメージ】を選択し、【イメージのインポート】をクリックします。
 4. 操作画面の指示に従って、まず [ COSを有効にする](https://console.cloud.tencent.com/cos4/index)、 [バケットを作成](/doc/product/436/6232)して 、イメージファイルをバケットにアップロードしてから、 [イメージファイルのURLを取得](/doc/product/436/6260)します。
 5.【次へ】をクリックします。
 6. 実際の状況に応じて、表に記入し、【インポート開始】をクリックします。
 >! 入力したCOSファイルのURLが正しいことを確認してください。
 >
インポートの結果は、 [ サイト内メール](https://console.cloud.tencent.com/message)の形で通知されます。

## インポートに失敗しました

コンソールにイメージをインポートできない場合があります。インポートに失敗した場合は、以下の内容に基づいて問題のトラブルシューティングを行います。

### 注意事項

このドキュメントによって、失敗の原因をトラブルシューティングする前に、 [ サイト内メールの管理画面](https://console.cloud.tencent.com/messageCenter/messageConfig) のmessage subscriptionページで製品サービスに関連する通知をサブスクライブしていることを確保します。これにより、失敗の原因を含むサイト内メッセージ、SMS、および電子メールを確実に受信することができます。
>! メッセージセンターで製品サービス通知をサブスクライブしない場合、インポートが成功したかどうかに関するサイト内メッセージを受信できません。

### トラブルシューティング

詳細なエラーメッセージと説明については、 [エラーコード](#errorcode)をご参照ください。

#### InvalidUrl：無効なCOS URL

InvalidUrl エラーが発生し、エラーメッセージ：イメージをインポートするページに間違ったCOSリンクが記入されています、次の原因が考えられます。
* 入力したイメージリンクは[Tencent Cloud COS](https://console.cloud.tencent.com/cos4/index) のイメージリンクではありません。
* COS URLには、パブリック読み取りおよびプライベート書き込み権限がありません。
* COS ファイルのアクセス権限はプライベート読み取りであり、署名の有効期限が切れています。
>! 署名付きのCOSファイルは1回しかアクセスできません。
>
* 他のリージョンのCOSリンクが記入されました。
>! イメージインポートサービスはプライベートネットワークを介してローカルリージョンのCOSサーバーにアクセスします。　
>
* ユーザーのイメージファイルが削除されました。
* 署名されたリンクが使用されました。
COSリンク無効のエラーを受け取った後、上記の原因によってトラブルシューティングします。

#### InvalidFormatSize：形式またはサイズが条件に該当しない

InvalidFormatSize エラーが発生し、エラーメッセージ：インポートするイメージの形式またはサイズは、Tencent Cloudのイメージインポート機能の要件を満たしていない、要件は以下の通りです。
* イメージをインポートする場合、`qcow2`、`vhd`、`vmdk`、`raw` の4つの形式のイメージファイルをサポートします。
* イメージをインポートする場合、実際のファイルサイズは50GB（qcow2形式のサイズに基づく）を超えてはいけません。
* イメージをインポートするシステムディスクのサイズは500GBを超えてはなりません。

「イメージの形式またはサイズが条件を満たさない」というエラーメッセージを受信した場合、
- [Linux イメージの作成 ](https://intl.cloud.tencent.com/document/product/213/17814)に記載しているイメージ形式の変換内容に基づいて、イメージファイルを適切なファイル形式に変換し、イメージ内容を簡素化して、サイズの要件を満たしてからイメージを再インポートします。
- [オフラインでのインスタンス移行](https://intl.cloud.tencent.com/document/product/213/19233) 機能も利用でき、インスタンスを移行します。この機能は、最大500 GBのサイズのイメージファイルの移行をサポートします。

#### VirtioNotInstall： Virtio ドライバーがインストールされていない

VirtioNotInstall エラーが発生し、エラーメッセージ：インポートするイメージは Virtio ドライバーをインストールしていません。Tencent CloudがKVM仮想化テクノロジーを利用して、ユーザーがインポートしたイメージにVirtioドライバーをインストールする必要があります。一部のユーザーがカスタマイズされたLinux OS を除き、ほとんどのLinux OS には既にVirtioドライバーがインストールされています。 Windows OSでは、ユーザーはVirtioドライバーを手動でインストールする必要があります。
* Linuxイメージのインポートについては、ドキュメント[LinuxでのVirtioドライバーの確認](https://intl.cloud.tencent.com/document/product/213/9929)をご参照ください。
* Windowsイメージのインポートについては、 [Windows イメージの作成](https://intl.cloud.tencent.com/document/product/213/17815)を参照して、 Virtio ドライバーをインストールしてください。

#### CloudInitNotInstalled：  cloud-init プログラムがインストールされていない

CloudInitNotInstalled エラーが発生し、エラーメッセージ：インポートするイメージは cloud-initプログラムをインストールしていません。Tencent Cloudはオープンソースプログラムcloud-initを利用してCVMの初期化を実行するため、cloud-initプログラムがインストールされていない場合、CVMの初期化が失敗することがあります。
* Linuxイメージのインポートについては、ドキュメント[Linux OSにcloud-initのインストール](https://intl.cloud.tencent.com/document/product/213/12587)をご参照ください。
* Windowsイメージのインポートについては、ドキュメント[Windows OSにcloudbase-initのインストール](https://intl.cloud.tencent.com/document/product/213/32364)をご参照ください。
* cloud-init/cloudbase-init をインストールした後、関連ドキュメントに従って構成ファイルを置き換えて、CVMを起動する時に正しいデータソースからデータを取得できます。　

#### PartitionNotPresent：パーティション情報が失われた

PartitionNotPresentエラーが発生し、エラーメッセージ：インポートされたイメージは不完全です。この場合、イメージの作成時にブートパーティションが含まれていたかどうかを確認してください。

#### RootPartitionNotFound：ルートパーティションが失われた

RootPartitionNotFound エラーが発生し、エラーメッセージ：インポートしたイメージにはルートパーティションを含むことが検出されていません。この場合は、イメージファイルを確認してください。考えられる原因は次のとおりです。
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
|InvalidUrl|無効なCOSリンク| COS リンクはインポートされたイメージリンクと同じかどうかを確認します。 |
|InvalidFormatSize|形式またはサイズは条件を満たさない| イメージは[インポートの準備](#インポートの準備)中の`イメージの形式`と`イメージのサイズ`の要件を満たす必要があります。|
|VirtioNotInstall| virtio ドライバーがインストールされていない| イメージにvirtioドライバーをインストールする必要があり、[インポートの準備](#インポートの準備) 中の`ドライバー`部分をご参照ください。|
|PartitionNotPresent|パーティションの情報を見つからない|不適切なイメージ作成方法が原因で、イメージが破損しています。 |
|CloudInitNotInstalled|cloud-init がインストールされていない|Linux イメージに cloud-initをインストールする必要があり、[インポートの準備](#インポートの準備) 中の`ドライバー`部分をご参照ください 。|
|RootPartitionNotFound|ルードパーティションが検出されていない|不適切なイメージ作成方法が原因で、イメージが破損しています。 |
|InternalError|他のエラー|カスタマサービスにお問い合わせください |

