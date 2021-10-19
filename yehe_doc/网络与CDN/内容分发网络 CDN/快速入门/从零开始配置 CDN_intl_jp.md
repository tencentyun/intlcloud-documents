Tencent Cloud CDNに接続すると、オリジンサーバーのコンテンツをエンドユーザーの最も近いサービスノードに配信され、サービスノードからユーザーリクエストに迅速に直接応答するため、ユーザーのアクセス遅延を効果的に減らし、可用性を向上させることができます。 
CDNの設定には、Tencent Cloudアカウントの登録、CDNのアクティブ化、ドメイン名のアクセス、CNAMEの設定が必要になります。ここでは順番にご説明していきます。

## 手順1：Tencent Cloudアカウントの登録
Tencent Cloudのアカウント登録が済んでいる場合は、このステップを無視してかまいません。
<div style="background-color:#00A4FF; width: 425px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3149.btn1">ここをクリックしてTencent Cloudアカウントを登録します</a></div>

## 手順2：CDNのアクティブ化 
#### 1. 実名認証の完了
実名認証をまだ行っていない場合は、先に実名認証を済ませる必要があります。CDNコンソールまたはアカウントセンターから実名認証を行うことができます。詳しい認証手順は、[実名認証ガイド](https://intl.cloud.tencent.com/document/product/378/3629)をご参照ください。
<div style="background-color:#00A4FF; width: 425px; height: 35px; line-height:35px; text-align:center;;"><a href="https://console.cloud.tencent.com/cdn" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3149.btn2">ここをクリックして CDN コンソールに入ります</a></div><br>

![](https://main.qcloudimg.com/raw/e593cf6199d64fbcc5c6f50089778cf9.png)
<div style="background-color:#00A4FF; width: 425px; height: 35px; line-height:35px; text-align:center;;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3149.btn2">ここをクリックしてアカウントセンターに入ります</a></div><br>

![](https://main.qcloudimg.com/raw/e71557f3118bf3579d551bb2ae2e2e9e.png)
#### 2. CDNサービスのアクティブ化
実名認証の完了後、CDNサービスのアクティブ化ができるようになります。
（1）課金方式の選択
Tencent Cloud CDNは、**中国国内**と**中国国外**の2つのサービスリージョンに分かれます。2020年12月7日21:30より、CDNをアクティブ化した時の課金方式は【1時間単位のトラフィック課金】のみをサポートしています。より詳しい説明については、[課金説明](https://intl.cloud.tencent.com/document/product/228/2949)をご参照ください。
![](https://main.qcloudimg.com/raw/5f75a3047566df1413233c2c0ac2736f.png)
（2）CDNのアクティブ化 
サービス条項にチェックを入れて同意した後、【CDNのアクティブ化】をクリックすると、アクティブ化が完了し、CDNサービスの使用を開始できます。
![](https://main.qcloudimg.com/raw/4b1997247ae88641d1c2af0289b7ad2a.png)

## 手順3：ドメイン名のアクセス
お客様のアクセラレーション業務のために、アクセラレーションドメイン名にアクセスする必要があります。CDNはアクセラレーションドメイン名を介してオリジンサーバーのリソースをCDNアクセラレーションノードにキャッシュします。これによりユーザーは必要なリソースを近くで取得でき、リソースアクセスの加速を実現できます。詳細については、 <a href="https://intl.cloud.tencent.com/document/product/228/5734" hotrep="document.guide.3149.linkdomain">ドメイン名のアクセス</a>をご参照ください。

## 手順4：CNAMEの設定
お客様のドメイン名がCDNに接続された後、さらにドメイン名のサービスプロバイダー側でCNAMEの設定を完了させる必要があります。設定が有効になると、CDNアクセラレーションサービスをご利用いただけるようになります。詳細については、<a href="https://intl.cloud.tencent.com/document/product/228/3121" hotrep="document.guide.3149.linkcname">CNAMEの設定</a>をご参照ください。
