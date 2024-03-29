﻿
## サブスクリプションTencentDB
### アラートの説明
クラウドリソースは、有効期限7日前になってからリソースがリリースされるまでの間、ユーザにアラートメッセージをプッシュします。具体的には、メールやSMSなどでTencent Cloudアカウントの作成者およびグローバルなリソースコラボレーター、財務コラボレーターに通知します（実際の受信方法は、ユーザの[メッセージセンター](https://console.tencentcloud.com/message)でのサブスクリプション設定をご確認ください）。
### 回収の仕組み
- TencentDBリソースの有効期限7日前になると、ユーザへ更新通知を送信します。
- 期限切れて7日以内にはTencentDBが使えますが、更新する必要があります。TencentDB期限切れの通知が届きます。
期限切れて8日目から、TencentDBは使用できなくなり、ごみ箱に回収されます。ユーザはコンソールのごみ箱ページでデバイスを確認し、更新操作を実施できます。
- ごみ箱での保持期間は**7日間**です。TencentDBがごみ箱に7日間保持されても更新を行っていない場合、リソースが回収され、データはクリアされ復元できなくなります。
- つまり、期限切れになっても、TencentDBには**7日間の利用可能期間**及び**7日間の利用不可期間**があります。ユーザはこの14日間でデバイスを更新できます。残額が十分である場合、自動更新を設定しているデバイスは自動的に更新されます。
## 従量課金クラウドデータベース
>!
>- 従量課金リソースを使用しなくなった場合は、課金が継続されないように、**速やかに破棄してください**。
>- お客様の実際のリソース消費は常に変化しているため、残高に関する事前アラートにはある程度の誤差が存在する可能性があります。

### 事前アラート説明
- システムは毎時0分に従量課金リソースの料金を差し引きます。アカウントの残高が0未満となった時点で、システムはメール、ショートメッセージなどの方法でTencent Cloudアカウントの作成者およびグローバルなリソースコラボレーター、財務コラボレーターに通知します（実際の受信方法は、ユーザーの[メッセージセンター](https://console.cloud.tencent.com/message)でのサブスクリプション設定に準じます）。
- メッセージ通知メカニズムについては、[従量課金説明 > 支払い延滞処理のメカニズム](https://intl.cloud.tencent.com/document/product/555/30328)をご参照ください。

### 支払い延滞処理
1. **アカウント残高が0未満となった時点で：**
 - 24時間は、クラウドデータベースを引き続き利用でき、課金も継続して行われます。
 - 24時間後、クラウドデータベースは**自動的にシャットダウンし**、課金を停止します。

2. **自動シャットダウン後：**
 - シャットダウンから3日以内に、残高が0以上になるようにチャージした場合、起動して課金も継続することができます。アカウント残高が0未満の場合は起動できません。
 - シャットダウンから3日後に、アカウント残高が引き続き0未満の状態であった場合、クラウドデータベースは回収されてデータがすべて削除され、元に戻せなくなります。クラウドデータベースの回収の際、システムはメール、ショートメッセージなどの方法でTencent Cloudアカウントの作成者およびグローバルなリソースコラボレーター、財務コラボレーターに通知します。

![](https://main.qcloudimg.com/raw/2a4084a3304cd60ede9a2675feda9e97.png)





