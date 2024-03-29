## 概要
ここでは、デフォルトのCDNアクセラレーションドメイン名を有効化する方法についてご説明します。具体的な手順は次のとおりです。

## 操作手順

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインします。左側ナビゲーションバーの【バケットリスト】をクリックし、バケットリストページに進みます。
2. ドメイン名を設定する必要があるバケットをクリックし、バケット設定ページに進みます。

3. 左側の【ドメイン名と伝送管理】>【デフォルトのCDNアクセラレーションドメイン名】をクリックし、【デフォルトのCDNアクセラレーションドメイン名】設定項目の【編集】をクリックして現在のステータスを有効化し、以下のオプションを設定します。
 - **アクセラレーションリージョン**：中国本土、中国本土以外およびグローバルアクセラレーションをサポートしています。グローバルアクセラレーションとは、すべてのリージョン間でのバケットアクセラレーションをサポートすることを指します。
 - **オリジンサーバータイプ**：通常デフォルトは**デフォルトオリジンサーバー**で、オリジンサーバーのバケットとして静的ウェブサイトを有効化しており、静的ウェブサイトをアクセラレーションしたい場合は、**静的ウェブサイトオリジンサーバー**を選択します。
		![](https://main.qcloudimg.com/raw/f6b32eea091da0d4d9c72e670c7135e8.png)
 - **back-to-origin認証**：バケットがパブリック読み取りの場合、back-to-origin認証を有効化する必要はありません。バケットがプライベート読み取りの場合、[back-to-origin認証の有効化](#step1)を行う必要があります（CDNサービス権限承認が追加されていることを前提とします）。
>?Tencent Cloud CDNサービスをまだご利用でない場合、【ドメイン名管理】に進むことができません。まず[CDNコンソール](https://console.cloud.tencent.com/cdn)に進み、CDNサービスを有効化する必要があります。
4. 【保存】をクリックすると、CDNアクセラレーションが有効化されます。
>!プライベート読み取りバケットに対して、back-to-origin認証とCDNサービス権限承認を同時に有効化すると、CDNがオリジンサーバーへアクセスする際に署名を必要としないため、CDNキャッシュリソースがパブリックネットワーク配信を行い、データセキュリティに影響します。CDN認証を有効化することをお勧めします。


<span id="step1"></span>
#### back-to-origin認証の有効化

- バケットがプライベート読み取りの場合は、CDNサービス権限承認を追加し、back-to-origin認証を有効にする必要があります。
1. デフォルトのCDNアクセラレーションドメイン名の設定画面で【CDNサービス権限承認の追加】をクリックし、指示に従ってCDNサービス権限承認の追加操作を完了します。
![](https://main.qcloudimg.com/raw/f6b32eea091da0d4d9c72e670c7135e8.png)
2. 【back-to-origin認証】をクリックしてボタンをオンにし、バケットのback-to-origin認証を有効化します。
3. 【保存】をクリックすると、CDNアクセラレーションが有効化されます。
4. 保存すると、デフォルトのアクセラレーションドメイン名がデプロイされていることが確認できます。また、**CDN認証**のステータスプロンプトが下に表示されたら、【認証設定】をクリックしてCDN認証の設定を開始します。
 ![](https://main.qcloudimg.com/raw/3b12f1a208662a170c9e829c88006ce3.png)
5. [CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、【ドメイン名管理】>対応するドメイン名の【管理】>【セキュリティコンフィグレーション】を選択します。具体的な設定手順については、[設定の説明](https://intl.cloud.tencent.com/document/product/228/35237)ドキュメントの認証設定の箇所をご参照ください。
