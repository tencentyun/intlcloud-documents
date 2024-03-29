## 概要

Cloud Object Storage（COS）のログストレージ機能を有効にすると、ログ分析機能が有効になり、発行されたログファイルに対してさらにデータ分析を行うことができます。ログ分析機能は、指定した期間のログファイルを集約して統計分析を行い、重要な指標を抽出してお客様が確認できるようにします。

##  前提条件

ログ分析機能を使用するには、まず[COSログストレージのアクティブ化](https://intl.cloud.tencent.com/document/product/436/17040)サービスを行ってから、ログ分析SCFを作成する必要があります。作成ガイドについては、[COSログ分析関数の追加](https://intl.cloud.tencent.com/document/product/436/45569)をご参照ください。

## 操作手順

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインします。
2. 左側ナビゲーションバーで**バケットリスト**をクリックし、バケットリスト管理ページに進みます。
3. ログ分析を行いたいバケットを見つけ、そのバケット名をクリックし、バケット管理ページに進みます。
4. 左側ナビゲーションバーで、**ログ管理**を選択し、**ログストレージ**をクリックします。
>! ログ分析機能を使用するには、まずログストレージサービスをアクティブ化する必要があります。[ログ管理の設定](https://intl.cloud.tencent.com/document/product/436/17040)を参照して、ログストレージサービスを有効にしてください。
>
5. すでにCOSログ分析関数を追加している場合は、下のCOSログ分析セクションの**今すぐ使用**をクリックしてください。この時点でシステムが、COSログ分析関数ルールが追加されたかどうかチェックします。
COSログ分析機能を追加していない場合は、[COSログ分析関数の追加](https://intl.cloud.tencent.com/document/product/436/45569)を参照して関数を追加してください。
6. COSログ分析関数の追加が完了した後、このページで対応する関数名を選択し、分析したいログの時間帯を選択して、**分析タスクの作成**をクリックし、ポップアップウィンドウで以下の情報を設定します。 

 - **時間範囲**：分析したいログの時間帯です。**リクエスト終了時間**をもとに検索を行い、最大30日間をサポートします。指定された時間帯のログファイルの合計サイズは200GB以下とします。
 - **SCFの選択**：現在のバケットが配置されているリージョンに追加されたCOSログ分析関数を選択します。
 - **プロダクト配布ディレクトリ**：ログ分析後、システムは分析結果のプロダクトをパッケージ化し、お客様が指定した配布ディレクトリに保存します。プロダクトには、**結果ファイル**と**リストファイル**が含まれます。**結果ファイル**は、お客様が選択した分析シナリオに従って分析した後に得られた結果です。**リストファイル**は、この分析と検索により得られたログファイルのリストのことです。
 - **シナリオの選択**：現在サポートされているログ分析シナリオです。
 - **Nの値**：シナリオにおいて対応するNの値で、正の整数を入力してください。
 - **タスク説明**：この分析に関する説明情報をカスタマイズすることができます。
7. 設定が正しいことを確認し、**確定**をクリックすると、分析タスクが追加されたことを確認できます。

   作成された分析タスクに対しては、次のような操作が可能です。
 - **結果の確認**をクリックすると、このログ分析の結果と結果ファイルの保存先アドレスが確認できます。
>! 
>- 直近3日間に作成されたログ分析タスクを照会することができます。
>- 結果の確認には、ログ分析タスクの実行が終了するのを待つ必要があります。ログ分析は、ログサイズに応じて、通常、数分から数十分かかります。
 - **実行ログ**をクリックして、SCFコンソールにジャンプし、COSログ分析の実行ログを確認します。
