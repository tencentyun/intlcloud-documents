VODのビデオに対して開始されるアップロード、削除、ビデオ処理などの操作は、すべてイベントと呼ぶことができます。イベントの実行は、完了するまでに時間がかかります。VODはイベントが終了すると、直ちにAppサービスに実行結果、つまりイベント通知を送信します。

VODは、次のタイプのイベント通知をサポートします。

<table>
    <tr>
        <th style="width:30%">
            カテゴリー
        </th>
        <th style="width:70%">
            イベント通知
        </th>
    </tr>
    <tr>
        <td rowspan=3>
            アップロード削除
        </td>
        <td>
				    <a href="https://intl.cloud.tencent.com/document/product/266/33950">ビデオアップロードの完了</a>
        </td>
		<tr>
        <td>
            <a href="https://intl.cloud.tencent.com/document/product/266/33951">URLからのビデオプルアップロードの完了</a>
        </td>
    </tr>
		<tr>
        <td>
            <a href="https://intl.cloud.tencent.com/document/product/266/33952">ビデオ削除の完了</a>
        </td>
    </tr>
    <tr>
        <td rowspan=4>
            ビデオ処理
        </td>
        <td>
            <a href="https://intl.cloud.tencent.com/document/product/266/33953">タスクフロー状態の変更</a>
        </td>
		<tr>
        <td>
            <a href="https://intl.cloud.tencent.com/document/product/266/33954">ビデオ編集の完了</a>
        </td>
    </tr>
		<tr>
        <td>
            <a href="https://intl.cloud.tencent.com/document/product/266/35571">ビデオ合成の完了</a>
        </td>
</table>

イベント通知方法には、「通常のコールバック」と「信頼できるコールバック」があります。 [VODコンソール](https://console.cloud.tencent.com/vod) にログインしてコールバックモードを設定し、コールバックを受信するイベントを設定します。具体的な操作については、 [コールバック設定](https://intl.cloud.tencent.com/document/product/266/14055) をご参照ください。

- 通常のコールバック：コンソールでコールバックURLを設定すると、システムはイベントの完了後にそのURLに対し、HTTPリクエストを送信します。リクエストボディには通知内容が含まれています。
- 信頼できるコールバック：イベントが完了した後、VODシステムは通知を組み込みのキューに入れ、AppサービスはサーバーAPIを介してキュー内の通知を消費します。



## 通常のコールバック

通常のコールバックは、Appサービスがイベント通知を受動的に受信するモードです。コールバックURLを設定し、通常のコールバックモードを選択すると、VODはイベントの完了後にコールバックURLへのコールバックを開始します。

VODが開始する通常のコールバックの形式はHTTPリクエストであり、リクエストボディはJSON形式です。コンテンツに EventHandle パラメータの[EventContentの構造](https://intl.cloud.tencent.com/document/product/266/34187#EventContent) は含まれません。
[タスクステータス変更通知](https://intl.cloud.tencent.com/document/product/266/33953)を例に取った場合、コールバックの`EventType`パラメータは`ProcedureStateChanged`であり、情報は`ProcedureStateChangeEvent`パラメータ（[ProcedureTask](https://intl.cloud.tencent.com/document/product/266/34187#ProcedureTask) 構造）によって表されます。

## 信頼できるコールバック
信頼できるコールバックは、Appサービスがイベント通知をVODに対してアクティブにプルするモードです。信頼できるコールバックモードを選択した場合、VODシステムはイベント通知をキューに入れ、AppサービスはサーバーAPIを介してキュー内のイベント通知を順番に消費します。
Appサービスは[プルイベント通知](https://intl.cloud.tencent.com/document/product/266/34183) APIを介してメッセージを取得した場合、[イベント通知の確認](https://intl.cloud.tencent.com/document/product/266/34184) APIを呼び出して確認する必要があります。メッセージは必ず確認された上でVODのキューから削除されるので、「信頼できるコールバック」は「通常のコールバック」よりもの信頼性が高くなります。**イベント通知の信頼性の高い要件では、「信頼できるコールバック」モードを使用することをお勧めします**。
