Inputセキュリティグループは、フィルタリング機能を持つステートフルな仮想ファイアウォールです。主にプッシュタイプのinputについて、ユーザーがプッシュする際にセキュリティチェックを行います。現在IP(セグメント）ホワイトリスト方式をサポートしています。Tencent Cloudが提供するネットワークセキュリティに関する重要な隔離手段です。



## 前提条件
- [StreamLive](https://intl.cloud.tencent.com/products/mdl)はすでにアクティブ化されています。 
- [StreamLiveコンソール](https://console.intl.cloud.tencent.com/mdl/security)にログイン済みです。

## Inputセキュリティグループの管理
左側ナビゲーションバーの**Security Group Management**をクリックすると、すでに作成したinputセキュリティグループの名称、使用状態、IDを確認できます。また、作成、編集、削除操作も可能です。現在Tencent Cloud StreamLiveは、すでにムンバイ（インド）、バンコク（タイ）、ソウル（韓国）、東京（日本）、フランクフルト（ドイツ）の5カ所のアベイラビリティーゾーンで提供されています。ここからお客様の所在リージョンを選択できます。他のアベイラビリティーゾーンでデプロイのリクエストがある場合は[お問い合わせ](https://intl.cloud.tencent.com/contact-us)ください。

![](https://qcloudimg.tencent-cloud.cn/raw/fc7c32157eccae3591533e14c511fa8f.png)


### Inputセキュリティグループの作成
セキュリティグループは、入力ソースのIPV4アドレスの有効性を検証するために用いられます。セキュリティグループの設定を入力することにより、StreamLiveチャネルの入力をより安全なものにできます。inputセキュリティグループを作成する場合は、ページの左上隅にある**Create Security Group**ボタンをクリックし、ポップアップウィンドウで設定を行います。
1）**Name**：セキュリティグループの名称は、ユーザーによるカスタマイズが可能です。1～32桁の数字、アルファベット、アンダーバー「_」をサポートしています。
2）**IP Allowlist**：IPホワイトリストは、CIDR形式を使用します。コンマあるいは改行で区切られます。ソースIPの制限が不要な場合、0.0.0.0/0と入力すれば完了です。
入力後に**Confirm**ボタンをクリックすると、作成完了です。

![](https://qcloudimg.tencent-cloud.cn/raw/4fd4169c10d7b6f968f323822c37301a.png)

### Inputセキュリティグループの変更
Inputセキュリティグループの変更を行う場合、変更したい**input security group**の右側にある**Edit**をクリックし、ポップアップウィンドウで編集を行います。編集完了後に**Confirm**をクリックすると、変更が完了します。

![](https://qcloudimg.tencent-cloud.cn/raw/6fbf87ce94c7c1cc8e9914c5fb9425ef.png)

### Inputセキュリティグループの削除
Inputセキュリティグループの削除を行う場合、削除したい**input security group**の右側にある**Delete**をクリックします。ポップアップウィンドウで**Confirm**をクリックすると、削除が完了します。

![](https://qcloudimg.tencent-cloud.cn/raw/b0f08d28e5b0658c04756a179100dad9.png)

>?
>- セキュリティグループには、idleとoccupiedという2つのステータスがあります。
>- idleとは、現在のセキュリティグループがバインドされておらず、編集と削除ができることを意味します。
>- occupiedとは、現在のセキュリティグループがchannel-inputにバインドされていることを意味します。現時点では、セキュリティグループは編集のみが可能で、削除はできません。
>- コンソールがデフォルトでサポートしているセキュリティグループの作成は5つまでです。これ以上のセキュリティグループ作成が必要な場合は、[チケットを提出](https://console.cloud.tencent.com/workorder)してTencent Cloudカスタマサービス担当者までご連絡ください。

