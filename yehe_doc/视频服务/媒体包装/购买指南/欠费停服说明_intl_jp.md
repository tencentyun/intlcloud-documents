>! If you are a customer of a Tencent Cloud partner, the rules regarding resources when there are overdue payments are subject to the agreement between you and the partner.

## 支払い遅延によるサービス停止の説明
- StreamPackageの日次決済・後払い課金項目は、利用翌日に1日分の消費料金の請求が発生します。請求書の発行時間については、実際の請求時間を基準とします。
- Tencent Cloudアカウントの残高が不足し、アカウントに支払いの遅延があることが検出されると、アカウント支払い遅延のリマインド通知が送信されます。支払い遅延後72時間以内であればチャージできます。アカウントに72時間以内にチャージされた場合、StreamPackageは停止されません。アカウントが72時間以内にチャージされなかった場合、StreamPackageはサービスを停止します。サービス停止後は、コンソールおよびAPIは使用できなくなります。

## 回収の説明
**60日**以上停止状態が続くアカウントについては、Tencent Cloud StreamPackageが自動的にこのアカウント内のStreamPackageリソースを回収し、このアカウント内の関連データと記録（設定、サービスログなど）を定期的に削除します。削除後のデータは取り戻せません。
