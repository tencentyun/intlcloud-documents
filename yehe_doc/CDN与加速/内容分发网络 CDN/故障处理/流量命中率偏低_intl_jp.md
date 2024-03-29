## 現象の説明

リアルタイムモニタリングでのトラフィックヒット率の数値が低く、想定を満たさない。

## 考えられる原因

- キャッシュ更新が行われた
  キャッシュ更新により、指定されたコンテンツがノード上でクリアされ、一時的にトラフィックヒット率が低下する状況が発生します。
- オリジンサーバーに新しいリソースがある
  オリジンサーバーに新しいリソースが多くある場合、CDNノードでback-to-originが発生し、トラフィックヒット率が低下します。
- オリジンサーバーの異常
  オリジンサーバーに不具合が起こり、5XXまたは4XXエラーが多くなった場合、トラフィックヒット率に影響します。
- キャッシュポリシーの設定が適切でない
  実際の業務状況に合わせてキャッシュルールを設定してください。
- Back-to-Origin of Rangeがオフになっている
  Back-to-Origin of Rangeがオフの場合、リクエストに応じて分割して引き出すのではなく、back-to-origin時に大容量ファイルをすべて引き出します。これによりback-to-originトラフィックが増加し、トラフィックヒット率に影響します。
- ドメイン名設定のキャッシュキールール（すべてのパラメータを無視）が適用されたが、オリジンサーバーのリソースがパラメータの違いによって異なる
  オリジンサーバーのリソースがパラメータの違いによって異なる一方で、CDNはすべてのパラメータを無視してキャッシュを行うため、異なるパラメータのリソースがリクエストされた場合、対応するリソースにマッチせず、トラフィックヒット率に影響します。

## 解決方法

1. オリジンサーバーに異常がないかどうか確認します。
2. キャッシュ更新が行われたり、オリジンサーバーに新しいリソースが多かったりする場合、これは正常な現象です。
3. オリジンサーバーが、URLパラメータに基づき異なるリソースを出力するのと、CDNドメイン名設定のキャッシュキールール（すべてのパラメータを無視）が同時に使用されてないことを確認します。
4. 実際の業務状況に合わせてキャッシュルールを設定します。

## 処理手順
[](id:step1)
1. オリジンサーバーに異常がないか、またはキャッシュ更新が行われてないか確認します。
   - YESの場合、ヒット率の低下は正常な現象です。
   - NOの場合は、[手順2](#step2)を実行してください。
[](id:step2)
2. 自分の業務状況に応じて、オリジンサーバーがURLパラメータに基づき異なるリソースを出力するかどうか判断します。
   - YESの場合は、[手順3](#step3)を実行してください。
   - NOの場合は、[手順5](#step5)を実行してください。
[](id:step3)
3. [CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、【ドメイン名管理】を選択して対応するドメイン名設定を見つけ、【キャッシュ設定】>【キャッシュキールールの設定】の「パラメータを無視」の項目を確認します。CDN設定のドメイン名で、パラメータキャッシュを無視する機能が有効になっているかどうか確認します。
![img](https://main.qcloudimg.com/raw/53ceba436ae110bd0dafef8bad72ceff.png)
   - YESの場合は、[手順4](#step4)を実行してください。
   - NOの場合は、[手順5](#step5)を実行してください。
[](id:step4)
4. キャッシュキールール設定内の対応するルールの操作欄で、【変更】をクリックし、ポップアップ表示された「ルールの修正」ボックスでパラメータの無視機能をオフにしてから、【保存】をクリックします。
![img](https://main.qcloudimg.com/raw/f866bc80c384bc6daca649dbeb006fdb.png)
すべてをオフにすることがユーザーにとって不都合な場合のために、CDNには指定パラメータの無視を保持する機能が用意されています。ユーザーは実際の業務ニーズに基づき使用を選択することができます。具体的な方法については[キャッシュキールールの設定](https://intl.cloud.tencent.com/document/product/228/35316)をご参照ください。
>
[](id:step5)
5. [CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、【ドメイン名管理】を選択して対応するドメイン名設定を見つけ、【キャッシュ設定】>【ノードキャッシュ期限切れ設定】を確認します。キャッシュルールが自身の業務やオリジンサーバーの実際の状況に適合しているか確認してください。
   - YESの場合は、[手順5](#step5)を実行してください。
   - NOの場合は、[ノードキャッシュ期限切れ設定](https://intl.cloud.tencent.com/document/product/228/38424)を参照し、キャッシュルールを調整してください。
