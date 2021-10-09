ユーザーがルートアカウントのライブストリーミングリソースにアクセスする場合は認証ルールに従う必要があります。このテキストでは、ライブストリーミングAPI認証のルールについてご説明します。

## 認証ルール

サブアカウントがライブストリーミングサービスAPIを介してルートアカウントのライブストリーミングリソースにアクセスすると、リソース所有者の関連リソースの関連権限を呼び出し元に付与することを確実に保証するため、ライブストリーミングサービスのバックエンドでサブユーザーの権限をチェックします。

ライブストリーミングサービスAPIごとに、それぞれ関連するリソースとAPIのセマンティクスに応じて、チェックする必要のあるリソースの権限を決定します。各APIの具体的な認証ルールについては下表をご参照ください。

## リソースレベルの承認をサポートするAPI

| インターフェース名                        | インターフェースの機能                          | リソース（Resource）                                      |
| ------------------------------- | --------------------------------- | ----------------------------------------------------- |
| DescribeLiveDomainReferer       | ライブストリーミングドメイン名の照会Refererブラックリスト/ホワイトリストの設定 | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DescribeLivePlayAuthKey         | 再生認証keyの照会                  | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DescribeLivePushAuthKey         | プッシュ認証keyの照会                  | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| ModifyLiveDomainReferer         | ライブストリーミングドメイン名の設定Refererブラックリスト/ホワイトリスト     | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| ModifyLivePlayAuthKey           | 再生認証keyの修正                  | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| ModifyLivePushAuthKey           | プッシュ認証keyの修正                 | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DescribeLiveStreamEventList     | プッシュストリーム切断イベントの照会                  | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DescribeLiveStreamOnlineList    | ライブストリーミング中のストリームの照会                    | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DescribeLiveStreamPublishedList | 過去のストリームリストの照会                    | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DescribeLiveStreamState         | ストリームステータスの照会                      | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DropLiveStream                  | CSSストリームの切断                        | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| ForbidLiveStream                | CSSストリームプッシュ禁止                        | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| ResumeLiveStream                | CSSプッシュの復元                      | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| CreateLiveWatermarkRule         | ウォーターマークルールの作成                      | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DeleteLiveWatermarkRule         | ウォーターマークルールの削除                      | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| CreateLiveTranscodeRule         | トランスコードルールの作成                      | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DeleteLiveTranscodeRule         | トランスコードルールの削除                      | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| AddLiveDomain                   | ドメイン名の追加                          | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DeleteLiveDomain                | ドメイン名の削除                          | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DescribeLiveDomain              | ドメイン名情報の照会                      | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| EnableLiveDomain                | ドメイン名の有効化                          | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| ForbidLiveDomain                | ドメイン名の使用禁止                          | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| ModifyLivePlayDomain            | 再生ドメイン名情報の修正                  | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| CreateLiveSnapshotRule          | スクリーンキャプチャルールの作成                    | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DeleteLiveSnapshotRule          | スクリーンキャプチャルールの削除                    | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| AddDelayLiveStream              | 再生の遅延                          | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| ResumeDelayLiveStream           | 再生の遅延の修復                          | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DescribeLiveStreamPushInfoList  | オンラインストリームのプッシュデータの取得              | qcs::${ApiModule}:${Region}:uin/:domain/${PushDomain} |
| DescribeLiveTranscodeDetailInfo | CSSトランスコード統計情報の照会           | qcs::${ApiModule}:${Region}:uin/:domain/${PushDomain} |
| DescribeStreamDayPlayInfoList   | 全ストリームのトラフィックデータの照会              | qcs::${ApiModule}:${Region}:uin/:domain/${PlayDomain} |
| DescribeStreamPlayInfoList      | ストリームの再生情報リストの照会              | qcs::${ApiModule}:${Region}:uin/:domain/${PlayDomain} |
| CreateLiveCallbackRule          | コールバックルールの作成                      | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DeleteLiveCallbackRule          | コールバックルールの削除                      | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| BindLiveDomainCert              | ドメイン名バインド証明書                      | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DescribeLiveDomainCert          | ドメイン名証明書情報の取得                  | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| ModifyLiveDomainCert            | ドメイン名および証明書バインド情報の修正            | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| UnBindLiveDomainCert            | ドメイン名証明書のバインド解除                      | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| CreateLiveRecordRule            | レコーディングルールの作成                    | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| CreateRecordTask                | レコーディングタスクの作成（新）                | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DeleteLiveRecordRule            | レコーディングルールの削除                     | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DeleteRecordTask                | レコーディングタスクの削除（新）                | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DescribeRecordTask              | レコーディングタスクリストの照会（新）            | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| StopRecordTask                  | レコーディングタスクの終了（新）                | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |

