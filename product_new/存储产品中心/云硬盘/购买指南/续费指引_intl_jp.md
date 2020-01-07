タイムリーにCBSを更新するのは、期限切れによるデータロスを効果的に回避できるため、重要なデータに対して定期的な更新通知を設定することをお勧めします。

## Elastic CBSを更新する
- 有効期限が切る前に、Elastic CBSを更新することにより、期限切れ後にディスクがアンマウントされることにより読み書きできないことを防げます。
- Elastic CBSが期限切れから廃棄されるまで（14日以内）リカバリーできることは、タイムリーに更新しないことによってCBSが廃棄されてデータロスになることを防げます。

### コンソールを利用して更新する

1. [CBSコンソール](https://console.cloud.tencent.com/cvm/cbs)にログインします。
2. ターゲットCBSがある行の【更新】をクリックします。
3. CBSの更新画面で、更新したい時間を選択し、【OK】をクリックして、支払いの関連処理を完了させます。

###  API を利用して更新する
RenewDiskインターフェースを利用してElastic CBSを更新します。詳細な操作については、 [CBS更新](https://cloud.tencent.com/document/product/362/16319)をご参照ください。

### コンソールを利用してリカバーする

1.  [CBSごみ箱](https://console.cloud.tencent.com/cvm/recycle/cbs)にログインします 。
2. ターゲットCBSがある行の【リカバー】をクリックします。
3. 支払いの関連処理を完了させます。
    [CBSコンソール](https://console.cloud.tencent.com/cvm/cbs) にログインして、リカバーしたばかりのリソースを確認できます。

## 非Elastic CBSを更新する

### コンソールを利用して更新する
非Elastic CBSはCVMインスタンスのライフサイクルに依存します。それを更新する必要がある場合、詳細な操作については、[インスタンの更新](/doc/product/213/6143)をご参照ください。

### API を利用して更新する
非Elastic CBSはCVMインスタンスのライフサイクルに依存します。RenewInstance インターフェースを利用して非Elastic CBSを更新できます。詳細な操作については、 [インスタンス（サブスクリプション）の更新インターフェース](https://cloud.tencent.com/doc/api/229/1348)をご参照ください。
> 操作中に問題がある場合、[お問い合わせ](https://cloud.tencent.com/document/product/362/34345)にご連絡ください。

