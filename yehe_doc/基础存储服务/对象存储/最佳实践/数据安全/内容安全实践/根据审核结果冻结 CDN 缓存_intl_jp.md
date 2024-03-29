## 概要

コンテンツ審査機能は、自動凍結機能を提供し、不正ファイルを自動で凍結処理することができます。ただ、凍結するのはCloud Object Storage（COS）オリジンサーバーのデータに対してのみのため、CDNシナリオを使用しているユーザーは、CDNのキャッシュをタイムリーに処理することができません。

ここではServerless Cloud FunctionおよびAPI Gatewayの処理方式で、ユーザーのCDNのキャッシュがタイムリーに凍結できない問題を解決するサポートを提供します。

## 操作手順

1. [Tencent Cloud SCFコンソール](https://console.cloud.tencent.com/scf/list)にログインし、**関数サービス**ページで**新規作成**をクリックし、クラウド関数を作成します。
2. **最初から開始**を選択し、以下の基本設定を入力します。

 - 関数タイプ：「イベント関数」を選択します。
 - 関数名：関数の名称をカスタマイズします。
 - リージョン：使用する審査機能のバケットが所在しているリージョンを選択します。
 - 実行環境は、「Python2.7」を選択します。
3. 関数コードは以下のとおり設定します。
 - 送信方式：「ローカルからのzipパッケージをアップロード」あるいは「cosによるzipパッケージのアップロード」を選択します。zipパッケージは[ここをクリック](https://cos5.cloud.tencent.com/cosbrowser/code/scf/cos_audit_cdn_refresh.zip)からダウンロードできます。
 - 実行方法：index.main_handlerを入力します。
4. **高度な設定**をクリックし、**環境設定**を設定します。環境変数以外は、ニーズに応じてご自身で変更が可能です。
 - リソースタイプ：CPU
 - メモリ：512MB
 - 初期化タイムアウト時間：65
 - 実行タイムアウト時間：30
 - 環境変数：
    - CI_AUDITING_CALLBACK：コールバックアドレスです。ここでは従来のコンテンツ審査のコールバックで設定されているアドレスを入力します。コールバックアドレスを設定すればコールバックし、設定しなければコールバックしません。
    - CDN_URL：CDNアドレスです。入力必須です。CDNアドレスを設定し、CDNキャッシュをリフレッシュします。
    - REGION：リージョンです。入力必須です。bucket所在リージョンを設定します。
    - BUCKET_ID：バケットID(バケット名)です。入力必須です。バケットIDを設定します。バケットIDは画像スタイルの照会に用います。間違えて入力するとスタイルの照会がエラーになります。
    - IMAGE_STYLE_SEPARATORS：画像のスタイル区切り記号です。画像にリフレッシュスタイルが必要な場合は、この変数の設定が必要です。複数の区切り記号を連続入力します。区切る必要はありません。
    - CDN_REFRESH_TYPE：画像オブジェクトのキャッシュ更新方法です。デフォルトではurlに基づいてリフレッシュします。スタイルのみリフレッシュします。「path」を設定すると、画像処理パラメータがアクセスしたキャッシュをリフレッシュします。注意事項として、path方式のリフレッシュは、このファイル名よりもさらに長いファイル名を含むファイルを削除しますので、慎重に使用してください。
以上の環境変数について、キャッシュ更新が想定に合致するよう、以下の例のように、正しく入力されているかどうかを確認します。

5. 権限設定には「ロールの実行」にチェックを入れます。「実行ロールの新規作成」をクリックし、「カスタムロールの新規作成」ページへジャンプします。
6. ロールキャリアは「クラウド関数(scf)」を選択し、「次へ」をクリックします。

7. ロールポリシーの設定は、QcloudCDNFullAccessおよびQcloudCIReadOnlyAccessを選択し、「次へ」をクリックします。
8. ロールに名前を付けたら、「完了」をクリックします。
9. ロールのカスタマイズ作成が完了したら、クラウド関数作成ページに戻ります。ロールのドロップダウンリストを更新し、先ほど作成したロールを選択します。
10. 上記ステップ完了後、「完了」をクリックし、クラウド関数を作成します。
11. [API Gatewayコンソール](https://console.cloud.tencent.com/apigateway/service)に再度進み、API Gatewayサービスをアクティブにします。
12. [バックエンドを作成してSCFにアクセスするAPI](https://intl.cloud.tencent.com/document/product/628/39486) を参考にして、作成を完了できます。
13. パブリッシュ環境で「リリース」を選択し、「リリースサービス」をクリックします。
14. Cloud Infiniteの「コンテンツ審査」ページで、画像あるいはその他ターゲットタイプについてコールバックパラメータを設定します。コールバックURLは、前のステップで作成したAPI Gatewayのアドレスを設定します。
15. コールバックの設定完了後、CDNのリソースは自動で審査コールバックの結果に基づき、キャッシュを更新します。
