>! If you are a customer of a Tencent Cloud partner, the rules regarding resources when there are overdue payments are subject to the agreement between you and the partner.

<span id="p1"></span>
## 従量課金（後払い）

VODは、日次決済ユーザーに対し、従量課金を行い、残高不足によりアカウントの支払い延滞が発生したユーザーに対し、VODはまずアカウントリソースのサービスを停止し、長期的に支払い延滞が継続するユーザーについては、リソース回収メカニズムを発動します。デフォルトの料金計算方式は日次決済ですが、月次決済に変更したい場合は、サービス担当者にご連絡ください。

## サービス停止メカニズム

VODは支払い延滞が発生したユーザーのアカウントサービスを停止することができます。

- 毎日12：00〜18：00に前日に発生した料金が決済され、請求書が出力され、料金が差し引かれます。
- アカウントの残高不足により料金の差し引きができなかった場合は、料金が差し引かれる時間から24時間以内に、ユーザーは支払い延滞を通知するショートメッセージを受け取ります。料金が差し引かれる時間から24時間以内にアカウントにチャージを完了していない場合、サービスが正式に停止されます。料金が差し引かれる時間から24時間以内にアカウントにチャージを完了した場合、サービスは停止されません。
- サービスの停止後、VODが提供する各種サービスを使用できなくなり、コンソールの使用も禁止されますが、VODファイルと各種設定情報は削除、変更されません。

## 回収メカニズム

アカウントサービスの停止後、30日以内に支払い延滞が発生したアカウントに料金がチャージされずサービスが有効化されない場合は、回収ポリシーが起動します。

- VODはそのアカウント内にストレージされているソースファイルとトランスコードファイルを削除し、リソースをリリースします。**この削除操作を元に戻すことはできません**。
- 重要ファイルが削除されないように、アカウントの支払い延滞情報に注意し、適時、料金を支払うようにしてください。

## サービス開始メカニズム

サービスの停止後に、ユーザーが未払金を支払えば、VODサービス開始ポリシーが起動し、サービスがリスタートされます。リソースの割り当てにかかる時間は約30分であり、アカウントが調整されてから1時間経ってもサービスが開始されない場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category) して弊社にご連絡ください。
