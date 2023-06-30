[カスタマイズイメージの作成](https://intl.cloud.tencent.com/document/product/213/4942)機能を使用する以外に、Tencent Cloudはインポート機能もサポートしています。ローカルまたは他のプラットフォームのサーバーのシステムディスクにあるイメージファイルをCloud Virtual Machine（CVM）のカスタマイズイメージにインポートできます。イメージをインポートした後、それを使用してCVMを作成したり、既存のCVMシステムをリインストールしたりできます。


## インポートの準備[](id:importPreparation)

事前にインポート要件を満たすイメージファイルを準備してください。

<dx-tabs>
::: Linuxシステムタイプのイメージ制限
<table>
<tr><th style="width:17%">イメージ属性</th><th>条件</th></tr>
<tr><td>OS</td><td><ul><li> CentOS、CentOS Stream、Ubuntu、Debian、OpenSUSE、CoreOS、FreeBSD、AlmaLinux、Rocky Linux、Fedora、Kylin、UnionTech、TencentOSリリースバージョンに基づくイメージです。</li><li>32ビットと64ビットの両方のOSがサポートされています。</li></ul></td></tr>
<tr><td>イメージ形式</td><td><ul><li>RAW、VHD、QCOW2、VMDKのイメージ形式をサポートします。</li><li><code>qemu-img info imageName &#124; grep 'file format'を利用して</code>イメージ形式を確認します。</li></ul></td></tr>
<tr><td>ファイルシステムのタイプ</td><td>GPTパーティションはサポートされていません。</td></tr>
<tr><td>イメージのサイズ</td><td><ul><li>イメージの実際のサイズは50Gを超えることはできません。<code>qemu-img info imageName &#124; grep 'disk size'</code>を利用して、イメージの実際のサイズを確認します。</li><li>イメージのvsizeは500Gを超えることはできません。<code>qemu-img info imageName &#124; grep 'virtual size'</code>を利用して、イメージのvsizeを確認します。</li></ul><b>注記：</b>イメージをインポートする時のサイズはQCOW2形式に変換したイメージ情報に準じます。</td></tr>
<tr><td>ネットワーク</td><td><ul><li>デフォルトでは、Tencent Cloudはインスタンスに<code>eth0</code>ネットワークインターフェースを提供します。</li><li>ユーザーはインスタンスのmetadataサービスを使用して、インスタンスのネットワーク設定を確認できます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/4934">インスタンスのメタデータをご参照ください</a></li></ul></td></tr>
<tr><td>ドライバー</td><td><ul><li>イメージに仮想化プラットフォームKVMのVirtioドライバーをインストールする必要があります。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/9929">LinuxでのVirtioドライバーの確認</a>をご参照ください。</li><li>イメージにcloudinitをインストールする必要があります。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/12587">Linuxでのイメージインポートによるcloudinitのインストール</a>をご参照ください。</li><li>他の原因で、イメージにcloudinitをインストールできない場合、<a href="https://intl.cloud.tencent.com/document/product/213/12849">イメージの強制インポート</a>を参照して、自分でインスタンスを設定してください</li></ul></td></tr>
<tr><td>カーネルの制限</td><td>イメージにはネイティブカーネルが推奨されます。カーネルを変更すると、イメージをCVMにインポートできなくなる場合があります</td></tr>
<tr><td>地域の制限</td><td>現在、上海金融区、深セン金融区では、その他の地域のCloud Object Storage（COS）サービスからのイメージのインポートをサポートしていません。</td></tr>
</table>

:::
::: Windowsシステムタイプのイメージ制限
<table>
<tr><th style="width:16%">イメージ属性</th><th>条件</th></tr>
<tr><td>OS</td><td><ul><li>Windows Server 2008関連バージョン、Windows Server 2012関連バージョン、Windows Server 2016関連バージョン、Windows Server 2019関連バージョン、Windows Server 2022関連バージョン</li><li>32ビットと64ビットの両方のOSがサポートされています</li></ul></td></tr>
<tr><td>イメージ形式</td><td><ul><li>RAW、VHD、QCOW2、VMDKのイメージ形式をサポートします。</li><li><code>qemu-img info imageName &#124; grep 'file format'を利用して</code>イメージ形式を確認します</li></ul></td></tr>
<tr><td>ファイルシステムのタイプ</td><td><ul><li>MBRパーティションを使用するNTFSファイルシステムのみをサポートします。</li><li>GPTパーティションをサポートしません。</li><li>ロジックボリュームマネージャー（LVM）をサポートしません</li></ul></td></tr>
<tr><td>イメージのサイズ</td><td><ul><li>イメージの実際のサイズは50Gを超えることはできません。<code>qemu-img info imageName &#124; grep 'disk size'</code>を利用して、イメージの実際のサイズを確認します。</li><li>イメージのvsizeは500Gを超えることはできません。<code>qemu-img info imageName &#124; grep 'virtual size'</code>を利用して、イメージのvsizeを確認します。</li></ul><b>注記：</b>イメージをインポートする時のサイズはQCOW2形式に変換したイメージ情報に準じます</td></tr>
<tr><td>ネットワーク</td><td><ul><li>デフォルトでは、Tencent Cloudはインスタンスに<code>ローカルエリア接続</code>ネットワークインターフェースを提供します。</li><li>ユーザーはインスタンスのmetadataサービスを使用して、インスタンスのネットワーク設定を確認できます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/4934">インスタンスメタデータをご参照ください</a></li></ul></td></tr>
<tr><td>ドライバー</td><td>イメージにはバーチャル化プラットフォームKVMのVirtioドライバーをインストールする必要があります。WindowsシステムにはデフォルトでVirtioドライバーがインストールされていませんが、ユーザーはWindows Virtioドライバーをインストールして、ローカルイメージをエクスポートすることができます。Windows Virtioドライバーのダウンロードアドレスは次のとおりです。実際のネットワーク環境に応じてダウンロードしてください。<ul><li>パブリックネットワークダウンロードアドレス：<code>http://mirrors.tencent.com/install/windows/virtio_64_1.0.9.exe</code></li><li>プライベートネットワークダウンロードアドレス：<code>http://mirrors.tencentyun.com/install/windows/virtio_64_1.0.9.exe</code></li></ul></td></tr>
<tr><td>地域の制限</td><td>現在、上海金融区、深セン金融区では、その他の地域のCOSサービスからのイメージのインポートをサポートしていません。</td></tr>
<tr><td>その他</td><td>インポートされたWindowsシステムイメージ<b>は、</b> <a href="https://intl.cloud.tencent.com/document/product/213/2757">Windowsアクティベーション</a>サービスを提供しません</td></tr>
</table>

:::
</dx-tabs>


## インポート手順

 1. [CVM](https://console.cloud.tencent.com/cvm/instance/index?rid=19)コンソールにログインし、左側ナビゲーションバーの**[イメージ](https://console.cloud.tencent.com/cvm/image)**をクリックします。
 3. **カスタマイズイメージ**を選択し、**イメージのインポート**をクリックします。
 4. 操作インターフェースの要件に基づき、まず[COSのアクティブ化](https://console.cloud.tencent.com/cos4/index)、次に[bucketの作成](https://intl.cloud.tencent.com/document/product/436/13309)を実行し、イメージファイルをbucketに[オブジェクトのアップロード](https://www.tencentcloud.com/document/product/436/13321)して、[イメージファイルURLの取得](https://intl.cloud.tencent.com/document/product/436/13322)を実行します。
 5. **次のステップへ**をクリックします。
 6. 実際の状況に応じて、リストを記入し、**インポート開始**をクリックします。
<dx-alert infotype="notice" title="">
入力したCOSのURLが正確であることを確認してください。
</dx-alert>
インポートの成功または失敗は、いずれも<a href="https://console.cloud.tencent.com/message">内部メッセージ</a>の形式で通知されます。

## インポートに失敗する

コンソールでイメージのインポート操作を実行した後、何らかの理由でタスクが失敗する場合があります。タスクが失敗した場合は、以下の内容に基づいて問題のトラブルシューティングを行います。

### 注意事項

このドキュメントによって、失敗の原因をトラブルシューティングする前に、[内部メッセージの管理ページ](https://console.cloud.tencent.com/messageCenter/messageConfig)のメッセージサブスクリプションバーで製品サービスに関連する通知をサブスクリプションしていることを確保します。これにより、失敗の原因を含む内部メッセージ、SMS、および電子メールを確実に受信することができます。


<dx-alert infotype="notice" title="">
メッセージセンターで製品サービスに関連する情報をサブスクリプションしないと、インポートに成功/失敗する内部メッセージを受信ことができません。
</dx-alert>



### トラブルシューティング

次の内容を参考に、対応するエラー情報のトラブルシューティングを実行することができます。具体的なエラープロンプトとエラーの説明については、[エラーコード](#errorcode)をご参照ください。


<dx-accordion>
::: InvalidUrl：COSリンクの無効
InvalidUrlエラーが発生します。エラーメッセージ：イメージのインポートページに間違ったCOSリンクが記入されています。次の原因が考えられます：
* 入力したイメージリンクは[Tencent Cloud COS](https://console.cloud.tencent.com/cos4/index)のイメージリンクではありません。
* COSのオブジェクトアドレスにはパブリック読み取り権限、プライベート書き込み権限がありません。
* COSファイルのアクセス権限はプライベート読み取りですが、署名の有効期限が切れています。
<dx-alert infotype="notice" title="">
署名のあるCOSファイルのリンクには一度しかアクセスできません。
</dx-alert>
* 海外地域でイメージをインポートする場合、別の地域からのCOSリンクが使用されます。
<dx-alert infotype="notice" title="">
現在、海外地域からインポートされたイメージサービスは、同一地域のCOSサーバーのみをサポートします。つまり、同一地域のCOSリンクを使用してインポートしてください。
</dx-alert>
* ユーザーのイメージファイルが削除されました。
COSリンクが無効であるというエラーメッセージが表示された場合、上記の原因に基づいて問題のトラブルシューティングを行います。
:::
::: InvalidFormatSize：形式またはサイズの条件は不適合である
InvalidFormatSizeエラーが発生します。エラーメッセージ：事前にインポートされるイメージの形式またはサイズは、Tencent Cloudのイメージインポート機能の制限を満たしません。制限は以下の通りです：
* イメージのインポートは`qcow2`、`vhd`、`vmdk`、`raw`という4種類の形式のイメージファイルをサポートしています。
* イメージをインポートするファイルの実際のサイズが50GB（qcow2形式に変換したイメージファイルに基づく）を超えることはできません。
* イメージをインポートするシステムディスクのサイズが500GBを超えることはできません。

イメージの形式またはサイズの条件が不適合であるというエラーメッセージを受信した場合：
- [Linuxイメージの作成 ](https://intl.cloud.tencent.com/document/product/213/17814)に記載しているイメージ形式の変換内容に基づいて、イメージファイルを適切なファイル形式に変換し、イメージ内容を簡素化して、サイズの制限を満たしてからイメージを再インポートします。
- [オフラインインスタンス移行](https://intl.cloud.tencent.com/document/product/213/19233)機能を利用してインスタンスを移行することもできます。この機能は最大500GBのイメージファイル移行をサポートしています。
:::
::: VirtioNotInstall：Virtioドライバーの未インストール
VirtioNotInstallエラーが発生します。エラーメッセージ：事前にインポートされたイメージにはVirtioドライバーがインストールされていません。Tencent CloudがKVM仮想化テクノロジーを利用して、ユーザーがインポートしたイメージにVirtioドライバーがインストールされている必要があります。一部のユーザーがカスタマイズされたLinux OSを除き、ほとんどのLinux OSには既にVirtioドライバーがインストールされています。Windows OSでは、ユーザーはVirtioドライバーを手動でインストールしてください：
* Linuxイメージのインポートについては、ドキュメント[Linux OSでのVirtioドライバーの確認](https://intl.cloud.tencent.com/document/product/213/9929)をご参照ください。
* Windowsイメージのインポートについては、ドキュメント[Windowsイメージの作成](https://intl.cloud.tencent.com/document/product/213/17815)を参照して、Virtioドライバーをインストールしてください。
:::
::: CloudInitNotInstalled：cloud-initプログラムの未インストール
CloudInitNotInstalledエラーが発生します。エラーメッセージ：事前にインポートされたイメージにcloud-initプログラムがインストールされていません。Tencent Cloudはオープンソースプログラムcloud-initを利用してCVMの初期化を実行するため、cloud-initプログラムがインストールされていない場合、CVMの初期化に失敗することがあります。
* Linuxイメージのインポートについては、ドキュメント[Linux OSへのcloud-initのインストール](https://intl.cloud.tencent.com/document/product/213/12587)をご参照ください。
* Windowsイメージのインポートについては、ドキュメント[Windows OSへのcloudbase-initのインストール](https://intl.cloud.tencent.com/document/product/213/32364)をご参照ください。
* cloud-init/cloudbase-initをインストールした後、関連ドキュメントに従って構成ファイルを置き換えて、CVMを起動する時に正しいデータソースからデータを取得できます。
:::
::: PartitionNotPresent：パーティション情報の損失
PartitionNotPresentエラーが発生します。エラーメッセージ：インポートされたイメージは不完全です。この場合は、イメージの作成時にブートパーティションが含まれているかどうかを確認してください。
:::
::: RootPartitionNotFound：ルートパーティションの損失
RootPartitionNotFoundエラーが発生します。エラーメッセージ：インポートしたイメージにはルートパーティションを含むことが検出されていません。この場合は、イメージファイルを確認してください。考えられる原因は次のとおりです：
* インストールパッケージファイルがアップロードされました。
* データディスクイメージがアップロードされました。
* ブートパーティションイメージがアップロードされました。
* 間違ったファイルがアップロードされました。
:::
::: InternalError：未知のエラー
InternalErrorが発生します。エラーメッセージ：イメージインポートサービスにはエラーの原因が記録されていません。この場合は、弊社カスタマーサービスまでご連絡ください。技術担当者が顧客の問題をできるだけ早く解決するお手伝いをします。
:::
</dx-accordion>



## エラーコード[](id:errorcode)
 
|エラーコード|エラーの原因|推奨される解決策|
|-----|-----|-----|
|InvalidUrl|無効なCOSリンク|COSリンクはインポートされたイメージリンクと同じであるかどうかを確認します。|
|InvalidFormatSize|形式またはサイズの条件は不適合です|イメージは[インポートの準備](https://www.tencentcloud.com/document/product/213/4945#.E5.AF.BC.E5.85.A5.E5.87.86.E5.A4.87.3Ca-id.3D.22importpreparation.22.3E.3C.2Fa.3E)中の`イメージの形式`と`イメージのサイズ`の制限を満たす必要があります。|
|VirtioNotInstall|virtioドライバーがインストールされていません|イメージにvirtioドライバーをインストールする必要があります。[インポートの準備](https://www.tencentcloud.com/document/product/213/4945#.E5.AF.BC.E5.85.A5.E5.87.86.E5.A4.87.3Ca-id.3D.22importpreparation.22.3E.3C.2Fa.3E)中のドライバー`部分をご参照ください。|
|PartitionNotPresent|パーティションの情報を見つかりません|イメージの作成方法が間違っているため、イメージが破損する可能性があります|
|CloudInitNotInstalled|cloud-initがインストールされていません|Linuxイメージにcloud-initをインストールする必要があります。[インポートの準備](https://www.tencentcloud.com/document/product/213/4945#.E5.AF.BC.E5.85.A5.E5.87.86.E5.A4.87.3Ca-id.3D.22importpreparation.22.3E.3C.2Fa.3E)中の`ドライバー`部分をご参照ください。|
|RootPartitionNotFound|ルードパーティションが検出されていません|イメージの作成方法が間違っているため、イメージが破損する可能性があります|
|InternalError|他のエラー|カスタマサービスにお問い合わせください|

