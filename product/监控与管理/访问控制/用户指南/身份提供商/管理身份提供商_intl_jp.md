## SAML IDプロバイダーの削除

IDプロバイダーを管理する方法は2つあります。CAMコンソールまたはCAM APIを使用する方法です。

### コンソールで削除
1.	アクセス管理（CAM）コンソールにログインし、[IDプロバイダー](https://console.cloud.tencent.com/cam/idp)ページに移動します。
2. アカウントのIDプロバイダーリストで、削除するIDプロバイダーを選択し、【操作】の【削除】をクリックします。
3.	IDプロバイダーを削除するときは、関連するIDプロバイダーを削除するかどうかを確認し、【OK】をクリックしてIDプロバイダーを削除できます。

### APIで削除

- （オプション）すべてのIdP情報をページ別にリストするために、[ListSAMLProviders](https://intl.cloud.tencent.com/document/product/598/30298)を呼び出してください。
- （オプション）特定のプロバイダーに関する詳細情報を取得するために、[GetSAMLProvider](https://intl.cloud.tencent.com/document/product/598/30297)を呼び出してください。
- SAML IDプロバイダーを削除するために、[DeleteSAMLProvider](https://intl.cloud.tencent.com/document/product/598/30301)を呼び出してください。

## SAML IDプロバイダーの変更

IDプロバイダーを変更する方法は2つあります。CAMコンソールまたはCAM APIを使用する方法です。

### コンソールで変更
1.	アクセス管理（CAM）コンソールにログインし、[IDプロバイダー](https://console.cloud.tencent.com/cam/idp)ページに移動します。
2.	アカウントのIDプロバイダーリストで、変更するIDプロバイダーを選択し、プロバイダー名をクリックして詳細ページに移動します。
3.	メタデータドキュメントをアップロードして現在のIDプロバイダーを再定義して、または現在のメタデータドキュメントをダウンロードできます。

### APIで変更

SAML IDプロバイダーの説明、またはメタデータドキュメントをアップデートします。
- 次の操作を呼び出す：[UpdateSAMLProvider](https://intl.cloud.tencent.com/document/product/598/30296)
