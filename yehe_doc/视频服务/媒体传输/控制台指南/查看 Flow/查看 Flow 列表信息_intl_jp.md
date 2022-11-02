## 概要
Tencent CloudのStreamLinkは、安全かつ安定的なリアルタイム伝送機能を提供し、ビデオストリームメディアを高速、低遅延、安定的に伝送するという動画サプライヤーのニーズを満たします。StreamLinkコンソールはストリームディメンションをベースとして管理され、各ストリームはそれぞれ1つのストリームの送信リンクに対応しています。StreamLinkコンソールをベースとして、ビデオストリームを迅速かつ安定的に送信できると同時に、送信プロセスにおけるビデオストリームの品質をオールラウンドにモニタリングすることができます。

## Flowリスト情報の確認
StreamLinkコンソールは、Flowディメンションをベースとして管理されます。各Flowは、1つのCSSストリームを伝送し、複数のリージョンに渡し、複数のプルアドレスを提供できます。コンソールの[Flow Management](https://console.tencentcloud.com/mdc/flow)で、すべてのFlowを管理できます。このページから、Flowの追加、確認、編集、削除、操作の開始と停止を行うことができます。

![](https://qcloudimg.tencent-cloud.cn/raw/afd0fc995dafc79a23feb9ba2df91dae.jpg)

図のように、**Flow**リストには、各Flowの簡単な情報が表示されています。
- **ステータス Status**：IDLEは未起動、RUNNINGはFlowが起動していることを示します。
- **プロトコル Source Protocol**：Inputのプッシュプロトコルです。
- **アドレス Input Address**：Inputのプッシュアドレスです。
Flowが停止しているときのみ、Flowのフル編集操作を行うことができます。Flowが停止していない場合、ホワイトリストの編集、既存のOutput設定の削除または新しいOutput設定の作成のみが可能です。