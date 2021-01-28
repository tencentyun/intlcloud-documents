TRTCコンソールでは、オンラインでの署名（UserSig）生成をサポートしていますが、このUserSigは開発段階のクイックテストにのみ使用されます。正式なサービス開始前に、UserSig計算ロジックを[バックエンドサーバーに移行](https://intl.cloud.tencent.com/document/product/647/35166)し、暗号化キーの漏洩によるトラフィックの盗用を回避してください。

<span id="generate"></span>

## 署名（UserSig）生成ツール
開発者とTencent Cloudサービスとは、署名（UserSig）検証を通じて信頼関係が確立されます。

1. TRTCコンソールに入り、左側のバーの【開発支援ツール】>【[UserSigの生成&検証](https://console.cloud.tencent.com/trtc/usersigtool)】を選択して、【署名(UserSig)生成ツール】コンポーネントを確認してください。
2. ドロップダウンリストをクリックして作成済のアプリケーション（SDKAppID）を選択します。完了すると対応するキー（Key）が自動生成されます。
3. ユーザー名（UserID）を入力します。
3. 【署名（UserSig）生成】をクリックして、対応する署名（UserSig）を生成します。


<span id="check"></span>

## 署名（UserSig）検証ツール
このツールを使用して署名（UserSig）の有効性を確認します。

>! 使用時は、検証をリクエストする時に入力するSDKAppID、UserIDがUserSigのSDKAppID、UserIDと一致していることを確認してください。

1. TRTCコンソールに入り、左側のバーの【開発支援ツール】>【[UserSigの生成&検証](https://console.cloud.tencent.com/trtc/usersigtool)】を選択して、【署名(UserSig)検証ツール】コンポーネントを確認します。
2. 検証したいアプリケーション（SDKAppID）を選択します。完了すると対応するキー（Key）が自動生成されます。
3. ユーザー名（UserID）を入力します。
4. 検証したい署名（UserSig）をコピーして、【署名(UserSig)】の中にペーストし、【検証開始】をクリックします。
>? 【署名(UserSig)生成ツール】コンポーネントの中で生成したUserSigである場合、【署名（UserSig）のコピー】をクリックしてコピーすることを推奨します。
>
5. 検証の完了後、下側の検証結果を確認できます。
	- 検証成功のサンプル：
	- 検証失敗のサンプル：


## 関連資料
その他のUserSigに関するご質問は、 [UserSigに関するご質問](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。
