Tencent Cloudは、HTTPレスポンスヘッダーの設定機能を提供します。この機能から、HTTPトランザクションの具体的な操作パラメータを定義できます。レスポンスヘッダー設定は、ドメイン名に関連するものです。このため、いったん有効に設定すると、ドメイン名の下にある任意のリソースのレスポンスメッセージが有効になります。


## 前提条件
- [CSSコンソール](https://console.cloud.tencent.com/live)にログイン済みであること。
- [再生ドメイン名](https://intl.cloud.tencent.com/document/product/267/35970)を追加済みであること。

[](id:limit)
## 使用制限
- 最大10件の設定をサポートできます。
- 重複禁止のメッセージヘッダーにおいては、複数の値のパラメータがあり、パラメータ`値1、値2、値3`から実装します。
- 設定したパラメータ名とバックエンドのプライベートパラメータ名が競合する場合は、システムによって通知されるので、パラメータ名を変更する必要があります。
- カスタマイズしたパラメータ名は、アルファベットの大文字、小文字、数字および-（ハイフン）で構成し、長さは1～100字まで対応します。
- パラメータ値を空にすることはできません。中国語はサポートしていません。長さは1～1000文字まで対応します。


## HTTPレスポンスヘッダーの設定
1. [ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)に進み、設定したい**再生ドメイン名**または右側の**管理**をクリックしてドメイン名詳細ページに進みます。
2. **高度な設定**のタブを選択し、**HTTPレスポンスヘッダーの設定**のタグを確認します。
![](https://qcloudimg.tencent-cloud.cn/raw/57a34fdc0b51c2f9384a677163c302ff.png)
3. **編集**ボタンをクリックし、HTTPレスポンスヘッダーを設定します。既存ルールの編集、既存ルールの削除、ルールの追加をサポートしています。
![](https://qcloudimg.tencent-cloud.cn/raw/2fcc14051e1ed41d2896bbcea41c5293.png)
ルールの追加が必要な場合は、**ルールの追加**をクリックします。

  - **オプションパラメータ**をクリックすることで、既存のパラメータを選択することができます。：`Access-Control-Allow-Methods`、`Access-Control-Max-Age`、`Access-Control-Expose-Headers`から設定します。
![](https://qcloudimg.tencent-cloud.cn/raw/416416d2cba4a0cff15a016ce987658c.png)

<table>
<thead><tr><th style="width:30%">ヘッダーパラメータ</th><th>説明</th></tr></thead>
<tbody>
<tr>
<td>Access-Control-Allow-Methods</td>
<td>クロスドメインが許可するHTTPリクエスト方法の設定に使用します。同時に複数の方法を設定することができます。例：<br><code>Access-Control-Allow-Methods: POST, GET, OPTIONS</code>。</td>
</tr>
<tr>
<td>Access-Control-Max-Age</td>
<td>プレリクエストの有効期間の指定に使用します。単位は秒です。
</tr>
<tr>
<td>Access-Control-Expose-Headers</td>
<td>いずれかのヘッダーを指定し、レスポンスの一部としてクライアントへ公開するのに使用します。
</tr>
</tbody></table>

  - **カスタムパラメータ**をクリックすることで、カスタムパラメータ設定をすることができます。
>! カスタマイズしたパラメータ名は、アルファベットの大文字、小文字、数字および-（ハイフン）で構成し、長さは1～100字まで対応します。パラメータ値は中国語をサポートしていません。長さは1～1000字まで対応します。

![](https://qcloudimg.tencent-cloud.cn/raw/31ee91ac9ef344cd26ea5c89ed73740e.png)
5. 設定完了後、**提出**機能をクリックすることができます。システムはバックエンドのアクティブ化状態に基づき、`設定中、アクティブ化されていません`、`設定エラー、失敗の原因`、`設定はアクティブ化済みです`などと表示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/d8982f6db31f73de86eae641ab82b6ba.png)

