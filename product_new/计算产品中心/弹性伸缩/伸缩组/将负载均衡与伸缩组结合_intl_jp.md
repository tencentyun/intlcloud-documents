ASでCVMインスタンスを追加及び削除する場合、アプリケーションのトラフィックがすべてのCVMインスタンスにアサインされるように確保する必要があります。あるload balanceにCVMをスケールアウトすることを希望すれば、かつユーザーの介入なしでload balanceから転送されるトラフィックを取得する場合は、CVMにload balanceを指定する必要があります。このload balanceは、Auto Scalingグループ内のインスタンスのすべての転送トラフィックのシングルアクセスポイントとして機能します。

**スケーリンググループにCloud Load Balancerを追加する**

スケーリンググループとCLBを統合することにより、Cloud Load Balancerを既存のスケーリンググループに付与することができます。 Cloud Load Balancerに付与した後、グループにインスタンスが自動的に登録され、転送トラフィックがそれらのインスタンスに配布されます。

AS [コンソール](https://console.cloud.tencent.com/autoscaling)で【新規作成】を選択し、画面の下部に「Cloud Load Balancer」オプションがあり、必要なCloud Load Balancerを選択できます。 事前に作成していない場合は、オプションの下にある“新規作成”リンクをクリックして、新しいCloud Load Balancerを作成します。

>スケーリンググループに関連されたCloud Load Balancerインスタンスは、スケーリンググループと同じネットワーク環境にある必要があります（VPCまたは同じリージョン内の基幹ネットワーク）。


**スケーリンググループのCloud Load Balancerを削除する**

クリックしてスケーリンググループの詳細画面に入り、詳細の下部に「修正」をクリックして、該当するLBを削除することができます。

削除後、スケーリンググループ内のCVMも、削除されたCloud Load Balancerによって自動的にバインド解除されます。
