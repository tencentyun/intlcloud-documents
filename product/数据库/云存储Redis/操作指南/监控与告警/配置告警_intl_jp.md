##　操作シナリオ
TencentDB for Redis には総合的なカスタムアラーム機能が備えられ、指標データが一定の閾値を超えた場合に SMS でアラームを発します。本項では、TencentDB for Redis コンソールでアラームを設定するプロセスについて説明します。

## 操作手順
1. [Redis コンソール](https://console.cloud.tencent.com/redis)にログインし、次のアイコンをクリックしてアラームページに移動します。
![](https://main.qcloudimg.com/raw/51fe5d9b8490699db4211ed7980f9b14.png)
2. アラームページで【アラーム設定】をクリックします。
![](https://main.qcloudimg.com/raw/256855352c13bcca7ad5e21ab18304e8.png)
3. ポリシーの新規作成ページでパラメータを設定します。アラームサービスの詳細については、[アラームサービスの概要](https://cloud.tencent.com/document/product/248/6126)を参照してください。
 - ポリシータイプ：TencentDB for Redis を選択します。
 - アラーム対象：関連付けるインスタンス対象を選択します。
 - アラームチャネル：承認グループを設定し、SMS で受信する対象を選択します。
![](https://main.qcloudimg.com/raw/09bbe7a937f717511e99062f52ea9024.jpg)
4. 間違いがないか確認してから【完了】をクリックします。

