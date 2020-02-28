Tencent Cloud CDNにアクセスして、オリジンサーバーのコンテンツをユーザーに最も隣接するノードへ送信します。直接にサービスノードより迅速に応答することによって、ユーザーアクセスのディレーを有効的に下げて、ユーザビリティを上げます。 
CDNを構成するには、Tencent Cloudアカウントの登録やCDNのアクティブ化、ドメイン名の導入、CNAMEの構成を行う必要があります。本節では順を追って説明します。

## ステップ1：Tencent Cloudアカウントを登録します

既にTencent Cloudアカウントを登録している場合は、このステップをスキップしてください。

<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:16px;">ここをクリックしてTencent Cloudアカウントを登録します</a></div>

## ステップ2：CDNをアクティブ化にします

#### 1. 実名認証を完了します

実名認証を行っていないユーザーの場合は、先に実名認証を行う必要があります。お客様はCDNコンソールまたはアカウントセンターで実名認証を行うことが可能です。認証手順の詳細については[実名認証ガイド](https://intl.cloud.tencent.com/document/product/378/3629) を参照してください。

<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;">ここをクリックしてアカウントセンターに入ります</a></div><br>

![](https://main.qcloudimg.com/raw/e71557f3118bf3579d551bb2ae2e2e9e.png)

#### 2. サービス情報を補完します

[CDNコンソール](https://console.cloud.tencent.com/cdn)に入って、実名認証の情報を確認して、サービス内容を選択してから、【次へ】をクリックします。
![](https://main.qcloudimg.com/raw/087a21d256d40282127396a63b67c7b4.png)

#### 3. 課金モードを選択します

CDNは従量課金と帯域幅課金という二つの課金モードを提供しています。お客様はサービスモデルに応じて課金モードを選択することができます。詳細については、[課金説明](https://cloud.tencent.com/doc/product/228/2949)を参照してください。
サービス条項の同意にチェックを入れた後に、【CDNのアクティブ化】をクリックすると、加速サービスが利用可能になります。
![](https://main.qcloudimg.com/raw/03c8c19ce7c7c73c956c23dc1c36dd3f.png)

## ステップ3：ドメイン名を導入します

お客様は加速サービスに加速ドメイン名を導入する必要があります。CDNは加速ドメイン名によってオリジンサーバーのリソースをCDN加速ノードにキャッシュすると、ユーザーは近くにあるリソースを取得することが可能になって、リソースアクセスの加速を実現できます。詳細については [ドメイン名の導入](https://intl.cloud.tencent.com/document/product/228/5734)を参照してください。 

## ステップ4：CNAMEを構成します

お客様のドメイン名がCDNに導入された後に、ドメイン名サービスプロバイダーのところでCNAMEの構成を完了する必要があります。構成が有効になった後に、CDN加速サービスが利用可能になります。詳細については[CNAMEの構成](https://intl.cloud.tencent.com/document/product/228/3121)を参照してください。
