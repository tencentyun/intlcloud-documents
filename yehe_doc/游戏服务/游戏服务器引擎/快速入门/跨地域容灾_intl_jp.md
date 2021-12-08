## 操作シナリオ

このドキュメントで、ゲームサーバーキューを通じたクロスリージョン災害復帰機能の実現について主にガイドします。


## 前提条件 

- 上海とシリコンバレーの2個のサーバーフリートを作成します。操作手順：
  - [ビギナー向け例](https://intl.cloud.tencent.com/document/product/1055/37401) 操作完了までの最初の3つの手順：**ワンクリックでデモパッケージをアップロード**、**ワンクリックでサーバーフリートを作成**、**ゲームサーバーセッションの作成**をクリックし、最後に**完了**をクリックします。
- サーバーフリート1作成済み（上海地区）。
![](https://main.qcloudimg.com/raw/7726bf7876142b7b1e7ed626e2cd2f46.png)
- サーバーフリート2作成済み（米国地区）。
![](https://main.qcloudimg.com/raw/5881c69ab304675cf86c741364a5502b.png)

## 操作手順

### ゲームサーバーキューの作成

1. [GSEコンソール](https://console.cloud.tencent.com/gse)にログインし、左側のメニュー**ゲームサーバーキュー**をクリックして、ゲームサーバーキューページに入ります。
2. 左上のサービス地域を選択して、**新規作成**をクリックします。
3. ゲームサーバーキューの新規作成ページに入り、基本情報を記入します。
   - 識別子：有効な識別子を入力します。アルファベットのみが有効です。この例では「disasterrecovery」と記入します。
   - タイムアウト時間をアサイン：ゲームサーバーセッションリクエストが複数エリアで待機できる最長時間を入力します。最大値は600秒です。この例では30秒で構成します。
4. ディレーポリシーを記入 
  - 残りのタイムアウト時間（30s）ですべてのプレイヤーとの遅れが150ms内のサーバーフリートを検出します。
5. ターゲットが作成済みのサーバーフリート1（上海地区）とサーバーフリート2（米国地区）を選択します。
6. **確定**をクリックすると、ゲームサーバーキューの作成が完了します。
![](https://main.qcloudimg.com/raw/5499f546232f016127e201c6ce40f871.png)


### 不具合がない場合、サーバーアドレスをリクエストします

「ゲームサーバーセッション配置開始」TencentCloud APIを通じて、ゲームサーバーセッションをサーバーフリートのプロセスに配置します。コードの中でTencentCloud APIを呼び出します。この例では [TencentCloud APIデバッグ](https://console.cloud.tencent.com/api/explorer?Product=gse&Version=2019-11-12&Action=StartGameServerSessionPlacement&SignVersion=) を通じてショートカットで作成します。
>?パラメータ説明の入力：
>- Regionは地域です。この例では「華東地区（上海）」を選択します。
>- PlacementIdはゲームサーバーセッションのデプロイを開始する唯一の識別子です。この例では1と記入します。
>- GameServerSessionQueueNameはゲームサーバーセッションキューの名称です。この例では「disasterrecovery」と記入します。
>- MaximumPlayerSessionCountはゲームサーバーセッションに同時に接続できる最大プレイヤー数です。この例では2を記入します。
>- DesiredPlayerSessions.Nはプレイヤーのゲームセッション情報です。このうちPlayerIdは、プレイヤーセッションと関連付ける唯一のプレイヤーマークです。この例では2セットを追加し、それぞれ1、2と記入します。
>- PlayerLatencies.Nはプレイヤーのディレーです。このうちPlayerIdはプレイヤーID、RegionIdentifierはディレーに関わるエリアの名称、LatencyInMillisecondsはミリ秒レベルのディレーのことです。この例では4セットを追加します。それぞれ[1，ap-shanghai，100]、[1，na-siliconvalley，50]、[2，ap-shanghai，60]、[2，na-siliconvalley，80]を記入します。

![](https://main.qcloudimg.com/raw/bf528fd7700938e035cbe7ccd201954c.png)
![](https://main.qcloudimg.com/raw/29baaa97fb0e6a3e20a2f9b53f0a5bdd.png)
![](https://main.qcloudimg.com/raw/0327f3c13ce77d07af24e6fc5a417f59.png)
**ディレーポリシースケジューリング結果評価：**
プレイヤー2人が目標アドレスに到達するまでのディレー状況

- player1のディレーは、上海までは100ms、シリコンバレーまでは50msです。
- player2のディレーは、上海までは60ms、シリコンバレーまでは80msです。
ディレーポリシーは、すべてのプレイヤーのディレーが150ms内のサーバーを検出するよう構成され、シリコンバレーと上海が要件を満たします。このため、ゲームサーバーセッションは優先順位が高いサーバーフリート1（上海地区）に自動で作成されます。
![](https://main.qcloudimg.com/raw/7a1a2d5bbb156d6dd99e29abd3cb8821.png)

### 不具合時の自動災害復帰

今、上海で不具合が発生した場合、上海の速度は測定できません。
>?パラメータ説明の入力： 
  - PlayerLatencies.Nはプレイヤーのディレーです。このうち、PlayerIdはプレイヤーID、RegionIdentifierはディレーに関わるエリアの名称、LatencyInMillisecondsはミリ秒レベルのディレーのことです。この例では4セットを追加します。それぞれ[1，ap-shanghai，0]、[1，na-siliconvalley，50]、[2，ap-shanghai，0]、[2，na-siliconvalley，80]を記入します。速度の測定ができない条件を設定する場合、ディレーを0や無限大を記入するか、記入しないものとします。この例では上海までのディレー0を入力します。
  - その他パラメータの入力については、上で入力したものと統一させます。

![](https://main.qcloudimg.com/raw/bf528fd7700938e035cbe7ccd201954c.png)
![](https://main.qcloudimg.com/raw/e6b46c5b84adb4dea5e8da0613eb8bc2.png)
![](https://main.qcloudimg.com/raw/482798618d6366bd186a726364d7a831.png)


**ディレーポリシースケジューリング結果評価：**
プレイヤー2人が目標アドレスに到達するまでのディレー状況
- player1のディレーは、上海までは0ms、シリコンバレーまでは50msです。
- player2のディレーは、上海までは0ms、シリコンバレーまでは80msです。

上海のディレーが0msと表示されるのは、上海で不具合が発生し、ディレーを測定できなかったためです。このためゲームサーバーセッションは、米国エリアのサーバーフリート2に作成されます。
![](https://main.qcloudimg.com/raw/eccba22674c685285bb94220bd9b407c.png)

### 不具合時の手動災害復帰

ある地域で不具合が発生し、ゲームサーバーセッションキューのターゲットリストから、この不具合エリアのサーバーフリートを手動で削除する必要がある場合、GSEは、ゲームサーバーセッションをターゲットリストの残りのサーバーフリートにスケジューリングします。
![](https://main.qcloudimg.com/raw/94c558e6fa2df116135e8d0017bb19b2.png)

