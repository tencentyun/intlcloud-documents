## ユースケース

**共有イメージ**とは、自ら作成した[**カスタマイズイメージ**](https://intl.cloud.tencent.com/document/product/213/4942)を**他のユーザーに**共有することです 。 ユーザーは簡単に他のユーザーから共有イメージを取得できます。この共有イメージから必要なコンポーネントを取得して、カスタマイズ内容を追加できます。 

> Tencent Cloudは他のユーザーとイメージを共有する時、完全性或はセキュリティを保証することはできません。ユーザーは信頼できるソースの共有イメージを使用することをお勧めします。

## 注意事項
 - 一つのイメージは最大50個のユーザーと共有できます。
 - 共有イメージの名前と説明を変更することができません、CVMインスタンスの作成にのみ使用可能です。
 - 他のユーザーと共有するイメージは、独自のイメージクォータを占有しません。
 - 他のユーザーと共有したイメージを削除できますが、その前にこのイメージのすべての共有を取り消す必要があります。共有を取り消すことの詳細については、[カスタマイズイメージ共有の取り消し](/doc/product/213/7148)をご参照ください。取得した共有イメージを削除できません。
 - イメージは相手アカウントの同一リージョンへの共有をサポートしています。別リージョンに共有する必要がある場合は、イメージをこのリージョンにコピーしてから共有処理を行います。
 - 取得した共有イメージを他のユーザーと共有することができません。

## 操作手順

### アカウントIDを取得する

Tencent Cloud共有イメージは、対向側アカウントの唯一IDによって識別されます。以下の方法で取得することを該当のユーザーに通知します：
 1. [CVMコンソール](https://console.cloud.tencent.com/cvm/)にログインします。
 2. 右上にあるアカウント名をクリックして、【アカウント情報】を選択します。
  3. 「アカウント情報」管理画面で、アカウントIDを表示及び記録します。
 4. 取得したアカウントIDを自分に送信するように相手に通知します。

### コンソール経由で共有する

 1. [CVMコンソール](https://console.cloud.tencent.com/cvm/)にログインします。
 2. 左側ナビゲーションバーで、【[イメージ](https://console.cloud.tencent.com/cvm/image)】をクリックします。
 3. 【カスタマイズイメージ】タブを選択して、カスタマイズイメージ管理画面に入ります。
 4. カスタマイズイメージリストで、共有したいカスタマイズイメージを選択して、右側の【共有】をクリックします。
 5.  ポップアップの「共有イメージ」ウィンドウで、相手のアカウントIDを入力し、【共有】をクリックします。
 6. 相手に[CVMコンソール](https://console.cloud.tencent.com/cvm/)にログインすることを通知し、【イメージ】>【共有イメージ】を選択して、共有したイメージを確認することができます。
 7. 複数のユーザーに共有する場合は、上記の手順を繰り返してください。

### API経由で共有します

ShareImageインターフェースを使用してイメージを共有できます。
