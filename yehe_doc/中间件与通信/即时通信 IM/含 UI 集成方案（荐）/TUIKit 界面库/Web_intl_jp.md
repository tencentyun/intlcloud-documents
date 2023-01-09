# Web

## chat-uikit-reactの紹介
chat-uikit-reactはTencent Cloud IM SDKをベースにしたUIコンポーネントライブラリであり、汎用UIコンポーネント及び会話、チャット、リレーションシップチェーン、グループ、オーディオビデオ通話などの機能を提供します。
UIコンポーネントを使用すれば、自分の業務ロジックを積み木を組み合わせるように素早く構築できます。
chat-uikit-reactが提供したコンポーネントは、UI機能を実装すると同時に、IM SDKに応じてインスタンスを呼出して、IMに関するロジックとデータ処理も実装します。そのため、開発者がchat-uikit-reactを使用する時、自分の業務とカスタム拡張だけに集中するだけです。

## chat-uikit-reactの構成
chat-uikit-reactは主にTUIKit、TUIConversation、TUIChat、TUIManageモジュールから構成されます。個々のモジュールは異なる役割を果たします。

## TUIKitの機能紹介
一番外側のProviderとして、TUIKitはContextを介してtim、conversation、profileなどの豊富なコンテンツを提供します。詳しくは、[オープンソースコード](!https://github.com/TencentCloud/chat-uikit-react)をご参照ください。

## TUIConversationの機能紹介
TUIConversationは会話リストの表示と編集を実装し、会話のピンマークや削除などの機能を提供します。

## TUIChatの機能紹介
TUIChatは会話メッセージの表示と編集を実装し、メッセージの送信、取消し、転送などの機能を提供します。

## TUIManageの機能紹介
TUIManageは会話に関するメッセージの表示、会話のピンマークや削除などの処理を実装します。
