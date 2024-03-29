## 一般的な質問

### Androidのsoライブラリはx86_64バージョンが提供されていますか？
提供されていません。

### GMEをホットアップデートするときの注意事項は何ですか？

GME SDKをホットアップデートするとき、SDKに依存するモジュールも一緒に更新する必要があります。GME関連のソースコードを全部ホットアップデートの対象とすればよいです。

### どのようなゲームシーンでリアルタイム音声サービスを活用できますか？

大きく分けて以下の3つあります：
- **マイクシーケンスモード：**ユーザ達が交互にマイクを使用するモード。音質が良く音が途切れないため、人狼ゲームなどのボイスゲームに適します。
- **自由通話モード：**超低遅延で複数人の同時通話をサポートします。複数人からなるチームによる競技ゲームに適します。
- **コマンドモード：**複数人を指揮する作戦ゲームやキャスターとの音声ゲームプレイインタラクションなど、大規模国戦ゲームに適します。

Tencent Cloud SDKが提供するルーム内通話は上記のシーンに対応できます。具体的なモードは製品に対するユーザ要件であり、お客様のAppでの処理がより柔軟です。例えば、製品レイヤーからプロトコルを配布しユーザにマイクオンしてもらうことができます。

## 重要インターフェースに関する質問

### 初期化時にエラーコード7015が返されました。どうすればいいですか？

- 開発時にこのエラーが発生した場合、SDKファイルは全部同じバージョンか、SDKはアップデートされたか、SDKアップデート時にフルアップデートされているかをチェックしてください。
- 実行可能なファイルをエクスポートした後このエラーが発生した場合、エラーを無視してください。これは、Unityのパッケージングプログラムとサードパーティのセキュリティ強化プログラムがSDKファイルのmd5を変更したことが、エラーの発生原因かもしれないからです。 

### OpenIdの値には要件がありますか？

現在、OpenIdは64ビットの符号なし整数型だけをサポートします。string型に変換してSDKに渡してください。

### 同じOpenIdで同時に複数のルームに参加することはできますか？

できません。1つのOpenIdは同時に1つのルームにしか参加できません。

### GME SDK中のPoll関数を呼び出すタイミングは？

SDKを初期化した後、定期的にPoll関数を呼び出してください。

### イベントを発生させるには定期的にPoll関数を呼び出す必要がありますが、新しいスレッドを起動し、定例的に喚起してPoll関数を呼び出してもよいですか？

論理上では、当社のインターフェースの呼び出し元は同一スレッドでなければなりません。呼び出し元をサブスレッドにした場合、すべての呼び出し元をそのサブスレッドにしなければなりません（特にInit関数とPoll関数）。

### Poll関数を呼び出す頻度は？

特別なニーズがない場合、Demoに示しているサンプルソースコードを参考にして呼び出してください。1/30秒ごとに1回呼び出すことをお勧めします（DemoのEnginePollHelper.mをご参照ください）。

### 録音が完了する前に定時的にPoll関数を呼び出すと、画面が動かなくなりました。これはなぜでしょうか？

Poll関数がメインスレッドによって呼び出されているかを確認してください。

### ボイスルームを退出するとき、初期化を解除する必要がありますか?

ありません。SDKを使用しないとき、または、アカウントを切り替えるときこそ、初期化を解除してください。
