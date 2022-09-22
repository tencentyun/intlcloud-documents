StreamLiveでは、チャネルの実行中にチャネルのイベントを処理できます。具体的な方法としては、プランをチャネルに関連付けて実行時間と実行イベントを設定し、この実行時点でチャネルはイベントの実行を開始します。

## イベントの表示
**Channel Management**から、Planを設定する必要があるチャネルを選択し、チャネル名をクリックしてチャネル詳細ページに入り、詳細ページの**Plan**タブページを選択すると、現在のチャネルの下の**Plan**リストが表示されます：
![](https://qcloudimg.tencent-cloud.cn/raw/1dd3eebf1e4e7714c29a1302d65a514b.png)
![](https://qcloudimg.tencent-cloud.cn/raw/907a629dac8736d4780d411f2988d33f.png)

## イベントの作成
ページの左上隅にある**Create Event**をクリックして、新しいイベントを作成します。現在サポートされているイベントタイプは次のとおりです：
- Input Switch：実行中のチャネルの場合、受信中の入力を切り替えます。
- Time Record：  実行中のチャネルの場合、時間帯ごとのレコーディングを実行します。

### 入力切り替えタイプのイベントの作成
<img src="https://qcloudimg.tencent-cloud.cn/raw/8136ad53ef809a22070e80f29a86cf84.png" style="zoom:80%;" />

- **Event Type**：Input Switchを選択します。
- **Input Attachment**：チャネルにバインディングされており、切り替えしたいInput名を選択します。
- **Event Name**：イベント名を入力します。数字、アンダーバー、大文字と小文字をサポートできます。最大長は32文字です。このチャネルでイベント名を繰り返すことはできません。
- **Start Type**：Fixed TimeまたはImmediateを選択できます。Fixed Time：UTC時間で指定された特定の時刻にイベントを実行します。指定された時間は、イベント開始の少なくとも10秒前で、現在の時刻よりも前であってはなりません。Immediate：設定したイベントをすぐ実行します。

### 時間指定レコーディングタイプのイベントの作成
<img src="https://qcloudimg.tencent-cloud.cn/raw/395c7b5bc4023a9160ada53913eea58c.png" style="zoom:80%;" />

- **Event Type**：Time Recordを選択します。
- **Event Name**：イベント名を入力します。数字、アンダーバー、大文字と小文字をサポートできます。最大長は32文字です。このチャネルでイベント名を繰り返すことはできません。
- **OutputGroupName**：レコーディングの必要があるOutputGroup名を選択します。具体的な名は、Output Group Settingページで確認できます。
- **ManifestName**：レコーディングして生成したMainfestファイル名を入力します。m3u8またはmpdサフィックスを入力する必要はありません。
- **DestinationUrl**：保存の必要があるファイルのCOSアドレスを入力します。
- **Timing**：レコーディングの時間帯を選択します。この時間はUTC時間です。

## イベントの削除
削除の必要がるイベントを選択し、イベントの最も右端にある**Operation**で**Delete**ボタンをクリックし、ポップアップ確認ボックスで**Confirm**をクリックしてイベントを削除できます。実行中のイベントは削除できません。削除できるのは、開始前または実行済みのイベントのみです。
![](https://qcloudimg.tencent-cloud.cn/raw/dae329be1090cbeb1b1705fe98fdef3d.png)