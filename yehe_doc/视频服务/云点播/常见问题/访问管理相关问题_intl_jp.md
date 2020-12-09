### ファイルをアップロードするにはどんな権限が必要ですか。

VODでは、以下の方法でファイルをアップロードできます。[Upload from Server](https://intl.cloud.tencent.com/document/product/266/33912)、[Upload from Client](https://intl.cloud.tencent.com/document/product/266/33921) 、[PullUpload](https://intl.cloud.tencent.com/document/product/266/34118) 。アップロードに必要な権限は次のとおりです。


| アップロード方法   |リソースアクセス権限     | 操作権限                                                     | 備考               |
| ---------- | ------------ | ------------------------------------------------------------ | ------------------ |
| Upload from server | Specified subapplication | [ApplyUpload](https://intl.cloud.tencent.com/document/product/266/34120)<br/>[CommitUpload](https://intl.cloud.tencent.com/document/product/266/34119) | -                  |
| Upload from client | Specified subapplication | [ApplyUpload](https://intl.cloud.tencent.com/document/product/266/34120)<br/>[CommitUpload](https://intl.cloud.tencent.com/document/product/266/34119) | -                  |
| Pull from URL   | Specified subapplication | [PullUpload](https://intl.cloud.tencent.com/document/product/266/34118)                      | -                  |
| LVB recording   | All subapplications   | -                                                            | LVBレコーディング機能を有効にする必要があります |

>VODコンソールでのビデオの [Local upload](https://intl.cloud.tencent.com/document/product/266/33890#.E6.9C.AC.E5.9C.B0.E4.B8.8A.E4.BC.A0.E6.AD.A5.E9.AA.A4)は、 クライアントからのアップロードとなります。

### サーバーからのアップロードで「権限なし」というエラーが返されますが、他の方法で正常にアップロードできるのはなぜですか。

サーバーSDKのバージョンが古すぎる可能性があります。最新版の[SDK](https://intl.cloud.tencent.com/document/product/266/33912#1.-.E5.8F.91.E8.B5.B7.E4.B8.8A.E4.BC.A0)にアップグレードしてください。

### ビデオを視聴するにはどんな権限が必要ですか。

ビデオを視聴するには、基本的にVOD CDNにリクエストを送信することになり、操作者は、TencentCloudアカウントではなく通常の視聴者としてアクセスするため、操作者に権限を付与する必要はありません（[Key hotlink protection](https://intl.cloud.tencent.com/document/product/266/33984) または[Video encryption](https://intl.cloud.tencent.com/document/product/266/33968)が有効になっている場合は、ビデオを視聴する前に、対象ドキュメントに記載されている要件を満たす必要がありますが、これらはアクセス管理と関係がありません）。

### 特定のファイルに対する権限を付与できますか。

できません。VODアクセス管理のリソース粒度はサブアプリケーションです。

### 権限設定が競合している場合はどうなりますか。

競合した場合、以下の利用が考えられます。

- 1つのカスタムポリシーには、説明が競合する複数のステートメントが含まれています（たとえば、1つのステートメントはリソースへのアクセスを許可しますが、別のステートメントでは同一リソースへのアクセスを拒否します）。
- 1つのサブユーザーは、説明が競合する複数のポリシーにバインドされています。

VODの権限管理はCAMに基づいているため、権限はCAMのポリシー[Evaluation Logic](https://intl.cloud.tencent.com/document/product/598/10605)に従って決定されます。

### VODはクロスアカウントのリソースアクセスをサポートしていますか。

クロスアカウントのリソースアクセスとは、ルートアカウントAがルートアカウントB（またはそのサブアカウント）にVOD権限のすべてまたは一部を付与することを示します。つまり、付与者と被付与者はそれぞれ独立したTencent Cloudアカウントとなります。VODは、クロスアカウントのリソースアクセスを**サポートしていません**。つまり、1つのTencent Cloudアカウントは、自身のサブアカウントにのみVODアクセス権限を付与できます。
