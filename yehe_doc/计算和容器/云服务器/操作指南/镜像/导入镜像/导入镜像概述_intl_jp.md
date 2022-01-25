[カスタムイメージの作成](https://intl.cloud.tencent.com/document/product/213/4942)機能を使用できる以外に、Tencent Cloudはインポート機能もサポートしています。ローカルまたは他のプラットフォームのサーバーのシステムディスクにあるイメージファイルをCloud Virtual Machine（CVM）のカスタムイメージにインポートできます。イメージをインポートした後、それを使用してCVMを作成したり、既存のCVMシステムを再インストールしたりできます。


## インポートの準備[](id:importPreparation)

事前にインポート要件を満たすイメージファイルを準備する必要があります。

<dx-tabs>
::: Linuxシステムタイプのイメージ制限
<table>
<tr><th style="width:17%">イメージ属性</th><th>条件</th></tr>
<tr><td>OS</td><td><ul><li> CentOS、Ubuntu、Debian、CoreOS、openSUSE、SUSE リリースバージョンに基づくイメージ。</li><li>32ビットと64ビットの両方のOSがサポートされています。</li></ul></td></tr>
<tr><td>イメージ形式</td><td><ul><li> RAW、VHD、QCOW2、VMDK 形式をサポートします。</li><li><code>qemu-img info imageName | grep 'file format'を利用して</code>イメージ形式を確認します。</li></ul></td></tr>
<tr><td>ファイルシステムの種類</td><td>GPTパーティションはサポートされていません。</td></tr>
<tr><td>イメージのサイズ</td><td><ul><li>イメージの実際のサイズはは50 GBを超えることはできません。<code>qemu-img info imageName | grep 'disk size'</code>を利用して、イメージの実際のサイズを確認します。</li><li>イメージのvsizeは500 GBを超えることはできません。<code>qemu-img info imageName | grep 'virtual size'</code>を利用して、 イメージのvsizeを確認します。</li></ul><b>注記：</b>イメージをインポートする時のサイズはQCOW2フォーマットに変換したイメージ情報に準じます。</td></tr>
<tr><td>ネットワーク</td><td><ul><li>デフォルトでは、Tencent Cloudはインスタンスに<code>eth0</code> ネットワークインターフェースを提供します。</li><li>ユーザーがインスタンスのメタデータサービスを使用して、インスタンスのネットワーク設定を確認できます。詳細については、 <a href="https://cloud.tencent.com/document/product/213/4934"> インスタンスメタデータ</a>をご参照ください。</a></li></ul></td></tr>
<tr><td>ドライバー</td><td><ul><li>イメージに仮想化プラットフォームKVMのVirtio ドライバーをインストールする必要があります。詳細について、<a href="https://intl.cloud.tencent.com/document/product/213/9929">LinuxでのVirtioドライバーの確認</a>をご参照ください。</li><li>イメージにcloudinitをインストールすることをお勧めします。詳細について <a href="https://intl.cloud.tencent.com/document/product/213/12587"> Linuxへのcloud-initのインストール </a>をご参照ください。</li><li>他の原因で、イメージにcloudinitをインストールできない場合は、<a href="https://intl.cloud.tencent.com/document/product/213/12849">イメージの強制インポート</a> を参照して、自分でインスタンスを設定してください。</li></ul></td></tr>
<tr><td>カーネルの制限</td><td>イメージにはネイティブカーネルが推奨されます。カーネルを変更すると、イメージをCVMにインポートできなくなる場合があります。</td></tr>
<tr><td>リージョン制限</td><td>現在、上海金融区、深圳金融区では、その他リージョンのCloud Object Storage（COS）サービスからのイメージのインポートをサポートしていません。</td></tr>
</table>

:::
::: Windowsシステムタイプのイメージ制限
<table>
<tr><th style="width:16%">イメージ属性</th><th>条件</th></tr>
<tr><td>OS</td><td><ul><li>Windows Server 2008 関連バージョン、Windows Server 2012 関連バージョン、Windows Server 2016 関連バージョン</li><li>32ビットと64ビットの両方のOSがサポートされています。</li></ul></td></tr>
<tr><td>イメージ形式</td><td><ul><li> RAW、VHD、QCOW2、VMDK 形式をサポートします。</li><li><code>qemu-img info imageName | grep 'file format'を利用して</code>イメージ形式を確認します。</li></ul></td></tr>
<tr><td>ファイルシステムの種類</td><td><ul><li> MBRパーティションを使用するNTFSファイルシステムのみサポートします。</li><li>GPT パーティションをサポートしません。</li><li>論理ボリュームマネージャ（LVM）をサポートしません。</li></ul></td></tr>
<tr><td>イメージのサイズ</td><td><ul><li>イメージの実際のサイズは50 GBを超えることはできません。<code>qemu-img info imageName | grep 'disk size'</code>を利用して、イメージの実際のサイズを確認します。</li><li>イメージのvsizeは500 GBを超えることはできません。<code>qemu-img info imageName | grep 'virtual size'</code>を利用して、イメージのvsizeを確認します。</li></ul><b>注記：</b>イメージをインポートする時のサイズはQCOW2フォーマットに変換したイメージ情報に準じます。</td></tr>
<tr><td>ネットワーク</td><td><ul><li>Tencent Cloudはデフォルトでインスタンスに<code>ローカルエリア接続</code>ネットワークインターフェースを提供します。</li><li>ユーザーがインスタンスのメタデータサービスを使用して、インスタンスのネットワーク設定を確認できます。詳細については、 <a href="https://cloud.tencent.com/document/product/213/4934"> インスタンスメタデータ</a>をご参照ください。</li></ul></td></tr>
<tr><td>ドライバー</td><td>イメージにはバーチャル化プラットフォームKVMのVirtioドライバーをインストールする必要があります。WindowsシステムにはデフォルトでVirtioドライバーがインストールされていませんが、ユーザーはWindows Virtioドライバーをインストールして、ローカルイメージをエクスポートすることができます。Windows Virtioドライバーのダウンロードアドレスは次のとおりです。実際のネットワーク環境に応じてダウンロードしてください：<ul><li>パブリックネットワークダウンロードアドレス：<code>http://mirrors.tencent.com/install/windows/virtio_64_1.0.9.exe</code></li><li>プライベートネットワークダウンロードアドレス：<code>http://mirrors.tencentyun.com/install/windows/virtio_64_1.0.9.exe</code></li></ul></td></tr>
<tr><td>リージョン制限</td><td>現在、上海金融区、深圳金融区では、その他リージョンのCOSサービスからのイメージのインポートをサポートしていません。</td></tr>
<tr><td>その他</td><td>インポートされたWindowsシステムイメージは<a href="https://intl.cloud.tencent.com/document/product/213/2757"> Windowsアクティベーション </a>サービス<b>を提供しません。</b></td></tr>
</table>

:::
</dx-tabs>


## インポート手順

 1. CVMコンソールにログインし、左側ナビゲーションバーの **[イメージ](https://console.cloud.tencent.com/cvm/image)**をクリックします。
 3. **カスタムイメージ**を選択し、**インポートイメージ**をクリックします。
 4. 操作インターフェースの要件に基づき、まず [COSのアクティブ化](https://console.cloud.tencent.com/cos4/index)、次に[bucketの作成](https://intl.cloud.tencent.com/document/product/436/13309)を実行し、イメージファイルをbucketにアップロードして、[イメージファイルURLの取得](https://intl.cloud.tencent.com/document/product/436/13322)を実行します。
 5. **次のステップ**をクリックします。
 6. 実際の状況に応じて、リストを入力し、**インポート開始**をクリックします。
<dx-alert infotype="notice" title="">
入力したCOSのURLが正確であることを確認してください。
</dx-alert>
インポートの成功または失敗は、いずれも <a href="https://console.cloud.tencent.com/message">サイト内メッセージ</a>の形式で通知されます。

## インポートに失敗しました

コンソールにイメージをインポートできない場合があります。インポートに失敗した場合は、以下の内容に基づいて問題のトラブルシューティングを行います。

### 注意事項

このドキュメントによって、失敗の原因をトラブルシューティングする前に、 [ サイト内メールの管理画面](https://console.cloud.tencent.com/messageCenter/messageConfig) のmessage subscriptionページで製品サービスに関連する通知をサブスクライブしていることを確保します。これにより、失敗の原因を含むサイト内メッセージ、SMS、および電子メールを確実に受信することができます。


<dx-alert infotype="notice" title="">
メッセージセンターで製品サービス関連情報をサブスクリプションしないと、インポート成功/失敗のサイト内メッセージを受け取ることができません。
</dx-alert>



### トラブルシューティング

次の内容を参考に、対応するエラー情報のトラブルシューティングを実行することができます。具体的なエラープロンプトとエラーの説明については、 [エラーコード](#errorcode)をご参照ください。


<dx-accordion>
::: InvalidUrl：COSリンクの無効
InvalidUrl エラーが発生し、エラーメッセージ：イメージをインポートするページに間違ったCOSリンクが記入されています、次の原因が考えられます。
* 入力したイメージリンクは[Tencent Cloud COS](https://console.cloud.tencent.com/cos4/index) のイメージリンクではありません。
* COSのオブジェクトアドレスにはパブリック読み取り権限、プライベート書き込み権限がありません。
* COS ファイルのアクセス権限はプライベート読み取りであり、署名の有効期限が切れています。
<dx-alert infotype="notice" title="">
署名のあるCOSファイルのリンクには一度しかアクセスできません。
</dx-alert>
* 他のリージョンのCOSリンクが記入されました。
<dx-alert infotype="notice" title="">
イメージサービスをインポートし、プライベートネットワークを使用してこのリージョンのCOSサーバーにアクセスします。
</dx-alert>
* ユーザーのイメージファイルが削除されました。
COS URLが無効であることを示すエラーメッセージが表示された場合、上記の原因に基づいて問題のトラブルシューティングを行います。
:::
::: InvalidFormatSize：フォーマットまたはサイズの条件不適合
InvalidFormatSize エラーが発生し、エラーメッセージ：インポートするイメージの形式またはサイズは、Tencent Cloudのイメージインポート機能の要件を満たしていない、要件は以下の通りです。
* イメージのインポートは`qcow2`、`vhd`、`vmdk`、`raw` という4種類のフォーマットのイメージファイルをサポートしています。
* イメージをインポートする場合、実際のファイルサイズは50GB（qcow2形式のサイズに基づく）を超えてはいけません。
* イメージをインポートするシステムディスクのサイズは500GBを超えてはなりません。

「イメージの形式またはサイズが条件を満たさない」というエラーメッセージを受信した場合、
- [Linux イメージの作成 ](https://intl.cloud.tencent.com/document/product/213/17814)に記載しているイメージ形式の変換内容に基づいて、イメージファイルを適切なファイル形式に変換し、イメージ内容を簡素化して、サイズの要件を満たしてからイメージを再インポートします。
- [オフラインインスタンスマイグレーション](https://intl.cloud.tencent.com/document/product/213/19233)機能を利用してインスタンスをマイグレーションすることもできます。この機能は最大500GBのイメージファイルマイグレーションをサポートしています。
:::
::: VirtioNotInstall：Virtioドライバーの未インストール
VirtioNotInstall エラーが発生し、エラーメッセージ：インポートするイメージは Virtio ドライバーをインストールしていません。Tencent CloudがKVM仮想化テクノロジーを利用して、ユーザーがインポートしたイメージにVirtioドライバーをインストールする必要があります。一部のユーザーがカスタマイズされたLinux OS を除き、ほとんどのLinux OS には既にVirtioドライバーがインストールされています。 Windows OSでは、ユーザーはVirtioドライバーを手動でインストールする必要があります。
* Linuxイメージのインポートについては、ドキュメント[LinuxでのVirtioドライバーの確認](https://intl.cloud.tencent.com/document/product/213/9929)をご参照ください。
* Windowsイメージのインポートについては、 [Windows イメージの作成](https://intl.cloud.tencent.com/document/product/213/17815)を参照して、 Virtio ドライバーをインストールしてください。
:::
::: CloudInitNotInstalled：cloud-initプログラムの未インストール
CloudInitNotInstalled エラーが発生し、エラーメッセージ：インポートするイメージは cloud-initプログラムをインストールしていません。Tencent Cloudはオープンソースプログラムcloud-initを利用してCVMの初期化を実行するため、cloud-initプログラムがインストールされていない場合、CVMの初期化が失敗することがあります。
* Linuxイメージのインポートについては、ドキュメント[Linux OSにcloud-initのインストール](https://intl.cloud.tencent.com/document/product/213/12587)をご参照ください。
* Windowsイメージのインポートについては、ドキュメント[Windows OSにcloudbase-initのインストール](https://intl.cloud.tencent.com/document/product/213/32364)をご参照ください。
* cloud-init/cloudbase-init をインストールした後、関連ドキュメントに従って構成ファイルを置き換えて、CVMを起動する時に正しいデータソースからデータを取得できます。　
:::
::: PartitionNotPresent：パーティション情報の消失
PartitionNotPresentエラーが発生し、エラーメッセージ：インポートされたイメージは不完全です。この場合、イメージの作成時にブートパーティションが含まれていたかどうかを確認してください。
:::
::: RootPartitionNotFound：ルートパーティションの消失
RootPartitionNotFound エラーが発生し、エラーメッセージ：インポートしたイメージにはルートパーティションを含むことが検出されていません。この場合は、イメージファイルを確認してください。考えられる原因は次のとおりです。
* インストールパッケージファイルがアップロードされました。
* データディスクイメージがアップロードされました。
* ブートパーティションイメージがアップロードされました。
* 間違ったファイルがアップロードされました。
:::
::: InternalError：未知のエラー
InternalErrorが発生し、エラーメッセージ：イメージインポートサービスがこのエラーの原因を記録しません。この場合は、弊社カスタマーサービスまでご連絡ください、技術担当者が顧客の問題をできるだけ早く解決するお手伝いをします。
:::
</dx-accordion>



## エラーコード[](id:errorcode)
 
|エラーコード|エラーの原因|推奨される解決策|
|-----|-----|-----|
|InvalidUrl|無効なCOSリンク| COS リンクはインポートされたイメージリンクと同じかどうかを確認します。 |
|InvalidFormatSize|形式またはサイズは条件を満たさない| イメージは[インポートの準備](#インポートの準備)中の`イメージの形式`と`イメージのサイズ`の要件を満たす必要があります。|
|VirtioNotInstall| virtio ドライバーがインストールされていない| イメージにvirtioドライバーをインストールする必要があり、[インポートの準備](#インポートの準備) 中の`ドライバー`部分をご参照ください。|
|PartitionNotPresent|パーティションの情報を見つからない|不適切なイメージ作成方法が原因で、イメージが破損しています。 |
|CloudInitNotInstalled|cloud-init がインストールされていない|Linux イメージに cloud-initをインストールする必要があり、[インポートの準備](#インポートの準備) 中の`ドライバー`部分をご参照ください 。|
|RootPartitionNotFound|ルードパーティションが検出されていない|不適切なイメージ作成方法が原因で、イメージが破損しています。 |
|InternalError|他のエラー|カスタマサービスにお問い合わせください |

