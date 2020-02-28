## back to origin ホストとは
back to origin ホストは、CDNノードがback to originプロセス中に、オリジンサーバーでアクセスするサイトのドメイン名を示します。設定されたback to origin ホストが正常にアクセスできるようにしてください。そうしないと、back to originが失敗することを引き起こし、ユーザーの業務に影響を与えます。また、業務状況に基づいてカスタムホストヘッダーを設定することもできます。


> -オリジンサーバーとback to origin ホスト：オリジンサーバーに複数のWebサイトが存在する可能性がありますが、back to origin ホストはリソースが存在するサイトを明確にします。

> - 関連部門の規定により、オリジンサーバーがTencent Cloud CVMの加速ドメイン名である場合、設定されたback to origin ホストドメイン名はTencent Cloudに登録する必要があります。

## 設定ガイド
### 設定の確認
　1. [CDNコンソール](https://console.cloud.tencent.com/cdn)にログインして、左側のメニュー欄の【Domain Management】を選択し管理画面に入ります。

　2.表示されるドメインリストの中で編集したいドメイン名の行を見つけ、アクションバーで【管理】をクリックします。

　3.基本設定ページの一番下に、back to originホストの設定情報が表示されます。
![](https://main.qcloudimg.com/raw/650b683d8908042600b24d0d410a9b10.jpg)

デフォルトでは、サブドメイン名のback to originホストは設定された加速ドメイン名であり、汎用ドメイン名のback to originホストはアクセスドメイン名です。
	-　アクセスした加速ドメイン名が「wwww.test.com」である場合、このノードはこのドメイン名におけるリソースにback to originリクエストを発送する時、Request HTTP HeaderのHostフィールドの値は「wwww.test.com」となります。
	- 　追加された加速ドメイン名が「*.test.com」のような汎用ドメイン名である場合、アクセスドメイン名が「abc.test.com」である場合、back to originホストは「abc.test.com」となります。

### back to originホストの変更
back to originの設定情報で【edit】をクリックすることで、back to originホストの設定を調整することができます。

![](https://main.qcloudimg.com/raw/13e522ee379e14a998a5be0e0b2daf47.jpg)


## 設定ケース
ユーザーのアクセスドメイン名は「www.test.com」で、オリジンサーバーにドメイン名「origin.test.com」が設定する場合、「origin.test.com」に対応するA記録は「1.1.1.1」です。
ユーザーリクエストは「http://www.test.com/1.jpg」です。
1. 次の通りに設定されている場合、
 
 
 ![](https://main.qcloudimg.com/raw/13e522ee379e14a998a5be0e0b2daf47.jpg)


デフォルトでは、back to originホストは加速ドメイン名で、back to originする時、実際のリクエストは「1.1.1.1」に送信されます。
   取得されたリソースは「http://www.test.com/1.jpg」です。


2. 次の通りに設定されている場合、

![](https://main.qcloudimg.com/raw/0ea2184b08ddfc4ad54ec3467ea93bc2.jpg)


back to originホストは「origin.test.com」で、back to originする時、実際のリクエストは「1.1.1.1」に送信されます。
取得されたリソースは「http://origin.test.com/1.jpg」です。
