[コンソール](https://console.cloud.tencent.com/autoscaling/config)を開き、ナビゲーションバーの【スケーリンググループ】を選びます。

### a.リージョンを選択する

コンソール上部で作成対象のリージョンを選択します。リージョンの選択により、手動で追加できるCVMとバインディングできるCloud Load Balancerが制限されます。例えば、起動設定のリージョンを中国広州に選ぶと、スケーリンググループに自動で追加されたのは広州のCVMとなります。広州リージョンのスケーリンググループで手動で上海、北京、中国香港、トロントなどのリージョンにCVMを追加することとCloud Load Balancerをバインディングすることができません。

![](https://mc.qcloudimg.com/static/img/9a39d87fa90f3ae5995073a6077b1057/1.jpg)

### b.定義情報
「新規作成」ボタンをクリックし、スケーリンググループの属性を定義します：

  - **スケーリンググループ名**：このスケーリンググループを表示します。例えば「ウェブサイトロジック層」
  - **最小スケーリング数**：スケーリンググループ中の最小インスタンス数を指定します
  - **初期インスタンス数**：スケーリンググループ開始する時**自働的に**稼働するインスタンス数量を指定します。スケーリンググループを作成した後、対応する数のインスタンスを作り出す
  - **最大スケーリング数**：スケーリンググループ中の最大インスタンス数を指定する
  - **起動設定**：作成された起動設定を指定し、スケールアウトする時起動設定に応じてCVMのスケールアウトを作成します。
  - **ネットワークのサポート**：選択したのはスケールアウトされたCVMのネットワーク属性です。つまり、スケールアウトされたCVMが基幹ネットワークにあるか、Virtual Private Cloud（VPC）にあるかのことです。クラスターがVPCを使用しない限り、通常は「基幹ネットワーク」を選択します。
  - **アベイラビリティーゾーンのサポート**：自動的にスケールアウトされたCVMが生成できるアベイラビリティーゾーンを指定します。複数のアベイラビリティーゾーンを選択でき、自動的にスケールアウトされたCVMがチェックしたアベイラビリティーゾーンからランダムに作成され、クロスアベイラビリティーゾーンの災害復帰効果を得られます。
  - **削除ポリシー**：スケーリンググループがインスタンスを減らしたい、且つ複数の選択肢がある場合、削除ポリシーに応じてCVMを選択して削除します。通常は「最も古いCVMを削除する」を選択すればいいです。2つのポリシー[詳細](https://intl.cloud.tencent.com/document/product/377/4166)を確認してください。
  - **Cloud Load Balancer**：一つのCloud Load Balancerを指定します、スケールアウトされたCVMが自動的にこのCloud Load Balancerにマウントされます。

スケーリンググループとはすなわち作成完了されます。この時スケーリンググループはCVMを格納できるが、スマートなスケーリング機能はまだ付いてないです。次に、下記の3つの操作を続行することを強くお勧めします：
 - 既存のCVMに加入する
 - スケーリングポリシーを作成する
 - 通知を作成する

