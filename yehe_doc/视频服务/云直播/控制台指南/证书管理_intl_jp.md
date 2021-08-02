ライブストリーミングのドメイン名はシンプルなHTTPプロトコルを使用し、HTTPはSSL/TLSプロトコルでカプセル化され、HTTPSとして、データを暗号化して送信します。複数のドメイン名を一括で管理してSSL証明書を設定する場合は、【証明書管理】でSSL証明書のクエリーと設定を一括で実現することができます。

## 設定の原理
ドメイン名のSSL証明書の設定は、送信中にユーザーのキー情報を暗号化して、 SSL証明書を基にサイトを HTTP（Hypertext Transfer Protocol）から HTTPS（Hyper Text Transfer Protocol over Secure Socket Layer）に切り替えること、つまり、SSL（Secure Socket Layer）を基に安全なデータ伝送を行う暗号化版 HTTPプロトコルを実施することを目的としています。 

[](id:c_ssl)
## 証明書設定
1. CSSコンソールの【[ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)】に進み、【証明書管理】をクリックして証明書管理の設定ページに進みます。
![](https://main.qcloudimg.com/raw/e39413b101a445ed747d78c8c9e7c8ac.png)
2. 【証明書設定】をクリックして証明書設定を作成します。
![](https://main.qcloudimg.com/raw/5aeee06ba8b978b823be16e9191bf705.png)
3. 証明書設定のポップアップウィンドウで証明書のアップロード方法を選択します。Tencent Cloudでは2種類の証明書ソースをサポートしています：
  - **証明書をお持ちの場合**：証明書の備考を入力し、証明書の内容と証明書の暗号鍵を入力する必要があります。その証明書が正常に保存されると、 [SSL証明書管理](https://console.cloud.tencent.com/ssl)に同期され、そこで証明書を確認できます。証明書の内容と証明書の暗号鍵の入力操作は [HTTPS設定](https://intl.cloud.tencent.com/document/product/267/31066)をご参照ください。
![](https://main.qcloudimg.com/raw/998de2fdadf6ed9ab52e7fdcef288f51.png)
  - **Tencent Cloudホスト証明書 **：Tencent Cloud SSL証明書管理で購入済みの証明書を選択して、証明書リストから証明書に適したアクセラレーションドメイン名を選択できます。
![](https://main.qcloudimg.com/raw/4f36c491c7392798bc81410ecc65ae6e.png)
4. 証明書に誤りがないことをチェックした後、【次のステップ】をクリックしてドメイン名設定画面に進みます。
5. 「関連付けられたドメイン名」欄で証明書のドメイン名を基に、符合した再生ドメイン名をフィルタリングして選択すれば、複数を選択できます。現在のドメイン名をほかの証明書にバインドしている場合は、上書きして証明書を更新します。
6. 選択が終わると、右側の「選択済み」欄に選択したドメイン名およびバインド後のステータスが表示されます。
![](https://main.qcloudimg.com/raw/bc1a0c51023d295120b8c94420b7b628.png)
7. 選択したドメイン名と同時にHTTPS設定を有効にするかを選択します：
  >? 
  >- 【HTTPS設定を同時に有効にする】ボタンで、 HTTPS 設定を有効にするかどうかを選択します。有効にすると、 HTTPとHTTPSを同時にサポートします。無効にするとHTTPのみをサポートします。
  >- 【HTTPS設定を同時に有効にする】ボタンはデフォルトでは有効になっています。保存後は更新したドメイン名でHTTPS設定が有効になります。無効にすると証明書の更新のみが実行され、 HTTPSのON/OFFは変更されません。
6. 【OK】をクリックして証明書の設定を完了します。


[](id:check)
## 証明書設定の確認
[証明書の設定](#c_ssl) が完了すると、【[証明書管理](https://console.cloud.tencent.com/live/common/certificate)】の設定リストで作成された設定情報を確認することができます。表示されるデータには、証明書設定済みのドメイン名、証明書の備考、証明書ソース、HTTPS設定および有効期限があります。
![](https://main.qcloudimg.com/raw/e4012e075b695afc912840462e0c5694.png)

[](id:update)
## 証明書設定の更新
1. 【[証明書管理](https://console.cloud.tencent.com/live/common/certificate)】の設定リストで、**更新**する設定の列の右側にある【更新】をクリックします。
![](https://main.qcloudimg.com/raw/bfad71179c2ab41cd3c35e23e47e0224.png)
2. 証明書の設定画面に進み、 [証明書の設定](#c_ssl) 情報を更新します。
3. 【OK】をクリックし、再送信して証明書を更新します。

[](id:delete)
## 証明書のバインドの削除
1. 【[証明書管理](https://console.cloud.tencent.com/live/common/certificate)】の設定リストで、**削除**する設定情報の列の右側にある【削除】をクリックします。
![](https://main.qcloudimg.com/raw/a5d8f92c8aa7f2264c56e5ef6bf1f15b.png)
2. 証明書のバインドの削除の要否を確認して、【OK】をクリックして削除します。
![](https://main.qcloudimg.com/raw/10305e0609cfcda523505cbcf8a099c8.png)
>! 削除後は、このドメイン名ではHTTPS設定を使用することはできません。


