ビデオ合成は、VODの中のビデオに対して、トリミング、スプライシング、オーバーレイ、反転などの複雑な操作を行なうことを指し、オフラインタスクです。ビデオ合成を使用すると、次の効果を付けることができます。

* **画面の回転**：ビデオ、画像の画面を一定の角度に回転、または特定の方向に反転させます。
* **サウンドコントロール**：ビデオ、音声の中の音のボリュームを上げ下げしたり、またはビデオをミュートにしたりします。
* **画面のオーバーレイ**：ビデオ、画像の中の画面を順番に重ねて1つにし、例えば、「ピクチャーインピクチャー」効果を実現します。
* **音声ミキシング**：ビデオ、音声の中の音を1つに合成します（オーディオミキシング）。
* **音声抽出**：ビデオの中の音声を抽出します（画面は残しません）。
* **トリミング**：指定時間範囲のビデオ、音声を切り取ります。
* **スプライシング**：ビデオ、音声、画像を時間順に前後をつなぎ合わせます。
* **場面転換**：複数の場面のビデオまたは画像をスプライシングするとき、段落の間に場面転換の効果を追加することができます。
* **倍速**：ビデオまたはオーディオ素材を早送りまたはスロー再生処理します。

合成後に生成されるメディアのコンテナ形式はMP4（ビデオ）またはMP3（音声）です。

## タスクの開始

ビデオ合成タスクは、[サーバーAPI](https://intl.cloud.tencent.com/document/product/266/34127) 方式により開始されます。APIの呼び出しで戻される結果の中にタスクIDが含まれ、これを [結果の取得](#.E7.BB.93.E6.9E.9C.E8.8E.B7.E5.8F.96) 時の対応するタスクの結果とのバインドに使用します。

## 結果の取得

タスクの開始後、非同期の[結果通知](https://intl.cloud.tencent.com/document/product/266/33931) 待ちおよび同期の [タスク確認](https://intl.cloud.tencent.com/document/product/266/33931) の2種類の方式でビデオ合成の実行結果を取得できます。以下は、ビデオ合成タスクの開始後、通常のコールバック方式での結果通知の例となります（値がnullのフィールドは省略）。

```json
{
	"EventType": "ComposeMediaComplete",
	"ComposeMediaCompleteEvent": {
		"TaskId": "ComposeMedia-f5ac8127b3b6b85cdc13f237c6005d8",
		"Status": "FINISH",
		"ErrCode": 0,
		"Message": "SUCCESS",
		"Input":{
			"Tracks": [{
					"Type": "Video",
					"TrackItems": [{
						"Type": "Video",
						"SourceMedia": "5285485487985271487",
						"AudioOperations": [{
							"Type": "Volume",
							"VolumeParam": {
								"Mute": 1
							}
						}]
					}]
				},
				{
					"Type": "Audio",
					"TrackItems": [{
							"Type": "Empty",
							"EmptyItem": {
								"Duration": 5
							}
						},
						{
							"Type": "Audio",
							"AudioItem": {
								"SourceMedia": "5285485487985271488",
								"Duration": 15
							}
						},
						{
							"Type": "Audio",
							"AudioItem": {
								"SourceMedia": "5285485487985271489",
								"SourceMediaStartTime": 2,
								"Duration": 14
							}
						}
					]
				}
			],
			"Output":{
				"FileName": "ビデオ合成効果テスト",
				"Container": "mp4"
			}
		},
		"Output":{
			"FileType": "mp4",
			"FileId": 5285485487985271490,
			"FileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.mp4"
		}
	}
}
```

コールバックの結果の中で、`Input.Tracks`には2つのエレメントが含まれ、`Type`が それぞれVideoとAudioになっています。これは合成されたビデオに1つのビデオトラックと音声トラック含まれていることを表します。
- ビデオトラック：ソースビデオIDは5285485487985271487です。それに対してミュート処理を行いました。
- 音声トラック：5秒のミュート、および15秒と14秒の2つのダビングが含まれています。

`Output.FileId`はビデオ合成後に生成される新しいビデオFileIdで、ビデオ再生URLは`FileUrl`の中の値です。


