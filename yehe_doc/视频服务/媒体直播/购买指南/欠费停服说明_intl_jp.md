>! If you are a customer of a Tencent Cloud partner, the rules regarding resources when there are overdue payments are subject to the agreement between you and the partner.

### 支払い遅延によるサービス停止の説明
- StreamLiveの日次決済・後払い課金項目は、利用翌日に1日分の消費料金の請求が発生します。請求書の発行時間については、実際の請求時間を基準とします。
- Tencent Cloudアカウントの残高が不足し、アカウントに支払いの遅延があることが検出されると、アカウント支払い遅延のリマインド通知が送信されます。支払い遅延後**72時間**以内であればチャージできます。アカウントに**72時間以内**にチャージされた場合、StreamLiveは停止されません。アカウントが**72時間内にチャージされなかった場合、StreamLiveはサービスを停止します。サービス停止後は、コンソールおよびAPIは使用できなくなります。**


### 回収の説明
**60日以上**停止状態が続くアカウントについては、Tencent Cloud StreamPLiveが自動的にこのアカウント内のStreamLiveリソースを回収し、このアカウント内の関連データと記録（設定、サービスログなど）を定期的に削除します。削除後のデータは取り戻せません。
