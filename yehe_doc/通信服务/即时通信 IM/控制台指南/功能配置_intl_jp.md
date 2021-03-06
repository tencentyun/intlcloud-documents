## ログインとメッセージ
[IMコンソール](https://console.cloud.tencent.com/im)にログインし、対象のアプリケーションカードをクリックして、左側ナビゲーションバーで【機能設定】>【ログインとメッセージ】を選択すると、実際の業務応じて、ログインとメッセージに関する設定を管理することができます。

### ログインの設定
1. 【ログインとメッセージ】ページで、【ログイン設定】の右側にある【編集】をクリックします。
2. ポップアップ表示されたログイン設定ダイアログボックスで複数端末のログインタイプを選択し、Web端末の同時オンラインインスタンスの数を設定します。
 ![](https://main.qcloudimg.com/raw/9774753fc2c7f4d46f47d0573404bc32.png)
3. 【OK】をクリックして設定を保存します。

### メッセージ履歴の保存期間の設定
メッセージ履歴はデフォルトで7日間保存されます。**メッセージ履歴の保存期間の延長は、付加価値サービスです**。具体的な料金に関する説明については、 [課金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。設定を変更できるのは、暦月につき1回のみです。

1. 【ログインとメッセージ】ページで、【メッセージ履歴の保存期間の設定】の右側にある【編集】をクリックします。
2. ポップアップ表示されたメッセージ履歴の保存期間のダイアログボックスで、メッセージ履歴の保存期間の延長を設定します。
3. 【OK】をクリックして設定を保存すると、その設定は直ちに有効になります。

### メッセージ取り消しの設定
1. 【ログインとメッセージ】ページで、【メッセージ取り消しの設定】の右側にある【編集】をクリックします。
2. ポップアップ表示された【メッセージ取り消しの設定】ダイアログボックスで、メッセージを取り消せる時間の長さを設定します。
3. 【OK】をクリックして設定を保存します。

### ブラックリストチェック
【ログインとメッセージ】ページの【ブラックリストチェック】エリアで、メッセージの送信後に「メッセージを送信」の表示を有効または無効にできます。
- 有効：相手があなたのアカウントをブラックリストに追加している場合、相手にシングルチャットメッセージを送信すると、メッセージが正常に送信されたことを示す文言が表示されますが、実際には相手はそのメッセージを受信しません。デフォルトでは有効になっています。
- 無効：相手があなたのアカウントをブラックリストに追加している場合、相手にシングルチャットメッセージを送信すると、メッセージ送信が失敗したことを示す文言が表示されます。

### フレンドシップチェック
【ログインとメッセージ】ページの【フレンドシップチェック】エリアで、シングルチャットの送信のリレーションシップチェーンのオンまたはオフを選択することができます。
- 有効： シングルチャットを開始する前にフレンドシップがチェックされ、フレンド間でのみシングルチャットメッセージの送信が許可されます。あなたの知らない人があなたにシングルチャットメッセージを送信した場合、SDKは[エラーコード20009](https://intl.cloud.tencent.com/document/product/1047/34348)を受信します。
- 無効：シングルチャットを開始するときにフレンドシップをチェックしないため、ユーザーはフレンドや知らない人にもシングルチャットメッセージを送信できます。デフォルトでは無効になっています。

## ユーザーカカスタムフィールド
[IMコンソール](https://console.cloud.tencent.com/im)にログインし、対象のアプリケーションカードをクリックして、左側ナビゲーションバーで【機能設定】>【ユーザーカスタムフィールド】を選択すると、実際の業務に応じてユーザーカスタムフィールドを管理することができます。
>!最大20個のユーザーカスタムフィールドを追加することができます。設定すると、これらのフィールドを削除したり、名前やタイプを変更したりすることはできません。業務上の必要に応じてこのフィールドを適切に計画してください。

### ユーザーカスタムフィールドの追加

1. 【ユーザーカスタムフィールド】ページで、【ユーザーカスタムフィールドの追加】をクリックします。
2. ポップアップ表示されたユーザーカスタムフィールドのダイアログボックスで、カスタムフィールド名を入力し、フィールドタイプや読み取り・書き込み権限を設定します。
 >?
 >- フィールド名は必ずアルファベットにしてください。長さは8文字以下とします。
 >- 少なくとも1つの読み取り権限と1つの書き込み権限を設定する必要があります。
 >
 ![](https://main.qcloudimg.com/raw/95851bca861f45aed20c045a8d09928e.png)
3. 【OK】をクリックして設定を保存します。

### ユーザーカスタムフィールド権限の変更
1. 【ユーザーカスタムフィールド】ページで、対象のカスタムフィールドがある行の【権限の変更】をクリックします。
2. ポップアップ表示されたユーザーカスタムフィールドのダイアログボックスで、読み取り・書き込み権限を変更します。
 ![](https://main.qcloudimg.com/raw/01081d71fe7ec45b470a249d685696c1.png)
3. 【確定】をクリックして設定を保存します。

## フレンドカスタムフィールド
>!最大20個のフレンドカスタムフィールドを追加することができます。設定すると、これらのフィールドを削除したり、名前やタイプを変更したりすることはできません。業務上の必要に応じてこのフィールドを適切に計画してください。

1. [IMコンソール](https://console.cloud.tencent.com/im)にログインし、ターゲットのアプリケーションカードをクリックします。
2. 左側ナビゲーションバーで【機能設定】>【フレンドカスタムフィールド】を選択します。
3. 【フレンドカスタムフィールドの追加】をクリックします。
4. ポップアップ表示されたフレンドカスタムフィールドのダイアログボックスで、カスタムフィールド名を入力し、フィールドタイプを設定します。
 >?フィールド名は必ずアルファベットにしてください。長さは8文字以下とします。
 >
 ![](https://main.qcloudimg.com/raw/271b68191ae3b1acb28fcbb4f7fea63e.png)
5. 【OK】をクリックして設定を保存します。

## グループメンバーカスタムフィールド
[IMコンソール](https://console.cloud.tencent.com/im)にログインし、対象のアプリケーションカードをクリックして、左側ナビゲーションバーで【機能設定】>【グループメンバーカスタムフィールド】を選択すると、実際の業務に応じてグループメンバーカスタムフィールドを管理することができます。
>!最大5個のグループメンバーカスタムフィールドを追加することができます。このフィールドは削除できず、グループタイプとそれに対応する読み取り・書き込み権限のみを変更できます。業務上の必要に応じて、このフィールドを適切に計画してください。

### グループメンバーカスタムフィールドの追加
1. 【グループメンバーカスタムフィールド】ページで、【グループメンバーカスタムフィールドの追加】をクリックします。
2. ポップアップ表示されたグループメンバーカスタムフィールドのダイアログボックスに、フィールド名を入力し、グループタイプとそれに対応する読み取り・書き込み権限を設定します。
  >?
  >- フィールド名は、英数字およびアンダーバー(\_)のみで構成され、数字で始めることはできません。長さは16文字以下とします。
  >- グループメンバーカスタムフィールド名は、グループカスタムフィールド名と同じにすることはできません。
  >
 - 【グループタイプの追加】をクリックして、グループタイプのパラメータを追加することができます。グループタイプは重複できません。
 - 対象のグループタイプのパラメータがある行の【削除】をクリックすると、グループタイプのパラメータを削除することができます。少なくとも1つのグループタイプのパラメータを残す必要があります。
 ![](https://main.qcloudimg.com/raw/3b6bcff0f4156f2340f71d082a29ac45.png)
3. 【カスタムフィールドとグループタイプを追加した後は、タイプの読み取り・書き込み権限は変更できても、削除はできないことを了承します】にチェックを入れます。
4. 【OK】をクリックして設定を保存します。

### ググループメンバーカスタムフィールドの編集
1. 【グループメンバーカスタムフィールド】ページで、対象のグループメンバーカスタムフィールドがある行の【編集】をクリックします。
2. ポップアップ表示されたグループメンバーカスタムフィールドのダイアログボックスで、選択したグループタイプの読み取り・書き込み権限を変更するか、または【グループタイプの追加】をクリックしてグループタイプを追加し、パラメータを設定します。グループタイプは重複できません。
 ![](https://main.qcloudimg.com/raw/19532e3441d0de3a1b7c29e2fd0b4a4a.png)
3. 【カスタムフィールドとグループタイプを追加した後は、タイプの読み取り・書き込み権限は変更できても、削除はできないことを了承します】にチェックを入れます。
4. 【OK】をクリックして設定を保存します。


## グループカスタムフィールド
[IMコンソール](https://console.cloud.tencent.com/im)にログインし、対象のアプリケーションカードをクリックして、左側ナビゲーションバーで【機能設定】>【グループカスタムフィールド】を選択すると、実際の業務に応じてグループカスタムフィールドを管理することができます。
>!最大5個のグループカスタムフィールドを追加することができます。このフィールドは削除できず、グループタイプとそれに対応する読み取り・書き込み権限のみを変更できます。業務上の必要に応じて、このフィールドを適切に計画してください。

### グループカスタムフィールドの追加
1. 【グループカスタムフィールド】ページで、【グループカスタムフィールドの追加】をクリックします。
2. ポップアップ表示されたグループカスタムフィールドのダイアログボックスに、フィールド名を入力し、グループタイプとそれに対応する読み取り・書き込み権限を設定します。
  >?
  >- フィールド名は、英数字およびアンダーバー(\_)のみで構成され、数字で始めることはできません。長さは16文字以下とします。
  >- グループカスタムフィールド名は、グループメンバーカスタムフィールド名と同じにすることはできません。
  >
 - 【グループタイプの追加】をクリックして、グループタイプのパラメータを追加することができます。グループタイプは重複できません。
 - 対象のグループタイプのパラメータがある行の【削除】をクリックすると、グループタイプのパラメータを削除することができます。少なくとも1つのグループタイプのパラメータを残す必要があります。
 ![](https://main.qcloudimg.com/raw/b529d0ca03ea819db6e619f7e93e9b1e.png)
3. 【カスタムフィールドとグループタイプを追加した後は、タイプの読み取り・書き込み権限は変更できても、削除はできないことを了承します】にチェックを入れます。
4. 【OK】をクリックして設定を保存します。

### グループカスタムフィールドの編集
1. 【グループカスタムフィールド】ページで、対象のグループカスタムフィールドがある行の【編集】をクリックします。
2. ポップアップ表示されたグループカスタムフィールドのダイアログボックスで、選択したグループタイプの読み取り・書き込み権限を変更するか、または【グループタイプの追加】をクリックしてグループタイプを追加し、パラメータを設定します。グループタイプは重複できません。
 ![](https://main.qcloudimg.com/raw/7ff1658c9fdc8d58e92e378445d1192f.png)
3. 【カスタムフィールドとグループタイプを追加した後は、タイプの読み取り・書き込み権限は変更できても、削除はできないことを了承します】にチェックを入れます。
4. 【OK】をクリックして設定を保存します。

