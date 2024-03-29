## 1\. **背景**

本モジュールは、お客様が顧客IDおよびアクセス管理（CIAM）（以下「**機能**」といいます）を使用する場合に適用されます。本モジュールは、（「[DPSA](https://intl.cloud.tencent.com/document/product/301/17347 )」）に掲載されているData Processing and Security Agreement（データ処理およびセキュリティに関する契約）に組み込まれます。本モジュールにおける用語のうち本書内に定義のないものは、DPSA内で定義された意味を有するものとします。DPSAと本モジュールとの間に矛盾がある場合には、その不一致の範囲で本モジュールを優先するものとします。


## 2\. **処理**

当社は、本機能に関連して以下のデータを処理します：

| **個人情報**                                     | **用途**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **ユーザー管理構成データ：** お客様が決定したプリセットユーザー属性（説明、国籍、ユーザーポジション、誕生日、性別、住所）、ユーザーグループ（ユーザーグループリスト、名前、備考、作成時刻、含まれるユーザーリスト）。 | 当社は、お客様への本機能の提供という目的の範囲で、これらのデータを処理します。<br/>  このデータは、弊社のTencentBD for MongoDB（MongoDB）および機能と統合、保存、バックアップされ、弊社のTencentDB for  Redis（Redis）機能とも統合されることに注意してください。 |
| **アプリケーション管理データ：** <br><li>M2Mアプリケーション：アイコン、アプリケーション名、アプリケーションタイプ、業界、クライアントID、パスワードキー、アプリケーション記述、アクセストークンの有効性、セキュリティ・ドイン、およびCORS の固有設定済みURI。<br><li>ミニプログラムアプリケーション： スタイルのアプリケーションダウンロード、構成ガイド、アイコン、アプリケーション名、アプリケーションタイプ、業界、クライアントID、パスワードキー、アプリケーション記述、リダイレクトURI、ログアウトリダイレクトURI、アクセストークンの有効性、リフレッシュトークン、クレーム、登録およびログインプロセス構成、セキュリティドメインCORS固有構成URI。<br><li>モバイルアプリ：アイコン、アプリケーション名、アプリケーションタイプ、業界、クライアントID、パスワードキー、アプリケーション記述、リダイレクトURI、ログアウトリダイレクトURI、アクセストークンの有効性、リフレッシュトークン、クレーム、登録処理、ログインプロセス、MFA処理、パスワード忘却処理、ユーザー名忘却処理、プロトコル管理、セキュリティドメインCORS固有構成URI。<br><li>Web アプリケーションおよび Web アプリケーション：アイコン、アプリケーション名、アプリケーションタイプ、業界、クライアントID、パスワードキー、アプリケーション記述、リダイレクトURI、ログアウトリダイレクトURI、アクセストークンの有効性、リフレッシュトークン、クレーム、登録処理、ログインプロセス、MFA処理、パスワード忘却処理、ユーザー名忘却処理、プロトコル管理、セキュリティドメインCORS固有構成URI。| 当社は、お客様への本機能の提供という目的の範囲で、これらのデータを処理します。   <br/> このデータは、Cloud Object  Storage（COS）およびMongoDBの機能と統合、保存、バックアップされますのでご注意ください。 |
| **データ同期設定データ：** データソース名、データソースID、説明、設定ガイド、クライアントID、クライアントパスワードキー、トークン、ユーザーURL、グループURL。 | 当社は、お客様への本機能の提供という目的の範囲で、これらのデータを処理します。<br/> このデータは、MongoDBの機能と統合、保存、バックアップされますのでご注意ください。 |
| **証明書管理データ：** <br><li>一般的な認証ソース：認証ソースアイコン、認証ソース名、認証ソース属性、認証ソースの説明、パスワードポリシー、SMS検証コードの長さ、SMS検証コードの有効期間、電子メール検証コードの長さ、電子メール検証コードの有効期間。  <br><li>ソーシャル認証ソース：認証ソースアイコン、認証ソース名、認証ソースの説明、AppID、アプリパスワードキー、属性マッピング。| 当社は、お客様への本機能の提供という目的の範囲で、これらのデータを処理します。<br/> このデータは、弊社のCOSおよびMongoDB の機能と統合、保存、バックアップされていることにご注意ください。弊社のショートメッセージサービス（SMS）およびシンプルメールサービス（SES）サービスを購入された場合、一般認証ソースデータは、弊社のSMSおよびSES機能にも統合されます。 |
| **個人化データ：** <br><li>ドメイン名設定：お客様が設定および提供したドメイン名（または必要に応じて、 弊社が提供する標準ドメイン名）。<br><li>テンプレート設定（SMS および/またはSES機能を使用するオプションに関する構成設定）：SMS テンプレート（SMSサーバ、SMSログイン署名、SMSテンプレートID）、メールボックステンプレート（電子メールサーバー、確認コードテンプレートID、パスワードテンプレートID、ユーザー名テンプレートIDの取得）。<br><li>実名認証テンプレート（実名認証サービスプロバイダ、API発信者のセキュリティ資格情報（秘密ID、秘密キー））。 | 当社は、お客様への本機能の提供という目的の範囲で、これらのデータを処理します。<br/> このデータは、MongoDBの機能と統合、保存、バックアップされますのでご注意ください。弊社のSMSおよびSESサービスを購入された場合、テンプレート設定データは、弊社のSMSおよびSES機能にも統合されます。 |
| **内蔵ユーザー属性データ：** 間違ったログイン時間、ロック時間、AlipayユーザーID、電子メールアドレス、更新時間、ユーザータイムゾーン、地理的位置、最新のログイン時刻、電話番号、作成時間、ユーザーグループ、ユーザープール、ユーザーニックネーム、ユーザーID、ユーザー名、WeChatオープンID、初めてログインしたかどうか、ユーザーソース、Wechatunion ID、ユーザーステータス、QQ open ID、QQunion ID、実名認証を持っているかどうか、実名認証方法名、ID番号、メインアカウントかどうか | 当社は、お客様への本機能の提供という目的の範囲で、これらのデータを処理します。<br/> このデータは、弊社のMongoDBおよび機能と統合、保存、バックアップされ、弊社のRedis機能にも統合されることに注意してください。弊社のSMSおよびSESサービスを購入された場合、電話番号も弊社のSMS機能と統合され、電子メールアドレスは弊社のSES機能と統合されます。 |


## 3\. **サービス地域**

DPSAに記載のとおり。


## 4\. **副処理者**

DPSAに記載のとおり。


## 5\. **データ保持**

当社は、本機能に関連して処理された個人データを以下のとおり保管します。

| **個人情報**                                     | **保持ポリシー**                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ユーザー管理構成データ  アプリケーション管理データ  データ同期設定データ  認証管理データ  個人化データ   内蔵ユーザー属性データ | 左記 データは、手動で削除するまで保持されます。あるいは、 アカウントを削除するか、機能の使用を終了すると、左記データが削除されます。 |

お客様は、DPSAに基づき、当該個人データの削除を依頼することができます。


## 6\. **特記条件**

お客様は、エンドユーザーのうち自己の個人データの処理に対して同意をすることのできる最低年齢に達している個人のみが本機能を使用するという状況を、確実なものとする必要があります。その年齢は、エンドユーザーの管轄法域によって異なることがあります。