### DynamoDBクラスタの紹介
DynamoDBは、ドキュメントとキー値ストレージモデルをサポートしているテーブルディメンションベースでスケーラビリティの高いNoSQLデータベースサービスです。TencentDBチームは、既存のNoSQLモジュールフレームワークに基づいて、DynamoDBプロトコルとの互換性が高く、パフォーマンスが高速で安定して、インスタンスレベルのバックアップとロールバックをサポートして、自動防災メカニズムを備えた新しいデータベースサービスを導入しました。DynamoDBの開発愛好家であれば、あまりコードを変更する必要がなくて、DynamoDBプロトコルを介してデータベースにアクセスできます。


### DynamoDBクラスタの作成
MongoDB[購入ページ](https://buy.cloud.tencent.com/mongodb?clusterType=1)に移動し、【シャードクラスタ】をクリックして、プロトコルタイプで「DynamoDBプロトコル」を選択します。
最下層も、データを複数の物理マシンに分散することによって、ストレージ容量のスムーズな拡大を実現します。そのため、必要に応じて、シャード数、シャード内のノード数、およびノード仕様も選択する必要があります。各シャードはマルチノードのレプリカセットであり、シャード内のマルチノードが自動防災で、サービスの高可用性を保証します。
[![](https://mc.qcloudimg.com/static/img/70d51b1da13f7334b54f14612b26c05c/create.png)](https://mc.qcloudimg.com/static/img/70d51b1da13f7334b54f14612b26c05c/create.png)

### コンソール管理
コンソールで、ノードの構成、ノードの仕様、使用容量などのDynamoDBクラスタインスタンスの詳細情報を確認できます。同時に、コンソールでインスタンスの更新管理と容量拡張などの操作を実行することもできます。
[![](https://mc.qcloudimg.com/static/img/c101b8878cb77a9e486ed5e34467a995/D.png)](https://mc.qcloudimg.com/static/img/c101b8878cb77a9e486ed5e34467a995/D.png)

###　容量拡張操作
現在、DynamoDBクラスタの容量拡張モードはすべてのノードの統合された容量拡張のみをサポートしており、ノードの追加による容量拡張はサポートされていません。インスタンスリストページの「容量拡張」ボタンをクリックし、拡張する容量仕様を選択して【アップグレード】をクリックします。
[![](https://mc.qcloudimg.com/static/img/eac99761afe97e60a18438f5ef196e14/kuo.png)](https://mc.qcloudimg.com/static/img/eac99761afe97e60a18438f5ef196e14/kuo.png)


###　バックアップとロールバック
現在、インスタンスレベルのバックアップとロールバックのみサポートしていますので、インスタンス詳細ページの【バックアップ】ボタンをクリックしてコメント情報を入力した後、【提出】をクリックしてインスタンスバックアップを実行します。
[![](https://mc.qcloudimg.com/static/img/608e4ec72a25d7a265d07d2720c5d1ef/beifeng.png)](https://mc.qcloudimg.com/static/img/608e4ec72a25d7a265d07d2720c5d1ef/beifeng.png)
ロールバック操作中に、ロールバックの日付を入力する必要があります。現在は5日以内の任意時間のロールバックをサポートしていますが、前提として、2つのバックアップ間の時点だけを選択してロールバックできます。満足するバックアップがない場合は、手動バックアップを1回実行してください。
[![](https://mc.qcloudimg.com/static/img/b2ef79e419a89976c96743aa7e4f6085/huidang.png)](https://mc.qcloudimg.com/static/img/b2ef79e419a89976c96743aa7e4f6085/huidang.png)

###　インスタンス監視
インスタンスは3つのディメンションの監視メトリックを提供します。インスタンスディメンション、シャードディメンション、およびノードディメンションは、クラスタ全体のデータ監視に使用されます。操作リクエスト、容量使用、および負荷などの複数のメトリックに関する監視データを提供します。
[![](https://mc.qcloudimg.com/static/img/98766957d1748618dad40f133c0b35d2/jiank2.png)](https://mc.qcloudimg.com/static/img/98766957d1748618dad40f133c0b35d2/jiank2.png)

