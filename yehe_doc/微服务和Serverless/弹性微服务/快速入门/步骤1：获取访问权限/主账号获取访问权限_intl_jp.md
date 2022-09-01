## 操作背景

TEMは他のクラウド製品のAPIにアクセスする必要があるため、TEMにサービスロール作成のための権限を与える必要があります。

## 前提条件

[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)

>?Tencent Cloudアカウントの登録を行うと、システムはデフォルトで1つのルートアカウントを作成します。これを使用してTencent Cloudのリソースに速やかにアクセスすることができます。

## 操作手順

TEMを初めて使用する際は、次の手順に従って、TEM_QCSLinkedRoleInAccessClusterサービスロール、TEM_QCSLinkedRoleInTEMLogサービスロールをそれぞれ作成し、他のクラウド製品リソースへのアクセス権限を承認する必要があります。

1. **ルートアカウント**を使用して、[TEMコンソール](https://console.cloud.tencent.com/tem)にログインします。
   ![](https://qcloudimg.tencent-cloud.cn/raw/9d3dc63147c10a39be367806c0871d3f.png)
2. **権限承認に進む**をクリックし、[CAMコンソール](https://console.cloud.tencent.com/cam/overview)に進んで権限承認を行います。**権限承認に同意**をクリックすると、TEM_QCSLinkedRoleInAccessClusterサービスロールが作成され、CLS以外のクラウド製品リソースへのアクセス権限が承認されます。
   ![](https://qcloudimg.tencent-cloud.cn/raw/bfc5e42cacfd469b62aa4e7199ff163a.png)
3. [TEMコンソール](https://console.cloud.tencent.com/tem)に戻り、**権限承認の完了**をクリックします。
4. 左側ナビゲーションバーで**アプリケーション管理**をクリックし、ポップアップした権限承認ウィンドウで**権限承認に進む**をクリックし、[CAMコンソール](https://console.cloud.tencent.com/cam/overview)に進んで権限承認を行います。**権限承認に同意**をクリックすると、TEM_QCSLinkedRoleInTEMLogサービスロールが作成され、CLSクラウド製品リソースへのアクセス権限が承認されます。



   
