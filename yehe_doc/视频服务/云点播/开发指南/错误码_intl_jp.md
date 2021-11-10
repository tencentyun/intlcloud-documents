## エラーコードリスト
### ビデオ処理エラーコード

| エラーコード | 意味 |
| -- | -- |
| InvalidInput | 入力パラメータが不正のため、入力パラメータをチェックしてください。 |
| InvalidInput.InvalidTimeOffset | 入力パラメータが不正：指定されたタイムポイントが不正です。 |
| InvalidInput.DefinitionNotExist | 入力パラメータが不正：指定されたテンプレートIDが存在しません。 |
|InvalidInput.ConfigurationUnsupported|入力パラメータが不正：無効な設定。以下を含むがこれらに限定されない：<li>ユーザーが未登録。</li><li>入力パラメータ値が不正（形式、値の範囲など）。</li><li>パラメータテンプレートの設定に問題があります。</li><li>ビデオ処理タスクを指定しません。</li>|
|InvalidInput.TaskDuplicated|入力パラメータ値が不正：重複するタスクが存在します。 |
|InvalidInput.PermissionDenied|入力パラメータ値が不正：権限がありません。この製品を使う権限を申請してください|
|InvalidInput.ResultFileSizeTooLarge|入力パラメータ値が不正：ファイルサイズが大きすぎます。|
| SourceFileError | ソースファイルエラー：ビデオデータが破損など、ソースファイルが正常かどうか確認してください。 |
| SourceFileError.NoVideoMedia | ソースファイルエラー：ビデオトラック画面がありません。 |
| SourceFileError.NoVideoResolution | ソースファイルエラー：ソースファイルの解像度を取得できません。 |
|SourceFileError.ContentMalformed|ソースファイルエラー：入力内容（ファイルが存在しない、ファイルが破損している、メディアファイルをデコードできないなど）が正しくありません。|
|SourceFileError.ContentUnsupported|ソースファイルエラー：入力形式（サポートされていないファイル形式、ファイルサイズ、ファイル期間など）が正しくありません。|
|SourceFileError.DownloadNotAccessible|ソースファイルエラー：入力ファイルをダウンロードしようとすると、これらのファイルにアクセスできません。ソースの可用性を確認してください。|
| InternalError | 内部サービスエラーのため、リトライをお勧めします。 |
