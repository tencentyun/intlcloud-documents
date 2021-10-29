Video on Demandは、2019年にイベント通知形式を改訂しました。
- 改訂後、新規登録ユーザーのイベント通知形式はバージョン3.0（現行形式）になりました。
- 改訂前に登録した一部のユーザーは、2.0バージョン（旧形式）を依然として使用している可能性があります。

このドキュメントは、2.0形式と3.0形式のイベント通知の比較対照表を提供することを目的としています。このドキュメントをお読みになる前に、あらかじめコンソールにログインし、【クラウド製品】>【VOD】>[【コールバック設定】](https://console.cloud.tencent.com/vod/callback)を選択してから、このページをご確認ください。
- 【コールバックURL】のみが表示されている場合は、通常のコールバックがデフォルトですでに3.0形式になっていることを意味しますので、このドキュメントをお読みになる必要はありません。
- 【2.0コールバックURL】と【3.0コールバックURL】の両方が同時に表示される場合は、2.0形式の通常のコールバックを使用していることを意味しますので、**続けて下記の内容をお読みください**。

>!2.0形式の通常のコールバックをまだ使用している場合は、使用しているイベント通知のバージョンを3.0形式へ徐々に移行することをお勧めします。2.0形式のイベント通知のドキュメントは、今後メンテナンスが行われなくなります。

**3.0形式と2.0形式のイベント通知の比較対照表は、**次のとおりです。

| イベント通知 | 3.0形式 | 2.0形式 |
| -- | -- | -- |
| ビデオアップロードの完了| [リンク](https://intl.cloud.tencent.com/document/product/266/33950) | [リンク](#NewFileUpload) |
| URLからのビデオプルアップロードの完了 | [リンク](https://intl.cloud.tencent.com/document/product/266/33951) | [リンク](#PullComplete) |
| ビデオ削除の完了 | [リンク](https://intl.cloud.tencent.com/document/product/266/33952) | [リンク](#FileDeleted) |
| タスクフローステータスの変更 | [リンク](https://intl.cloud.tencent.com/document/product/266/33953) | [リンク](#ProcedureStateChanged) |
| ビデオ編集の完了 | [リンク](https://intl.cloud.tencent.com/document/product/266/33954) | - |
| ビデオトランスコードの完了 | [リンク](https://intl.cloud.tencent.com/document/product/266/33957) | [リンク](#TranscodeComplete) |
| 指定タイムポイントスクリーンキャプチャの完了| [リンク](https://intl.cloud.tencent.com/document/product/266/33958) | [リンク](#CreateSnapshotByTimeOffsetComplete) |
| ビデオキャプチャスプライトイメージの完了 | [リンク](https://intl.cloud.tencent.com/document/product/266/33959) | [リンク](#CreateImageSpriteComplete) |
| ビデオトリミングの完了 | [リンク](https://intl.cloud.tencent.com/document/product/266/33960) | [リンク](#ClipComplete) |
| ビデオスプライシングの完了 | [リンク](https://intl.cloud.tencent.com/document/product/266/33961) | [リンク](#ConcatComplete) |

## 2.0形式イベント通知リスト
[](id:NewFileUpload)
### ビデオアップロードの完了
#### パラメータの説明
| パラメータ名 | タイプ | 説明 |
| -- | -- | -- |
| version | String | コールバックのバージョン番号。`4.0`に固定されています。 |
| eventType | String | コールバックタイプ。`NewFileUpload`に固定されています。 |
| data.fileId | String | ファイルの一意のID。 |
| data.fileName | String | ファイルの表示名。 |
| data.coverUrl | String | ファイルカバーアドレス。 |
| data.fileUrl  | String | ファイル再生アドレス。 |
| data.author | String | 作成者情報。 |
| data.sourceType | String | ファイルのアップロードソース。 現在、Record：レコード、ClientUpload：クライアントからのアップロード、ServerUpload：サーバーからのアップロードがあります。 |
| data.sourceContext | String | アップロード中にパススルーのフィールドを指定します。現在、このフィールドの最大バイト数は256バイトです。 |
| data.streamId | String | ストリームID。レコードとアップロードにのみあります。 |
| data.procedureTaskId | String | このビデオのアップロード後に指定されたプロセスが実行された場合、このパラメータはプロセスタスクIDとなります。 |
| data.transcodeTaskId | String | このビデオのアップロード後にトランスコードが開始された場合、このパラメータはトランスコードタスクIDとなります。 |

#### 事例
```
{
	"version": "4.0",
	"eventType": "NewFileUpload",
	"data": {
		"fileId": "5285890784273533167",
		"fileName": "アニマルワールド",
		"coverUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.jpg",
		"fileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.flv",
		"transcodeTaskId": "transcode-0bee89b07a248e27c83fc3d5951213c1",
		"procedureTaskId": "125676836723-mango-fa2fdf6a0f850d673be119cf51a7603a",
		"sourceType": "Record",
		"sourceContext": "rtmp://54xx.livepush.myqcloud.com/live?bizid=54xx&record=mp4&xx",
		"author": "CCTVレコード",
		"streamId": "54xx_45"
	}
}
```

[](id:PullComplete)
### URLからのビデオプルアップロードの完了
#### パラメータの説明
| パラメータ名 | タイプ | 説明 |
| -- | -- | -- |
| version | String | コールバックのバージョン番号。`4.0`に固定されています。 |
| eventType | String | コールバックタイプ。`PullComplete`に固定されています。 |
| data | Object | 具体的なコールバックデータ。 |
| data.vodTaskId | String | アップロードタスクIDのプル。 |
| data.status | Integer | エラーコード。0：成功。その他の値：失敗。 |
| data.message | String | エラーメッセージ。  |
| data.fileId | String | スプライシングリクエストが開始された後に取得した一意のID。 |
| data.fileUrl | String | ビデオアップロードが完了した後のURL。 |
| data.transcodeTaskId | String | このビデオのアップロード後にトランスコードが開始された場合、このパラメータはトランスコードタスクIDとなります。 |

#### 事例
```json
{
    "version":"4.0",
    "eventType":"PullComplete",
    "data":{
        "status":0,
        "message":"",
        "vodTaskId":"Pull-f5ac8127b3b6b85cdc13f237c6005d8",
        "fileId":"14508071098244959037",
        "fileUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.flv",
        "transcodeTaskId":"transcode-0bee89b07a248e27c83fc3d5951213c1"
    }
}
```

[](id:FileDeleted)
### ビデオ削除の完了
#### パラメータの説明
| パラメータ名 | タイプ | 説明 |
| -- | -- | -- |
| version | String | コールバックのバージョン番号。`4.0`に固定されています。 |
| eventType | String | コールバックタイプ。`FileDeleted`に固定されています。 |
| data.status | Integer | 削除の戻り値。0：成功。その他：失敗。 |
| data.message | String | 削除のエラーメッセージ。 |
| data.fileInfo | Array | 削除されたファイル情報。 |
| data.fileInfo.n.fileId | String | 削除されたファイルID。 |

#### 事例
```json
{
    "version":"4.0",
    "eventType":"FileDeleted",
    "data":{
        "status":0,
        "message":"",
        "fileInfo":[
            {
                "fileId":"24961954183381008"
            }
        ]
    }
}
```

[](id:ProcedureStateChanged)
### タスクフローステータスの変更
#### パラメータの説明
| パラメータ名 | タイプ | 説明 |
| -- | -- | -- |
| version | String | イベント通知のバージョン番号。`4.0`に固定されています。 |
| eventType | String | イベントタイプ。`ProcedureStateChanged`に固定されています。 |
| data | Object | 具体的なコールバックデータ。 |
| data.status | String | タスクフローステータス。PROCESSINGとFINISHがあります。 |
| data.errCode | Integer | エラーコード。0：成功。その他の値：失敗。 |
| data.message | String | エラーメッセージ。 |
| data.fileId | String | ファイルID。 |
| data.metaData | Object | ビデオメタ情報。このフィールドは必ず存在します。フィールド情報については、[metaData（ビデオメタ情報）](#metadata.EF.BC.88.E8.A7.86.E9.A2.91.E5.85.83.E4.BF.A1.E6.81.AF.EF.BC.89)をご参照ください。 |
| data.contentReviewList | Array | コンテンツレビュー結果リスト。フィールド情報については、[contentReviewList（コンテンツレビューリスト）](#contentreviewlist.EF.BC.88.E5.86.85.E5.AE.B9.E5.AE.A1.E6.A0.B8.E5.88.97.E8.A1.A8.EF.BC.89)をご参照ください。 |
| data.aIAnalysisList | Array | インテリジェント分析結果リスト。フィールド情報については、[aIAnalysisList（インテリジェント分析リスト）](#aianalysislist.EF.BC.88.E6.99.BA.E8.83.BD.E5.88.86.E6.9E.90.E5.88.97.E8.A1.A8.EF.BC.89)をご参照ください。 |
| data.drm | Object | ファイル暗号化情報。このフィールドは、ユーザーがタスクフローを開始するときに、[トランスコード制御パラメータ](https://intl.cloud.tencent.com/document/product/266/34125)で暗号化を指定した場合にのみ存在します。 フィールド情報については、[drm（ビデオ暗号化情報）](#drm.EF.BC.88.E8.A7.86.E9.A2.91.E5.8A.A0.E5.AF.86.E4.BF.A1.E6.81.AF.EF.BC.89)をご参照ください。 |
| data.processTaskList | Array | タスクフローに含まれるタスクリスト。フィールド情報については、[processTaskList（タスクリスト）](#processtasklist.EF.BC.88.E4.BB.BB.E5.8A.A1.E5.88.97.E8.A1.A8.EF.BC.89)をご参照ください。 |

##### metaData（ビデオメタ情報）
| **フィールド名** | **タイプ** | **説明** |
| -- | -- | -- |
| size | Integer | ビデオサイズ。単位：byte。 |
| container | String | コンテナタイプ。例えばM4Aや MP4など。 |
| bitrate | Integer | ビデオストリームの平均ビットレートとオーディオストリームの平均ビットレートの合計。単位：kbps。 |
| height | Integer | ビデオストリームの最大高さ。単位：px。 |
| width | Integer | ビデオストリームの最大幅。単位：px。 |
| md5 | String | ビデオのMD5値。 |
| duration | Integer | ビデオ継続時間。単位：秒。 |
| rotate | Integer | ビデオ撮影のときに選択した角度。単位：度。 |
| videoStreamList | Array | ビデオストリーム情報。 |
| videoStreamList.bitrate | Integer | ビデオストリームのビットレート。単位：kbps。 |
| videoStreamList.height | Integer | ビデオストリームの高さ。単位：px。 |
| videoStreamList.width | Integer | ビデオストリームの幅。単位：px。 |
| videoStreamList.codec | String | ビデオストリームのエンコード形式。例えばH.264。 |
| videoStreamList.fps | Integer | フレームレート。単位：Hz。 |
| audioStreamList | Array | オーディオストリーム情報。 |
| audioStreamList.bitrate | Integer | オーディオストリームのビットレート。単位：kbps。 |
| audioStreamList.samplingRate | Integer | オーディオストリームのサンプルレート。単位：Hz。 |
| audioStreamList.codec | String | オーディオストリームのエンコード形式。例えばAAC。 |

##### drm（ビデオ暗号化情報）
| **フィールド名** | **タイプ** | **説明** |
| -- | -- | -- |
| definition | Integer | 暗号化テンプレートID。 |
| keySource | String | KMSのタイプ。`VodBuildInKMS`に固定されています。 |
| getKeyUrl | String | 取得した復号キーのURL。|
| edkList | Array | 暗号化されたデータキーリスト。 |

##### contentReviewList（コンテンツレビューリスト）
コンテンツレビュー情報リストは、現在、[Porn（ポルノ検出）](#porn.EF.BC.88.E9.89.B4.E9.BB.84.EF.BC.89)のみをサポートしています。

##### Porn（ポルノ検出）
| **フィールド名** | **タイプ** | **説明** |
| -- | -- | -- |
| taskType | String | タスクタイプ。`Porn`に固定されています。 |
| status | String | タスクステータス。PROCESSING、SUCCESSおよびFAILがあります。 |
| errCode | Integer | エラーコード。 0：成功。その他の値：失敗。そのうち30009は元のファイルの異常による失敗を意味し、30010はシステム障害または不明を意味します。 |
| message | String | エラーメッセージ。 |
| input | Object | タスクの入力情報。 |
| input.definition | Integer | ポルノ検出テンプレートID。 |
| output | Object | タスクの出力情報。タスクが成功するとこのフィールドが表示され、失敗するとこのフィールドは表示されません。 |
| output.confidence | Float | ビデオポルノ検出スコア。スコアの範囲は0～100です。 |
| output.suggestion | String | ポルノ検出結果のアドバイス。pass、reviewおよびblockがあります。 |
| output.segments | Array | ポルノが疑われるビデオセグメント。 |
| output.segments.startTimeOffset | Float | 疑わしいセグメント開始のオフセット時間。単位は秒。 |
| output.segments.endTimeOffset | Float |疑わしいセグメント終了のオフセット時間。単位は秒。 |
| output.segments.confidence | Float | 疑わしいセグメントのポルノ検出スコア。 |
| output.segments.suggestion | Float | 疑わしいセグメントのポルノ検出結果のアドバイス。pass、reviewおよびblockがあります。 |
| output.segments.url | String | ポルノが疑われる画像のURL（画像は永続的には保存されず、しばらくすると無効になります）。 |
| output.segments.picUrlExpireTimeStamp | Integer | ポルノが疑われる画像のURL有効期限（Unixタイムスタンプ）。 |

##### aIAnalysisList（インテリジェント分析リスト）
インテリジェント分析情報リストには現在、次のような種類があります。
- [Classification（インテリジェント分類）](#classification.EF.BC.88.E6.99.BA.E8.83.BD.E5.88.86.E7.B1.BB.EF.BC.89)
- [Tag（インテリジェントタグ）](#tag.EF.BC.88.E6.99.BA.E8.83.BD.E6.A0.87.E7.AD.BE.EF.BC.89)

##### Classification（インテリジェント分類）
| **フィールド名** | **タイプ** | **説明** |
| -- | -- | -- |
| taskType | String | タスクタイプ。`Classification`に固定されています。 |
| status | String | タスクステータス。PROCESSING、SUCCESSおよびFAILがあります。 |
| errCode | Integer | エラーコード。 0：成功、その他の値：失敗。そのうち`30009`は元のファイルの異常による失敗を意味し、`30010`はシステム障害または不明を意味します。 |
| message | String | エラーメッセージ。 |
| input | Object | タスクの入力情報。 |
| input.definition | Integer | インテリジェント分類テンプレートID。 |
| output | Object | タスクの出力情報。タスクが成功するとこのフィールドが表示され、失敗するとこのフィールドは表示されません。 |
| output.classifications | Array | 分類情報リスト。 |
| output.classifications.classification | String | 分類カテゴリ名。 |
| output.classifications.confidence | Float | 分類の信頼性。 |

##### Tag（インテリジェントタグ）
| **フィールド名** | **タイプ** | **説明** |
| -- | -- | -- |
| taskType | String | タスクタイプ。`Tag`に固定されています。 |
| status | String | タスクステータス。PROCESSING、SUCCESSおよびFAILがあります。 |
| errCode | Integer | エラーコード。 0：成功、その他の値：失敗。そのうち`30009`は元のファイルの異常による失敗を意味し、`30010`はシステム障害または不明を意味します。 |
| message | String | エラーメッセージ。 |
| input | Object | タスクの入力情報。 |
| input.definition | Integer | インテリジェントタグテンプレートID。 |
| output | Object | タスクの出力情報。タスクが成功するとこのフィールドが表示され、失敗するとこのフィールドは表示されません。 |
| output.tags | Array | タグ情報リスト。 |
| output.tags.tag | String | タグ名。 |
| output.tags.confidence | Float | タグの信頼性。 |

##### processTaskList（タスクリスト）
タスク情報リストには現在、次のような種類があります。
- [Trancode（トランスコードタスク）](#trancode.EF.BC.88.E8.BD.AC.E7.A0.81.E4.BB.BB.E5.8A.A1.EF.BC.89)
- [AnimatedGraphics（アニメーション画像生成タスク）](#animatedgraphics.EF.BC.88.E8.BD.AC.E5.8A.A8.E5.9B.BE.E4.BB.BB.E5.8A.A1.EF.BC.89)
- [SampleSnapshot（サンプリングスクリーンキャプチャタスク）](#samplesnapshot.EF.BC.88.E9.87.87.E6.A0.B7.E6.88.AA.E5.9B.BE.E4.BB.BB.E5.8A.A1.EF.BC.89)
- [CoverBySnapshot（ビデオカバータスクとしてのスクリーンキャプチャ画像）](#coverbysnapshot.EF.BC.88.E6.88.AA.E5.9B.BE.E5.9B.BE.E7.89.87.E4.BD.9C.E4.B8.BA.E8.A7.86.E9.A2.91.E5.B0.81.E9.9D.A2.E4.BB.BB.E5.8A.A1.EF.BC.89)
- [SnapshotByTimeOffset（タイムポイントによるスクリーンキャプチャタスク）](#snapshotbytimeoffset.EF.BC.88.E6.8C.89.E6.97.B6.E9.97.B4.E7.82.B9.E6.88.AA.E5.9B.BE.E4.BB.BB.E5.8A.A1.EF.BC.89)
- [ImageSprites（スプライトイメージのスクリーンキャプチャタスク）](#imagesprites.EF.BC.88.E9.9B.AA.E7.A2.A7.E5.9B.BE.E6.88.AA.E5.9B.BE.E4.BB.BB.E5.8A.A1.EF.BC.89)


##### Trancode（トランスコードタスク）
| **フィールド名** | **タイプ** | **説明** |
| -- | -- | -- |
| taskType | String | タスクタイプ。`Transcode`に固定されています。 |
| status | String | タスクステータス。PROCESSING、SUCCESSおよびFAILがあります。 |
| errCode | Integer | エラーコード。 0：成功、その他の値：失敗。そのうち`30009`は元のファイルの異常による失敗を意味し、`30010`はシステム障害または不明を意味します。 |
| message | String | エラーメッセージ。 |
| input | Object | タスクの入力情報。 |
| input.definition | Integer | トランスコードテンプレートID。 |
| input.watermark | Integer | ウォーターマークを設定するかどうか。1は設定、0は設定しません。設定するかどうかは、ユーザーのトランスコード設定によって決まります。 |
| input.mosaicList | Array | モザイクブロック処理リスト。要素は単一のブロック処理したモザイク情報です。 |
| input.mosaicList.width | String | モザイクの幅。 |
| input.mosaicList.height | String | モザイクの高さ。 |
| input.mosaicList.left | String | モザイクの左上隅がビデオの水平位置にあります。 |
| input.mosaicList.top | String | モザイクの左上隅がビデオの垂直位置にあります。 |
| input.mosaicList.startTimeOffset | Float | ビデオのモザイクの開始時間。 |
| input.mosaicList.endTimeOffset | Float | ビデオのモザイクの終了時間。 |
| output | Object | タスクの出力情報。タスクが成功するとこのフィールドが表示され、失敗するとこのフィールドは表示されません。 |
| output.url | String | ビデオURL。 |
| output.size | Integer | ビデオサイズ。単位：byte。 |
| output.container | String | コンテナタイプ。例えばM4AやMP4など。 |
| output.bitrate | Integer | ビデオストリームとオーディオストリームのビットレートの和。単位：kbps。 |
| output.height | Integer | ビデオストリームの最大高さ。単位：px。 |
| output.width | Integer | ビデオストリームの最大幅。単位：px。 |
| output.md5 | String | ビデオのMD5値。 |
| output.duration | Integer | ビデオ継続時間。単位：秒。 |
| output.videoStreamList | Array | ビデオストリーム情報。要素フィールドはメタ情報のvideoStreamListと同じです。 |
| output.audioStreamList | Array |オーディオストリーム情報。要素フィールドはメタ情報のaudioStreamListと同じです。 |

#### AnimatedGraphics（アニメーション画像生成タスク）
| **フィールド名** | **タイプ** | **説明** |
| -- | -- | -- |
| taskType | String | タスクタイプ。`AnimatedGraphics`に固定されています。 |
| status | String | タスクステータス。PROCESSING、SUCCESSおよびFAILがあります。 |
| errCode | Integer | エラーコード。 0：成功、その他の値：失敗。そのうち`30009`は元のファイルの異常による失敗を意味し、`30010`はシステム障害または不明を意味します。 |
| message | String | エラーメッセージ。 |
| input | Object | タスクの入力情報。 |
| input.definition | Integer | アニメーション画像生成テンプレートID。 |
| input.startTime | Integer | ビデオのアニメーションの開始時間。単位：秒。 |
| input.endTime | Integer | ビデオのアニメーションの終了時間。単位：秒。 |
| output | Object | タスクの出力情報。タスクが成功するとこのフィールドが表示され、失敗するとこのフィールドは表示されません。 |
| output.url | String | アニメーションURL。 |
| output.container | String |アニメーションタイプ。例えばGIFやWEBPなど。 |
| output.fps | Integer | アニメーションフレームレート。単位：fps。 |
| output.height | Integer | アニメーションの高さ。単位：px。 |
| output.width | Integer | アニメーションの幅。単位：px。 |

#### SampleSnapshot（サンプリングスクリーンキャプチャタスク）
| **フィールド名** | **タイプ** | **説明** |
| -- | -- | -- |
| taskType | String | タスクタイプ。`SampleSnapshot`に固定されています。 |
| status | String | タスクステータス。PROCESSING、SUCCESSおよびFAILがあります。 |
| errCode | Integer | エラーコード。 0：成功、その他の値：失敗。そのうち`30009`は元のファイルの異常による失敗を意味し、`30010`はシステム障害または不明を意味します。 |
| message | String | エラーメッセージ。 |
| input | Object | タスクの入力情報。 |
| input.definition | Integer | サンプリングスクリーンキャプチャテンプレートID。 |
| input.watermarkDefinition | Array | 整数配列。ウォーターマークテンプレートIDリスト。 |
| output | Object | タスクの出力情報。タスクが成功するとこのフィールドが表示され、失敗するとこのフィールドは表示されません。 |
| output.imageUrls | Array | 文字列配列。生成されたスクリーンキャプチャURLリスト。 |

#### SnapshotByTimeOffset（タイムポイントによるスクリーンキャプチャタスク）
| **フィールド名** | **タイプ** | **説明** |
| -- | -- | -- |
| taskType | String | タスクタイプ。`SnapshotByTimeOffset`に固定されています。 |
| status | String | タスクステータス。PROCESSING、SUCCESSおよびFAILがあります。 |
| errCode | Integer | エラーコード。 0：成功、その他の値：失敗。そのうち`30009`は元のファイルの異常による失敗を意味し、`30010`はシステム障害または不明を意味します。 |
| message | String | エラーメッセージ。 |
| input | Object | タスクの入力情報。 |
| input.definition | Integer | タイムポイントによるスクリーンキャプチャテンプレートID。 |
| input.timeOffset | Array | 整数配列。スクリーンキャプチャの時間オフセット。単位はミリ秒。 |
| input.watermarkDefinition | Array | 整数配列。ウォーターマークテンプレートIDリスト。 |
| output | Object | タスクの出力情報。タスクが成功するとこのフィールドが表示され、失敗するとこのフィールドは表示されません。 |
| output.imgInfo | Array | 生成されたスクリーンキャプチャ情報リスト。 |
| output.imgInfo.timeOffset | Integer | このスクリーンキャプチャの時間オフセット。単位はミリ秒。 |
| output.imgInfo.url | String | スクリーンキャプチャURL。 |

#### CoverBySnapshot（ビデオカバータスクとしてのスクリーンキャプチャ画像）

| **フィールド名** | **タイプ** | **説明** |
| -- | -- | -- |
| taskType | String | タスクタイプ。`CoverBySnapshot`に固定されています。 |
| status | String | タスクステータス。PROCESSING、SUCCESSおよびFAILがあります。 |
| errCode | Integer | エラーコード。 0：成功、その他の値：失敗。そのうち`30009`は元のファイルの異常による失敗を意味し、`30010`はシステム障害または不明を意味します。 |
| message | String | エラーメッセージ。 |
| input | Object | タスクの入力情報。 |
| input.definition | Integer | サンプリングスクリーンキャプチャテンプレートID。 |
| input.positionType | String | スクリーンキャプチャ方式。Time：タイムポイントによるスクリーンキャプチャ。Percent：パーセンテージによるスクリーンキャプチャ。 |
| input.position | Integer | スクリーンキャプチャ位置。タイムポイントによるスクリーンキャプチャの場合、この値は、最初の数秒間にカバーとして指定されたビデオのスクリーンキャプチャを示します。パーセンテージによるスクリーンキャプチャの場合、この値は、ビデオのスクリーンキャプチャのうち何パーセントがカバーとして使用されているかを示します。 |
| input.watermarkDefinition | Array | 整数配列。ウォーターマークテンプレートIDリスト。 |
| output | Object | タスクの出力情報。タスクが成功するとこのフィールドが表示され、失敗するとこのフィールドは表示されません。 |
| output.imageUrl | Array | ビデオカバーとして使用されているスクリーンキャプチャURL。 |

#### PullFile（ビデオプルファイルタスク）
| **フィールド名** | **タイプ** | **説明** |
| -- | -- | -- |
| taskType | String | タスクタイプ。`PullFile`に固定されています。 |
| status | String | タスクステータス。PROCESSING、SUCCESSおよびFAILがあります。 |
| errCode | Integer | エラーコード。0：成功。その他の値：失敗。 |
| message | String | エラーメッセージ。 |
| input | Object | タスクの入力情報。 |
| input.url | String | プルする必要があるビデオのURL。 |
| input.fileName | String | ビデオファイルの名称。 |
| input.md5 | Integer | ビデオファイルのMD5。 |
| output | Object | タスクの出力情報。タスクが成功するとこのフィールドが表示され、失敗するとこのフィールドは表示されません。 |
| output.fileId | String | ビデオファイルID。 |
| output.fileSize | String | ビデオファイルサイズ。 |
| output.url | String | ビデオファイルの再生アドレス。 |

#### ImageSprites（スプライトイメージスクリーンキャプチャタスク）
| **フィールド名** | **タイプ** | **説明** |
| -- | -- | -- |
| taskType | String | タスクタイプ。`ImageSprites`に固定されています。 |
| status | String | タスクステータス。PROCESSING、SUCCESSおよびFAILがあります。 |
| errCode | Integer | エラーコード。0：成功。その他の値：失敗。 |
| message | String | エラーメッセージ。 |
| intput | Object | タスクの入力情報。タスクが成功するとこのフィールドが表示され、失敗するとこのフィールドは表示されません。 |
| input.definition | Integer | スプライトイメージテンプレートID。 |
| output | Object | タスクの出力情報。 |
| output.totalCount | Integer | スプライトイメージサムネイルの総数。 |
| output.urlList | Array | 文字列配列。生成されたスプライトイメージのURLリスト。 |
| output.webVttUrl | String | スプライトイメージサムネイルの位置と時間関係のWebVTTファイルアドレス。 |

#### 事例
```json
{
    "version":"4.0",
    "eventType":"ProcedureStateChanged",
    "data":{
        "vodTaskId":"125676836723-xxx-25f5aac63",
        "status":"PROCESSING",
        "message":"",
        "errCode":0,
        "fileId":"14508071098244959037",
        "metaData":{
            "size":10556,
            "container":"m4a",
            "bitrate":246035,
            "height":480,
            "width":640,
            "md5":"b3ae6ed07d9bf4efeeb94ed2d37ff3e3",
            "duration":3601,
            "videoStreamList":[
                {
                    "bitrate":246000,
                    "height":480,
                    "width":640,
                    "codec":"h264",
                    "fps":22
                }
            ],
            "audioStreamList":[
                {
                    "codec":"aac",
                    "samplingRate":44100,
                    "bitrate":35
                }
            ]
        },
        "drm":{
            "definition":10,
            "getKeyUrl":"https://123.xxx.com/getkey",
            "keySource":"VodBuildInKMS",
            "edkList":[
                "232abc30"
            ]
        },
        "contentReviewList":[
            {
                "taskType":"Porn",
                "status":"SUCCESS",
                "errCode":0,
                "message":"",
                "input":{
                    "definition":10
                },
                "output":{
                    "confidence":98,
                    "suggestion":"block",
                    "segments":[
                        {
                            "startTimeOffset":20,
                            "endTimeOffset":120,
                            "confidence":98,
                            "suggestion":"block",
                            "url":"http://125676836723.vod2.myqcluod.com/xxx/xxx/xx.jpg",
                            "picUrlExpireTimeStamp":1530005146
                        },
                        {
                            "startTimeOffset":120,
                            "endTimeOffset":130,
                            "confidence":54,
                            "suggestion":"review",
                            "url":"http://125676836723.vod2.myqcluod.com/xxx/xxx/xx.jpg",
                            "picUrlExpireTimeStamp":1530005146
                        }
                    ]
                }
            }
        ],
        "processTaskList":[
            {
                "taskType":"Transcode",
                "status":"PROCESSING",
                "errCode":0,
                "message":"",
                "input":{
                    "definition":10,
                    "watermark":1
                }
            },
            {
                "taskType":"Transcode",
                "status":"SUCCESS",
                "errCode":0,
                "message":"",
                "input":{
                    "definition":20,
                    "watermark":1
                },
                "output":{
                    "url":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f20.mp4",
                    "size":10556,
                    "container":"m4a",
                    "md5":"b3ae6ed07d9bf4efeeb94ed2d37ff3e3",
                    "bitrate":246035,
                    "height":480,
                    "width":640,
                    "duration":3601,
                    "videoStreamList":[
                        {
                            "bitrate":246000,
                            "height":480,
                            "width":640,
                            "codec":"h264",
                            "fps":20
                        }
                    ],
                    "audioStreamList":[
                        {
                            "codec":"aac",
                            "samplingRate":44100,
                            "bitrate":35
                        }
                    ]
                }
            },
            {
                "taskType":"SampleSnapshot",
                "status":"SUCCESS",
                "errCode":0,
                "message":"",
                "input":{
                    "definition":10
                },
                "output":{
                    "imageUrls":[
                        "http://125676836723.vod2.myqcloud.com/xxx/xxx/shotup/xx1.png",
                        "http://125676836723.vod2.myqcloud.com/xxx/xxx/shotup/xx2.png",
                        "http://125676836723.vod2.myqcloud.com/xxx/xxx/shotup/xx3.png"
                    ]
                }
            }
        ]
    }
}
```

[](id:TranscodeComplete)
### ビデオトランスコードの完了
#### パラメータの説明
| パラメータ名 | タイプ | 説明 |
| -- | -- | -- |
| version | String | イベント通知のバージョン番号。`4.0`に固定されています。 |
| eventType | String | イベントタイプ。`TranscodeComplete`に固定されています。 |
| data | Object | 具体的なコールバックデータ。 |
| data.status | Integer | エラーコード。0：成功。その他の値：失敗。 |
| data.message | String | エラーメッセージ。  |
| data.fileId | String | トランスコードされるファイルID。 |
| data.vodTaskId | String | トランスコードタスクID。 |

#### 事例
```json
{
    "version": "4.0",
    "eventType": "TranscodeComplete",
    "data": {
        "status": 0,
        "message": "",
        "vodTaskId": "Transcode-1edb7eb88a599d05abe451cfc541cfbd",
        "fileId": "14508071098244931831",
        "fileName": "アニマルワールド",
        "duration": 599,
        "coverUrl": "http://125676836723.vod2.myqcloud.com/0/xxx/640",
        "playSet": [
            {
                "url": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4",
                "definition": 0,
                "vbitrate": 246000,
                "vheight": 480,
                "vwidth": 640
            },
            {
                "url": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f10.mp4",
                "definition": 10,
                "vbitrate": 149193,
                "vheight": 240,
                "vwidth": 320
            },
            {
                "url": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f20.mp4",
                "definition": 20,
                "vbitrate": 297656,
                "vheight": 480,
                "vwidth": 640
            },
            {
                "url": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f30.mp4",
                "definition": 30,
                "vbitrate": 899976,
                "vheight": 960,
                "vwidth": 1280
            }
        ]
    }
}
```

[](id:CreateSnapshotByTimeOffsetComplete)
### 指定タイムポイントスクリーンキャプチャの完了
#### パラメータの説明
| パラメータ名 | タイプ | 説明 |
| -- | -- | -- |
| version | String | コールバックのバージョン番号。`4.0`に固定されています。 |
| eventType | String | コールバックタイプ。`CreateSnapshotByTimeOffsetComplete`に固定されています。 |
| data | Object | 具体的なコールバックデータ。 |
| data.vodTaskId | String | 指定タイムポイントスクリーンキャプチャタスクID。  |
| data.fileId | String | 指定タイムポイントスクリーンキャプチャのFileId。  |
| data.definition | Integer | スクリーンキャプチャの仕様については、[指定タイムポイントスクリーンキャプチャパラメータテンプレート](https://intl.cloud.tencent.com/document/product/266/33940)をご参照ください。 |
| data.picInfo | Array | 指定タイムポイントスクリーンキャプチャによって出力されたスクリーンキャプチャ情報。 |

data.picInfo配列の各要素はObjectで、パラメータの意味は次のとおりです。

| パラメータ名 | タイプ | 説明 |
| -- | -- | -- |
| timeOffset | Integer | スクリーンキャプチャの具体的なタイムポイント。単位：ミリ秒。 |
| url | String | スクリーンキャプチャファイルURL。  |
| status | Integer | エラーコード。0：成功。その他の値：失敗。 |

#### 事例
```json
{
    "version": "4.0",
    "eventType": "CreateSnapshotByTimeOffsetComplete",
    "data": {
        "vodTaskId": "CreateSnapshotByTimeOffset-1edb7eb88a599d05abe451cfc541cfbd",
        "fileId": "14508071098244929440",
        "definition": 10,
        "picInfo": [
            {
                "status": 0,
                "timeOffset": 10000,
                "url": "http://125676836723.vod2.myqcloud.com/xxx/xxx/1.png"
            },
            {
                "status": 0,
                "timeOffset": 20000,
                "url": "http://125676836723.vod2.myqcloud.com/xxx/xxx/2.png"
            }
        ]
    }
}
```

[](id:CreateImageSpriteComplete)
### ビデオキャプチャスプライトイメージ生成の完了
#### パラメータの説明
| パラメータ名 | タイプ | 説明 |
| -- | -- | -- |
| version | String | コールバックのバージョン番号。`4.0`に固定されています。 |
| eventType | String | コールバックタイプ。`CreateImageSpriteComplete`に固定されています。 |
| data | Object | 具体的なコールバックデータ。 |
| data.status | Integer | エラーコード。0：成功。その他の値：失敗。 |
| data.message | String | エラーメッセージ。 |
| data.vodTaskId | String | キャプチャスプライトイメージタスクID。 |
| data.fileId | String | キャプチャスプライトイメージのFileId。 |
| data.definition | Integer | スプライトイメージの仕様については、[スプライトイメージスクリーンキャプチャテンプレート](https://intl.cloud.tencent.com/document/product/266/33940)をご参照ください。 |
| data.totalCount | Integer | スプライトイメージサムネイルの総数。 |
| data.imageSpriteUrl | Array | スクリーンキャプチャスプライトイメージによって出力されたスプライトイメージ情報。 |
| data.webVttUrl | String | スプライトイメージサムネイルの位置と時間関係のWebVTTファイルアドレス。 |

#### 事例
```json
{
    "version":"4.0",
    "eventType":"CreateImageSpriteComplete",
    "data":{
        "status":0,
        "message":"",
        "vodTaskId":"CreateImageSprite-1edb7eb88a599d05abe451cfc541cfbd",
        "fileId":"14508071098244929440",
        "definition":10,
        "totalCount":106,
        "imageSpriteUrl":[
            "http://125676836723.vod2.myqcloud.com/xxx/xxx/1.png",
            "http://125676836723.vod2.myqcloud.com/xxx/xxx/2.png"
        ],
        "webVttUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.vtt"
    }
}
```

[](id:ClipComplete)
### ビデオトリミングの完了
#### パラメータの説明
| パラメータ名 | タイプ | 説明 |
| -- | -- | -- |
| version | String | コールバックのバージョン番号。`4.0`に固定されています。 |
| eventType | String | コールバックタイプ。`ClipComplete`に固定されています。 |
| data | Object | 具体的なコールバックデータ。 |
| data.vodTaskId | String | トリミングタスクID。  |
| data.srcFileId | String | トリミングタスクソースファイルFileId。 |
| data.fileInfo | Object | トリミングで出力されたビデオファイル情報。 |

data.fileInfo各パラメータの意味は次のとおりです。

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| fileType | String | トリミングするファイルタイプ。 |
| status | Integer | このタイプのファイルのエラーメッセージ。0：成功、その他：失敗。 |
| message | String | エラーメッセージ。 |
| fileId | String | トリミングするファイルのfileId。 |
| fileUrl | String | トリミングするファイルURL。 |

#### 事例
```json
{
    "version": "4.0",
    "eventType": "ClipComplete",
    "data": {
        "vodTaskId": "clipVideo-0a78cf44c4285026a4c",
        "srcFileId": "16092504232103571364",
        "fileInfo": {
            "fileType": "mp4",
            "status": 0,
            "message": "",
            "fileId": "14508071098244929440",
            "fileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4"
        }
    }
}
```


[](id:ConcatComplete)
### ビデオスプライシングの完了
#### パラメータの説明
| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| version | String | コールバックのバージョン番号。`4.0`に固定されています。 |
| eventType | String | コールバックタイプ。`ConcatComplete`に固定されています。 |
| data | Object | 具体的なコールバックデータ。 |
| data.vodTaskId | String | スプライシングタスクID。 |
| data.fileInfo | Array | スプライシングによって出力されたビデオファイル情報。 |

data.fileInfo配列の各要素はObjectで、パラメータの意味は次のとおりです。

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| fileType | String | スプライシングされたファイルタイプ。 |
| status | Integer | タスクの実行結果。0は成功を意味し、-1または4は失敗を意味します。 |
| message | String | エラーメッセージ。 |
| fileId | String | スプライシングされたファイルのfileId。 |
| fileUrl | String | スプライシングされたファイルURL。 |

#### 事例
```json
{
    "version": "4.0",
    "eventType": "ConcatComplete",
    "data": {
        "vodTaskId": "Concat-1edb7eb88a599d05abe451cfc541cfbd",
        "fileInfo": [
            {
                "fileType": "m3u8",
                "status": 0,
                "message": "",
                "fileId": "14508071098244931831",
                "fileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/playlist.f6.m3u8"
            },
            {
                "fileType": "mp4",
                "status": 0,
                "message": "",
                "fileId": "14508071098244929440",
                "fileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4"
            }
        ]
    }
}
```
