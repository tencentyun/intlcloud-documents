Elastic CBS（CVMのデータディスクとして利用される）を同じアベイラビリティーゾーンの任意のCVMにマウントして利用します。各CVMは最大20個のデータディスクをマウントするのがサポートします。以下の方法でCBSをマウントできます：
- 新しいCVMを起動する時に、該当するカスタマイズイメージとデータディスクスナップショットを指定します。
自動マウントした後、パーティション、フォーマットなどのディスクの初期化処理を行う必要がなく、直接データディスクを読み書きできます。
- 別途購入したCBSは、コンソールとAPIインターフェースを経由して、手動でElastic CBSを同じアベイラビリティーゾーンの既存CVMインスタンスにマウントします。
 - 直接作成されたCBS
 手動マウントした後、ディスクをパーティションやフォーマットなどを初期化処理を行う必要があります。詳細については、 [CBSの初期化（2TB未満）](https://intl.cloud.tencent.com/document/product/362/31597)或は [CBSの初期化（2TB以上）](https://intl.cloud.tencent.com/document/product/362/31598)をご参照ください。
 - スナップショットにより作成されたCBS
  CBSの容量がスナップショットの容量と等しい場合、手動マウントした後パーティション・フォーマットなどのディスクの初期化処理を行う必要がなく、直接データディスクを読み書きできます。
	CBSの容量がスナップショットの容量より大きい場合、ファイルシステムを拡張するか、或はパーティション形式を変換する必要があります。

 > 一部のLinux CVMはElastic CBSの状況を識別できない可能性があり、まずCVMにディスクホットスワップ機能を有効にします。詳細情報については、 [ディスクホットスワップ機能を有効にする](#modprobeacpiphp)のを参照してください。

## 自動マウント
### データディスク（Windows）のマウント
Windows CVMインスタンスを起動する時に、該当するデータディスクスナップショットによって作成されたCBSを自動的にマウントする必要がある場合、指定されたカスタマイズイメージとデータディスクスナップショットは以下の要件を満たす必要があります：
- データディスクはスナップショットを作成する前に、`ntfs`或は`fat32`形式としてフォーマットされていることが**必須**です。
- カスタマイズイメージの SAN ポリシーは`onlineAll`です。
 > Tencent Cloudは現在提供しているWindows パブリックイメージがデフォルトである程度設定されていますが、カスタマイズイメージを作成する前にこの構成を確認することをお勧めします。確認する方法は以下のようになります：
![](https://main.qcloudimg.com/raw/edac7337395de380c0ec801646e0a627.png)
 
 
### データディスク（Linux）のマウント
 Linux  CVMインスタンスを起動する時に、該当するデータディスクスナップショットによって作成されたCBSを自動的にマウントする必要がある場合、指定されたカスタマイズイメージとデータディスクスナップショットは以下の要件を満たす必要があります：
- データディスクはスナップショットを作成する前に、フォーマットされていることが**必須**です。つまり、元CVMで正常にマウントされています。
- システムディスクはカスタマイズイメージを作成する前に、 `/etc/rc.local` ファイルに以下のコマンドを追加する必要があり、データディスクのマウントポイントをファイルに書き込みします。
 ```
 mkdir -p <mount-point>
 mount <device-id> <mount-point>
 ```
>
> - `<mount-point>` をファイルシステムのマウントポイントに設定する必要があります、例えば `/mydata`。
> - `<device-id>` を実際のファイルパーティションの場所に設定する必要があります。例えば、パーティションがなく、ファイルシステムがある時、 `/dev/vdb`を記入します。パーティションがあり、ファイルシステムもある時、 `/dev/vdb1`を記入します。

## 手動マウント

### コンソールを利用してCBSをマウントする
1.  [CBSコンソール](https://console.cloud.tencent.com/cvm/cbs)にログインします。
2. CBSのリスト画面で、以下の方法でCBSをマウントすることができます：
 a. 状態は**マウント待ち**となっているCBSの行で【詳細】>【マウント】をクリックします。
 b. 状態が**マウント待ち**のCBSをチェックして、CBSリストの上部にある【マウント】をクリックして、一括マウントします。
3. ポップアップボックスにターゲットCVMを選択し、【OK】をクリックします。
4. CBSリストを更新します。
 CBSの状態が【マウント済み】となっている場合、マウントは成功したことを表します。
5. CBSの状況に応じて、適当な後続処理を行い、CBSを利用可能にします。
 <table>
 <tr>
 <th>作成モード</th>
 <th>CBS容量</th>
 <th>後続処理</th>
 </tr>
 <tr>
 <td  rowspan="2">直接作成</td>
 <td>CBS容量 < 2TB</td>
 <td><a href="https://intl.cloud.tencent.com/document/product/362/31597">CBSの初期化（2TB未満）</a></td>
 </tr>
 <tr>
  <td>CBS容量 ≥ 2TB</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/362/31598">CBSの初期化（2TB以上）</a></td>
 </tr>
  <tr>
	<td  rowspan="3">スナップショットから作成する</td>
	<td>CBS容量 = スナップショット容量</td>
	<td>後続処理する必要がない、マウントした後に直接利用できます。</td>
 </tr>
 </tr>
 <tr>
 <td nowrap="nowrap">スナップショット容量 < CBS容量 ≤ 2TB<br/>或は<br/>2TB < スナップショット容量 < CBS容量</td>
<td><ul><li> Windows CVMにマウントする：<a href="https://intl.cloud.tencent.com/document/product/362/31601">パーティション及びファイルシステム（Windows）を拡張する</a></li><li> Linux CVMにマウントする：<a href="https://intl.cloud.tencent.com/document/product/362/31602">パーティション及びファイルシステム（Linux）を拡張する</a></li></ul></td>
 </tr> 
 <tr>
 <td>スナップショット容量 ≤ 2TB < CBS容量</td>
<td nowrap="nowrap"><ul><li>スナップショットで MBR パーティションを利用する場合：</li><a href="https://intl.cloud.tencent.com/document/product/362/31598">CBSの初期化（2TB以上）</a> をご参照ください。 GPT を利用して再パーティションすると、<b>この操作により元のデータを削除されます</b><li>スナップショットで GPT パーティション形式を利用する場合：<ul><li> Windows CVMにマウントする：<a href="https://intl.cloud.tencent.com/document/product/362/31601">パーティション及びファイルシステム（Windows）を拡張する</a></li><li>Linux CVMにマウントする：<a href="https://intl.cloud.tencent.com/document/product/362/31602">パーティション及びファイルシステム（Linux）を拡張する</a></li></ul></td>
 </tr> 
 </table>

### API を利用してCBSをマウントする
 AttachDisksインターフェースを利用して、スナップショットを作成します。詳細な操作については、 [CBSのマウント](https://intl.cloud.tencent.com/document/product/362/16313)をご参照ください。

<span id="modprobeacpiphp"></span>
### ディスクのホットスワップ機能を有効にする
現在提供しているすべてのイメージは、Elastic CBSのマウント/アンマウント操作をサポートしています。**CBSをアンマウントする前に `umount`（Linux）或いはオフライン（Windows）操作を実行する必要があります。そうしないと、このCVMがElastic CBSを再マウントする時に認識されない可能性があります。**
ただし、この前に以下のOSのCVMを購入し、そのCVMにElastic CBSをマウントする予定がある場合は、CVMに関連するドライバーを追加して、ホットスワップ機能を獲得することがお勧めします。
<table>
<tbody>
<tr><th>CVM OS種類</th><th>バージョン</th>
<tr><td rowspan="4">CentOS</td><td>5.11 64ビット</td>
<tr><td>5.11 32ビット</td>
<tr><td>5.8 64ビット</td>
<tr><td>5.8 32ビット</td>
<tr><td >Debian</td><td>6.0.3 32ビット</td>
<tr><td rowspan="2">Ubuntu</td><td>10.04 64ビット</td>
<tr><td>10.04 32ビット</td>
<tr><td rowspan="2">openSUSE</td><td>12.3 64ビット</td>
<tr><td>12.3 32ビット</td>
</tbody>
</table>

1.  root ユーザーとして [ Linux CVMにログインします](https://intl.cloud.tencent.com/document/product/213/5436)。
2. 以下のコマンドを実行して、ドライバーを追加します。
```
modprobe acpiphp
```
> CVMをシャットダウン或いは再起動した後にも `acpiphp`ドライバーモジュールをロードする必要がある場合、[ステップ3](#step3)を実行して、`acpiphp` モジュールをスタートアップする時に自動ロードに設定することをお勧めします。
<span id="step3"></span>
3. （オプション）異なるOSに応じて、該当する操作方法を選択し、 `acpiphp` モジュールをスタートアップする時に自動ロードに設定します：
 - **CentOS 5 シリーズ**
 a. 以下のコマンドを実行して、`acpiphp.modules`ファイルを作成して開きます。
```
vi /etc/sysconfig/modules/acpiphp.modules
```
b. ファイルに以下の内容を追加して、保存します。
```
 #!/bin/bash
 modprobe acpiphp >& /dev/null
```
c. 以下のコマンドを実行して、実行可能な権限を追加します。
```
chmod a+x /etc/sysconfig/modules/acpiphp.modules
```
 - **Debian 6 シリーズ、Ubuntu 10.04 シリーズ**
 a. 以下のコマンドを実行して、ファイルを修正します。
```
vi /etc/modules
```
b. ファイルに以下の内容を追加して、保存します。
```
acpiphp
```
 - **openSUSE 12.3 シリーズ**
 a. 以下のコマンドを実行して、ファイルを修正します。
```
vi /etc/sysconfig/kernel
```
b. ファイルに以下の内容を追加して、保存します。
```
MODULES_LOADED_ON_BOOT="acpiphp"
```
