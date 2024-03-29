
## 操作シナリオ
Tencent Cloud CVMは、ストレージハードウェアメディアの調整をサポートしています。ストレージハードウェアメディアを調整することにより、異なる業務のストレージ要件に柔軟に対応できます。
Tencent Cloudは、[CBS](https://intl.cloud.tencent.com/document/product/213/4953) および[ローカルディスク](https://intl.cloud.tencent.com/document/product/213/5798)の2種類のブロックストレージを提供します。現在、ローカルディスクからCBSへの変更をサポートします。本ドキュメントでは、ディスクメディアの調整方法と関連する注意事項について説明します。
ローカルディスクCVMには次の制限があります：
- ホストリソースの影響を受けるため、構成をカスタマイズできません。
- スナップショットや作成の加速などの機能はサポートされていません。
- データの信頼性が低い。
- 長時間にわたるホスト障害の影響を受けます。

ローカルディスクを持つCVMの制限を解除したい場合は、アカウントの既存のローカルディスクを持つCVMをクラウドディスクを持つCVMに変更できます。

<span id="LocalDiskPrecondition"></span>
## 前提条件
- **CVMの状態**
 この操作は、CVMが【終了】状態の時のみ実行できます。まずは、CVMをシャットダウンしてください。
- **CVMの制限**
 - 入札型CVMは、ローカルディスクからCBSへの変更をサポートしていません。
 - ビッグデータモデル、高IOモデルはローカルディスクからCBSへの変更をサポートしていません
 - ベアメタル型インスタンスはローカルディスクからCBSへの変更をサポートしていません。
- **CVMの設定**
 - CVMのシステムディスクまたはデータディスクには、少なくとも1つの「**通常ローカルディスク**」または「**SSDローカルディスク**」がある場合のみ、ローカルディスクをCBSに変更できます。
 - CVMが配置されているアベイラビリティーゾーンで使用できるCBSタイプがあり、且つ現在のインスタンスのローカルディスクサイズはCBSのサポート範囲内である場合のみ、ローカルディスクをCBSに変更できます。
 - CVMのシステムディスクとデータディスクの両方がローカルディスクである場合、ローカルディスクをCBSに調整すると、CVMの**すべて**のローカルディスクがCBSに調整されます。部分的な調整はサポートされていません。各ディスクのクラウドディスクタイプを個別に設定できます。
 つまり、完全なローカルディスクのCVMでディスクメディアタイプを変更する場合、システムディスクのみCBSに調整することまたはデータディスクのみCBSに調整することはサポートされていません。すべてのディスクに調整する必要があります。
 - ディスクのメディアタイプを変更しても、ディスクのサイズは変わりません。メディアタイプを変更した後、[CBSの拡張](https://intl.cloud.tencent.com/document/product/362/5747) からディスクのサイズを調整できます。
 - ローカルディスクをCBSに変更しても、CVMのライフサイクル、インスタンスID、プライベート/パブリックIP、ディスクデバイス名及びマウントポイントは変更されません。

<span id="LocalDiskNotice"></span>
## 注意事項

- ローカルディスクをCBSに変更する操作にはデータコピーの方式を採用して、ローカルディスク上のデータをCBSシステムにコピーしますので、ソースのローカルディスクのサイズおよびデータ転送速度の制限を受けます。この操作の完了には時間がかかります。しばらくお待ちください。
- ローカルディスクをCBSに変更することのみが可能です。ローカルディスクをすでにCBSに変更している場合、このCBSをローカルディスクに戻すことはできません。
- **変更が完了した後、データが失われていないかどうかを確認するために、CVMを起動してログインすることをお勧めします**。

## 操作手順
1. [CVMコンソール](https://console.cloud.tencent.com/cvm)にログインし、インスタンス管理ページに進みます。
>? CVMが「無効」状態の場合は、直接[手順3](#step3)を実施します。
2. （オプション）調整対象のCVMの右側で、【その他】>【インスタンス状態】>【シャットダウン】を選択して、シャットダウン操作を実行します。
<span id="step3"></span>
3. 調整対象のCVMの右側で、【その他】>【リソース調整】>【ディスクメディアタイプの調整】をクリックします。
4. 【ディスクメディアの調整】ダイアログボックスで、システムディスク/データディスクに調整したいターゲットCBSタイプを選択し、同意のチェックボックスをONにすると、【すぐに変換する】をクリックします。
5. 情報を確認し、支払いが必要な注文を完了して、プロセスが完了するまで待ちます。
 
