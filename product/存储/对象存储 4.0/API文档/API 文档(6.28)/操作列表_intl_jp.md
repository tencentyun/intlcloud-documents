Tencent Cloud COS関連のAPIと説明は次のとおりです：

## サービス操作について
| API                                      | 操作名   | 操作説明            |
| ---------------------------------------- | ----- | --------------- |
| [GET Service](https://cloud.tencent.com/document/product/436/8291) | バケットリストを取得します | 指定されたアカウント下にあるすべてのバケットリストを取得します |

## バケット操作について

| API                                      | 操作名       | 操作説明                        |
| ---------------------------------------- | --------- | --------------------------- |
| [DELETE Bucket](https://cloud.tencent.com/document/product/436/7732) | バケットを削除します     | 指定されたアカウント下にあるブランクバケットを削除します             |
| [DELETE Bucket cors](https://cloud.tencent.com/document/product/436/8283) | クロスオリジン構成を削除します    | バケットのクロスオリジンアクセス構成情報を削除します         |
| [DELETE Bucket lifecycle](https://cloud.tencent.com/document/product/436/8284) | ライフサイクルを削除します    | バケットライフサイクル管理の構成を削除します                 |
|[DELETE Bucket policy](https://cloud.tencent.com/document/product/436/8285)  |  バケットポリシーを削除します |指定されたバケットの権限ポリシーを削除します|
| [GET Bucket(List Object)](https://cloud.tencent.com/document/product/436/7734) | オブジェクトリストを取得します      | バケット下にある一部またはすべてのオブジェクトを取得します |
| [GET Bucket acl](https://cloud.tencent.com/document/product/436/7733) | バケットACLを取得します | バケットのACLを取得します           |
| [GET Bucket cors](https://cloud.tencent.com/document/product/436/8274) | クロスオリジン構成を取得します    | バケットのクロスオリジンアクセス構成情報を取得します         |
| [GET Bucket lifecycle](https://cloud.tencent.com/document/product/436/8278) | ライフサイクルを照合します    | バケットライフサイクル管理の構成を照合します                 |
|  [GET Bucket policy](https://cloud.tencent.com/document/product/436/8276)  | バケットポリシーを照合します |指定されたバケットの権限ポリシーを照合します|
| [HEAD Bucket](https://cloud.tencent.com/document/product/436/7735) | バケットとその権限を検索します   | バケットは存在しているかどうか、およびアクセス権限を持っているかどうかを確認します        |
| [List Multipart Uploads](https://cloud.tencent.com/document/product/436/7736) | マルチパートアップロードを照合します    | 進行中のマルチパートアップロード情報を照合します              |
| [PUT Bucket](https://cloud.tencent.com/document/product/436/7738) | バケットを作成します     | 指定されたアカウント下に、1つのバケットを作成します             |
| [PUT Bucket acl](https://cloud.tencent.com/document/product/436/7737) | バケットACLを設定します | バケットのACLを設定します           |
| [PUT Bucket cors](https://cloud.tencent.com/document/product/436/8279) | クロスオリジン構成を設定します    | バケットのクロスオリジンアクセス権限を設定します         |
| [PUT Bucket lifecycle](https://cloud.tencent.com/document/product/436/8280) | ライフサイクルを設定します    | バケットライフサイクル管理の構成を設定します                 |
| [ PUT Bucket policy](https://cloud.tencent.com/document/product/436/8282) | バケットポリシーを設定します |指定されたバケットの権限ポリシーを設定します|

## オブジェクト操作について

| API                                      | 操作名      | 操作説明                                 |
| ---------------------------------------- | -------- | ------------------------------------ |
| [Abort Multipart Upload](https://cloud.tencent.com/document/product/436/7740) | マルチパートアップロードを終了します   | 1つのマルチパートアップロード操作を終了し、アップロードされたパートを削除します                 |
| [Complete Multipart Upload](https://cloud.tencent.com/document/product/436/7742) | マルチパートアップロードを完成します    | ファイル全体のマルチパートアップロードを完成します              |
| [DELETE Multiple Object](https://cloud.tencent.com/document/product/436/8289) | 複数オブジェクトを削除します   | バケットの中で、オブジェクト（ファイル/オブジェクト）を一括削除します        |
| [DELETE Object](https://cloud.tencent.com/document/product/436/7743) | 単一オブジェクトを削除します   | バケットの中で、指定されたオブジェクト（ファイル/オブジェクト）を削除します        |
| [GET Object](https://cloud.tencent.com/document/product/436/7753) | オブジェクトを取得します     | 1つのオブジェクト（ファイル/オブジェクト）をローカルにダウンロードします                |
| [GET Object acl](https://cloud.tencent.com/document/product/436/7744) | オブジェクトACLを取得します | オブジェクト（ファイル/オブジェクト）のACLを取得します           |
| [HEAD Object](https://cloud.tencent.com/document/product/436/7745) | オブジェクトのメタデータを取得します  | オブジェクトのメタ情報を取得します                  |
| [Initiate Multipart Upload](https://cloud.tencent.com/document/product/436/7746) | マルチパートアップロードを初期化します  | マルチパートアップロードのアップロード操作を初期化します            |
| [List Parts](https://cloud.tencent.com/document/product/436/7747) | アップロード済みパートを照合します     | 特定のマルチパートアップロード操作でのアップロード済みパートを照合します                    |
| [Options Object](https://cloud.tencent.com/document/product/436/8288) | プリフライトリクエストのクロスオリジン構成   | プリフライトリクエストを使用して、実際のクロスオリジンリクエストを送信できるかどうかを確認します                    |
|[POST Object](https://cloud.tencent.com/document/product/436/14690) |  フォームアップロードオブジェクト | フォームを使用してアップロードオブジェクトをリクエストします |
|[POST Object restore](https://cloud.tencent.com/document/product/436/12633) | アーカイブオブジェクトの回復 | アーカイブタイプのオブジェクトを取り戻し、アクセスします |
| [PUT Object](https://cloud.tencent.com/document/product/436/7749) | アップロードオブジェクト     | 1つのオブジェクト（ファイル/オブジェクト）をバケットにアップロードします         |
| [PUT Object acl](https://cloud.tencent.com/document/product/436/7748) | オブジェクトACLを設定します | バケットのあるオブジェクト（ファイル/オブジェクト）のACLを設定します             |
| [PUT Object - Copy](https://cloud.tencent.com/document/product/436/10881) | オブジェクトコピーを設定します     | ファイルをターゲットパスにコピーします                   |
| [Upload Part](https://cloud.tencent.com/document/product/436/7750) | マルチパートアップロード     | ファイルをマルチパートアップロードします                               |
| [Upload Part - Copy](https://cloud.tencent.com/document/product/436/8287) | パートのコピー |  既存のオブジェクトを新しいオブジェクトのパートにコピーします|

