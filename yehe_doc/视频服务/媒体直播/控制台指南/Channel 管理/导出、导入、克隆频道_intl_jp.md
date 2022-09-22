StreamLiveは、チャネル構成ファイルのエクスポート/インポートとチャネルのクローン機能により、チャネルの作成をすばやく完了する業務をサポートしています。

## チャネルのエクスポート
StreamLiveの**Channel Management**インターフェースには、作成したすべてのチャネルとその状態が表示されます。右側の**Export**ボタンをクリックすると、チャネル構成jsonファイルをすばやくエクスポートできます。
![](https://qcloudimg.tencent-cloud.cn/raw/df66d2e71c1dc9f54e3753eecbf1e12b.png)
![](https://qcloudimg.tencent-cloud.cn/raw/6c6402290ae2b5b9bfc987917f035941.png)

## チャネルのインポート
**Channel Management**インターフェースの**Create Channel**ボタンをクリックし、**Import Configuration** を選択し、チャネル構成のjsonファイルを選択し、jsonファイルを送信した後にチャネル編集状態に入り、通常の構成プロセスに従ってチャネルを保存して送信します。
![](https://qcloudimg.tencent-cloud.cn/raw/7bf6af58535a57e11a9f92339b8e5e34.png)
チャネルのインポート機能は、実際には簡単な入力プロセスです。インポートしたjsonファイルに基づいて**Basic Information**、**Output Group Setting**の2つの部分を迅速かつ自動的に入力されます。**Input Setting**部分は無視されるため、Inputを再度選択してください。

>! チャネルの編集時に新しい構成ファイルをインポートすると、元のチャネル構成情報が上書きされます。

## チャネルクローン
チャネルクローンの本質とは、特殊なチャネルのエクスポート/インポートのすばやい操作です。**Channel Management**インターフェースを開き、**Operation**の下の**Clone**をクリックすると、チャネルクローンの設定状態に進めます。
![](https://qcloudimg.tencent-cloud.cn/raw/27f233ac35cc1bd1316901ac7457ffa9.png)
このとき、チャネルはクローンされるチャネルの基本情報（**Input Setting**部分を除く）を自動的に入力し、通常の構成プロセスに従ってチャネルを保存して送信します。