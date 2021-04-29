## ポリシーの作成
プロジェクトレベルの権限付与操作を細分化したい場合は（例えばデータのクエリー、更新とホットスタンバイ、ドメイン名管理操作を異なるサブアカウントに権限を付与する）、下記手順に従いポリシーを作成します。
1.  [アクセス管理コンソール](https://console.cloud.tencent.com/cam/overview) にログインし、左側のナビゲーションメニューバーで【Policies】をクリックします。
2. 【Create Custom Policy】をクリックして、【Create by Product Feature or Project Permission】を選択します。
![](https://main.qcloudimg.com/raw/59c8c89263412208344bd071430db23d.png)
3. 画面の指示に従ってポリシー名を入力し、下のサービスタイプで【CDN】を選択します。
![](https://main.qcloudimg.com/raw/e057955abd823f0b92ff6cc13a016c4c.png)
4. 必要に応じ、権限を付与する必要がある操作セットを有効にして、プロジェクトに関連付けます（デフォルトのプロジェクトに権限を付与できない）。次に、サブユーザーに関連付けます。
![](https://main.qcloudimg.com/raw/961dfce5817ba690b554f12dfa22d7c9.png)

## リソースレベル&プロジェクトレベル
現在、操作セットのカテゴリ及び対応するOPEN API2.0とOPEN API3.0インターフェースは下記の通りです。操作セット権限を持つサブユーザーは、権限を持つプロジェクトの任意ドメイン名に対し、次のリストにある2.0または3.0 APIを呼び出すことができます。

| 権限セット              | API2.0                                                       | API3.0                                                       | 権限付与が必要か |
| :-------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------- |
| 消費データ及び統計量のクエリー  |  DescribeCdnHostInfo DescribeCdnHostDetailedInfo GetCdnStatusCode<br/>GetCdnStatTop<br/>GetCdnProvIspDetailStat | DescribeCdnData DescribeOriginData<br/>ListTopData<br/>DescribeIpVisit | はい           |
| ドメイン名情報のクエリー          | GetHostInfoById<br/>GetHostInfoByHost                        | DescribeDomains<br/>DescribeDomainsConfig                    | はい           |
| CDN ログダウンロードリンクのクエリー | GenerateLogList<br/>GetCdnLogList                            | DescribeCdnDomainLogs                                        | はい           |
| ドメイン名の追加              | AddCdnHost                                                   | AddCdnDomain                                                 | はい           |
| ドメイン名のオンライン/オフライン    | OnlineHost OfflineHost                                       | StartCdnDomain<br/>StopCdnDomain                             | はい           |
| ドメイン名の削除             | DeleteCdnHost                                                | DeleteCdnDomain                                              | はい           |
| ドメイン名設定の変更         | UpdateCdnConfig                                              | UpdateDomainConfig                                           |はい           |
|更新とホットスタンバイ             | RefreshCdnDir<br/>RefreshCdnUrl<br/>GetCdnRefreshLog<br/>CdnPusherV2<br/>GetPushLogs<br/>CdnOverseaPushser | PurgeUrlsCache<br/>PurgePathCache<br/>DescribePurgeTasks<br/>PushUrlsCache<br/>DescribePushTasks | はい           |
| サービスのクエリー              | QueryCdnIp（権限を付与する必要はありません）                                       | DescribeCdnIp                                                | はい           |

## コンソール権限
- 消費データ及び統計量のクエリー：ポリシーで【 View usage data and statistics】を有効にし、プロジェクトに関連付けられている場合、サブユーザーは、コンソールで下記モジュールの情報を確認することができます。
  - 概要ページ：データ表示モジュールのみ
  - 統計分析：リアルタイム監視
  - 統計分析：データ分析
  - ネットワーク全体のデータ監視
- ドメイン名情報のクエリー：ポリシーが【Query domain name information】を有効にし、プロジェクトに関連付けられている場合、コンソールの【ドメイン名管理】ページで権限を持つプロジェクトのドメイン名リスト及び詳細な設定情報をクエリーできます。
- CDNログのダウンロードリンクのクエリー：ポリシーが【Query a CDN log download link】を有効にし、プロジェクトに関連付けられている場合、サブユーザーは、コンソールの【Log Service】ページでログのダウンロードリンクをクエリーできます。
- ドメイン名の追加：ポリシーが【Add a domain】を有効にし、プロジェクトに関連付けられている場合、サブユーザーは指定されたプロジェクトにドメイン名を追加できます。
- ドメイン名のオンライン/オフライン ：ポリシーが【Launch/deactivate a domain name】を有効にし、プロジェクトに関連付けられている場合、サブユーザーは指定されたプロジェクトでアクセラレーションドメイン名をオンライン/オフラインできます。
- ドメイン名の削除：ポリシーが【Delete a domain name 】を有効にし、プロジェクトに関連付けられている場合、サブユーザーは指定されたプロジェクトのアクセラレーションドメイン名を削除できます。削除されたドメイン名はオフライン状態である必要があります。そのため、サブユーザーがオンライン状態であるドメイン名を削除するには、【Launch/deactivate a domain name】権限を有する必要があります。
- ドメイン名設定の変更：ポリシーが【Modify domain name configuration】を有効にし、プロジェクトに関連付けられている場合、サブユーザーは、指定されたプロジェクトのアクセラレーションドメイン名の設定を変更できます。
- 更新とホットスタンバイ：ポリシーが【Purge and prefetch 】を有効にし、プロジェクトに関連付けられている場合、サブユーザーは、【更新キャッシュ】ページで対応する更新、ホットスタンバイ（ホワイトリスト）タスクを送信し、ホットスタンバイタスクの実行状態を確認できます。
