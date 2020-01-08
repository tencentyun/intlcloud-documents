[カスタマイズイメージの作成](https://intl.cloud.tencent.com/document/product/213/4942)機能を使用できる以外に、Tencent Cloudはインポート機能の使用もサポートしています。ローカルまたは他のプラットフォームにあるサーバーのシステムディスクイメージファイルをCloud Virtual Machine（CVM）のカスタマイズイメージにインポートできます。インポートした後、該当のイメージを利用して、CVMを作成することまたは既存のCVMシステムをリインストールすることもできます。

<span id="インポートの準備"></span>
## インポートの準備

事前にインポート制限を満たすイメージファイルを準備する必要があります。
- **Linux タイプのイメージ制限：**
<table>
<tr><th>イメージの属性</th><th>条件</th></tr>
<tr><td>OS</td><td><ul><li> CentOS、Ubuntu、Debian、CoreOS、openSUSE、SUSE ディストリビューションに基づくイメージ</li><li>32ビットと64ビットをサポートする</li></ul></td></tr>
<tr><td>イメージのフォーマット</td><td><ul><li> RAW、VHD、QCOW2、VMDK フォーマットをサポートする</li><li>使用<code>qemu-img info imageName | grep 'file format'</code>イメージのフォーマットを確認する</li></ul></td></tr>
<tr><td>イメージのサイズ</td><td><ul><li>イメージの実際のサイズは50G以下の場合、<code>qemu-img info imageName | grep 'disk size'</code>を利用して、イメージの実際のサイズを確認する</li><li>イメージ vsize のサイズは500G以下の場合、<code>qemu-img info imageName | grep 'virtual size'</code>を利用して、 イメージvsizeを確認する</li></ul><b>注意：</b>イメージをインポートする時のサイズはQCOW2フォーマットに変換したイメージ情報に準ずる</td></tr>
<tr><td>ネットワーク</td><td><ul><li>Tencent Cloudはデフォルトでインスタンスに<code>eth0</code> ネットワークインターフェースを提供する</li><li>Tencent Cloudは現在IPV6をサポートしない</li><li>ユーザーがインスタンス内のmetadataサービスを利用して、インスタンスのネットワーク設定を確認できる。詳細については、 <a href="https://cloud.tencent.com/document/product/213/4934">インスタンスのメタデータ</a>を参照する</li></ul></td></tr>
<tr><td>ドライバー</td><td><ul><li>イメージに仮想化プラットフォームKVMのVirtio ドライバーをインストールする必要あり、詳細情報は <a href="https://intl.cloud.tencent.com/document/product/213/9929">Linux にイメージをインポートしてVirtio ドライバーをチェックする</a>ことを参照してください</li><li>イメージにcloudinitをインストールすることを推奨する、詳細情報は<a href="https://intl.cloud.tencent.com/document/product/213/12587">Linux にイメージをインポートしてcloudinitをインストールする </a>ことを参照してください</li><li>他の原因のため、イメージにcloudinitをインストールできない場合は、 <a href="https://cloud.tencent.com/document/product/213/12849">強制的にイメージをインポートする</a> 方法に基づいて、自分でインスタンスを設定してください</li></ul></td></tr>
<tr><td>カーネルの制限</td><td>イメージはネイティブカーネルであることが望ましく、修正するとCVMがインポートに失敗する可能性があります</td></tr>
</table>
- **Windows タイプのイメージ制限：**
<table>
<tr><th>イメージの属性</th><th>条件</th></tr>
<tr><td>OS</td><td><ul><li>Windows Server 2008 関連バージョン、Windows Server 2012 関連バージョン、Windows Server 2016 関連バージョン</li><li>32ビットと64ビットをサポートする</li></ul></td></tr>
<tr><td>イメージのフォーマット</td><td><ul><li> RAW、VHD、QCOW2、VMDK のイメージフォーマットをサポートする</li><li><code>qemu-img info imageName | grep 'file format'</code>を利用して、イメージのフォーマットを確認する</li></ul></td></tr>
<tr><td>ファイルシステム種類</td><td><ul><li> MBRパーティションを使用するNTFSファイルシステムのみがサポートする</li><li> GPT パーティションをサポートしない</li><li>論理ボリュームマネージャ（LVM）をサポートしない</li></ul></td></tr>
<tr><td>イメージのサイズ</td><td><ul><li>イメージの実際のサイズは50G以下の場合、<code>qemu-img info imageName | grep 'disk size'</code>を利用して、イメージの実際のサイズを確認する</li><li>イメージvsizeのサイズは500G以下の場合、<code>qemu-img info imageName | grep 'virtual size'</code>を利用して、イメージvsizeを確認する</li></ul><b>注意：</b>イメージをインポートする時のサイズはQCOW2フォーマットに変換したイメージ情報に準ずる</td></tr>
<tr><td>ネットワーク</td><td><ul><li>Tencent Cloudはデフォルトでインスタンスに<code>ローカル接続</code>ネットワークインターフェースを提供する</li><li>Tencent Cloudは現在IPV6をサポートしない</li><li>ユーザーがインスタンス内のmetadata サービスを通してインスタンスのネットワーク設定を確認できる。詳細については、 <a href="https://cloud.tencent.com/document/product/213/4934">インスタンスのメタデータ</a>を参照する</li></ul></td></tr>
<tr><td>ドライバー</td><td>イメージに仮想化プラットフォームKVMのVirtioドライバーをインストールする必要がある。WindowsシステムはデフォルトでVirtioドライバーがインストールされていないため、ユーザーが <a href="http://windowsvirtio-10016717.file.myqcloud.com/InstallQCloud.exe">Windows Virtio ドライバー</a> をインストールしてから、ローカルイメージをインポートする</td></tr>
<tr><td>その他</td><td>インポートされたWindowsシステムイメージは<a href="https://cloud.tencent.com/document/product/213/2757">Windowsのアクティベーション</a> サービス<b>を提供しない</b> </td></tr>
</table>

## インポート手順

 1. [CVMコンソール](https://console.cloud.tencent.com/cvm/)にログインします。
 2. 左側ナビゲーションバー中の【[イメージ](https://console.cloud.tencent.com/cvm/image)】をクリックします。
 3. 【カスタマイズイメージ】を選択し、【イメージのインポート】をクリックします。
 4. 操作インターフェースの要件に従って、まず [COSをアクティブ](https://console.cloud.tencent.com/cos4/index)し、 [ bucket バケットを作成](/doc/product/436/6232)して 、イメージファイルを bucketにアップロードしてから、 [イメージファイルのURLを取得](/doc/product/436/6260)します。
 5.【次へ】をクリックします。
 6. 実際の状況に応じて、表に記入し、【インポート開始】をクリックします。
 > COSファイルのURLが正確であることを確認してください。
 >
インポートの成功・失敗は、 [内部メッセージ](https://console.cloud.tencent.com/message) の形式で通知されます。

## インポート失敗

コンソールを利用してイメージをインポートした後、いくつかの原因によりタスクが失敗する可能性があります。タスクが失敗した場合、以下の内容に基づいてトラブルシューティングを行います。

### 注意事項

このドキュメントによって、失敗の原因をトラブルシューティングする前に、 [内部メッセージの管理画面](https://console.cloud.tencent.com/messageCenter/messageConfig) のメッセージサブスクライバー欄で製品サービスに関連する通知をサブスクライバーすることを確保します。これにより、内部メッセージ、SMS、メールを利用して失敗の理由を確実に受信することができます。
> メッセージセンターで製品サービス関連の情報をサブスクライバーしていない場合、インポート成功/失敗の内部メッセージを受信できません。

### 失敗原因のトラブルシューティング

詳細なエラーメッセージと説明は [エラーコード]](#errorcode)をご参照ください。

#### InvalidUrl：COS リンク無効

InvalidUrl エラーが発生し、エラーメッセージ：イメージをインポートする画面に間違い COSリンクを記入し、考えられる理由は次のとおりです。
* 入力したリンクは[Tencent Cloud COS](https://console.cloud.tencent.com/cos4/index) のイメージリンクではありません。
* COS ファイルのアクセス権限はプライベートリードであり、署名が無効になりました。
> 署名付きのCOSファイルは一回しかアクセスできません。
>
* 他のリージョンのCOSリンクを記入しました。
> インポートイメージサービスはプライベートネットワークを通してローカルドメインのCOSサーバーにアクセスします。
>
* ユーザーのイメージファイルが削除されました。
COS リンクが無効であるエラーを受信した後、上記の原因によってトラブルシューティングします。

#### InvalidFormatSize：フォーマットまたはサイズが基準を満たさない

InvalidFormatSize エラーが発生し、エラーメッセージ：インポートしたイメージのフォーマットまたはサイズは、Tencent Cloudのイメージインポート機能の制限を満たしていない、制限は以下の通り：
* イメージをインポートする場合、`qcow2`、`vhd`、`vmdk`、`raw` の4つフォーマットのイメージファイルをサポートします。
* イメージをインポートする場合、実際のファイルサイズは50GB（qcow2 フォーマットに変換したイメージファイルに準じる）を超えてはいけません。
* イメージをインポートするシステムディスクのサイズは500GBを超えてはいけません。

フォーマットとサイズが条件を満たさないエラーメッセージを受信した時：
- [Linux イメージの作成 ](https://intl.cloud.tencent.com/document/product/213/17814)に記載しているイメージフォーマットの転換内容に基づいて、イメージファイルを適切なファイルフォーマットに変換し、イメージ内容を最適化して、サイズの制限を満たした後にイメージを再インポートします。
- [オフラインでインスタンスのマイグレーション](https://console.cloud.tencent.com/csm/importOfflineCvm) 機能も利用でき、インスタンスのマイグレーションを実行します。この機能は、最大500GBイメージファイルのマイグレーションをサポートします。

#### VirtioNotInstall： Virtio ドライバーがインストールされていない

VirtioNotInstall エラーが発生し、エラーメッセージ：インポートのイメージは Virtio ドライバーをインストールしていません。Tencent CloudがKVM仮想化テクノロジーを利用して、ユーザーがインポートしたイメージにVirtioドライバーがインストールされていることが必要です。一部のユーザーがカスタマイズしたLinux OS を除き、ほとんどのLinux OS には既にVirtioドライバーがインストールされています。Windows OS がVirtioドライバーを手動でインストールする必要があります：
* Linux イメージのインポートは、 ドキュメント[Linux OSにVirtioドライバーの確認](https://intl.cloud.tencent.com/document/product/213/9929)をご参照ください。
* Windows イメージのインポートは、 [Windows イメージの作成](https://intl.cloud.tencent.com/document/product/213/17815) を参照して、 Virtio ドライバーをインストールします。

#### CloudInitNotInstalled： cloud-init プログラムをインストールしていない

CloudInitNotInstalled エラーが発生し、エラーメッセージ：インポートのイメージは cloud-initプログラムをインストールしていません。Tencent Cloudはオープンソースプログラムcloud-initを利用してCVMの初期化を実行するため、cloud-init プログラムをインストールしないと、CVMの初期化は失敗になります。
* Linux イメージのインポートは、ドキュメント[Linux OSにcloud-initのインストール](https://intl.cloud.tencent.com/document/product/213/12587)をご参照ください。
* Windows イメージのインポートは、ドキュメント[Windows OSにcloudbase-initのインストール](https://intl.cloud.tencent.com/document/product/213/32364)をご参照ください。
* cloud-init/cloudbase-init をインストールした後、ドキュメントに基づいて構成ファイルを置き換えて、CVMを起動する時に正しいデータソースからデータを獲得できます。

#### PartitionNotPresent：パーティション情報が失われた

PartitionNotPresentエラーが発生し、エラーメッセージ：インポートしたイメージは不完全です。イメージを作成するときに、ブートパーティションが含まれているかどうかを確認してください。

#### RootPartitionNotFound：ルートパーティションが失われた

RootPartitionNotFound エラーが発生し、エラーメッセージ：インポートしたイメージにはルートパーティションを含むことが検出されていません。イメージファイルを確認してください。以前発生したエラーは以下の通り、参考してください：
* インストールパッケージファイルをアップロードしました。
* データディスクイメージをアップロードしました。
* ブートパーティションイメージをアップロードしました。
* 間違ったファイルをアップロードしました。

#### InternalError：不明なエラー

InternalErrorが発生し、エラーメッセージ：イメージのインポートサービスにはこのエラーの原因が含まれていません。カスタマサービスに問い合わせください。技術者が迅速に対応し、問題を解決します。

<a id="errorcode"></a>
## エラーコード
 
|エラーコード|エラーの原因|処理方法|
|-----|-----|-----|
|InvalidUrl|COS リンク無効| COS リンクはイメージのインポートリンクと同じかどうかを確認する |
|InvalidFormatSize|フォーマットまたはサイズは条件を満たさない| イメージは[インポートの準備](#インポートの準備)中の`イメージのフォーマット`と`イメージのサイズ`の制限を満たす必要がある |
|VirtioNotInstall| virtio ドライバーがインストールされていない| イメージにvirtioドライバーをインストール必要があり、 [インポートの準備](#インポートの準備) 中の`ドライバー`部分をご参照ください|
|PartitionNotPresent|パーティションの情報を見つからない|イメージの損傷は、誤った方法でイメージを作成した場合に引き起こされる可能性がある |
|CloudInitNotInstalled|cloud-init がインストールされていない|Linux イメージに cloud-initをインストールする必要があり、[インポートの準備](#インポートの準備) 中の`ドライバー`部分をご参照ください |
|RootPartitionNotFound|ルードパーティションが検出されていない|イメージの損傷は、誤った方法でイメージを作成した場合に引き起こされる可能性がある |
|InternalError|他のエラー|カスタマサービスにお問い合わせください |

