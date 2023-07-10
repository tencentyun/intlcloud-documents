## 概要

Cloud Object Storage（COS）はデータをデータセンター内のディスクに書き込む前に、オブジェクトレベルでデータの暗号化を適用する保護ポリシーをサポートしています。データはアクセス時に自動的に復号されます。暗号化と復号の操作プロセスはサーバー側で完了します。このサーバー側での暗号化機能によって静的データを有効に保護することができます。

>!
> - 暗号化されたオブジェクトと暗号化されていないオブジェクトへのアクセスに体験上の違いはありません。ただしユーザーがオブジェクトへのアクセス権限を持っていることが前提です。
> - サーバー側での暗号化はオブジェクトデータのみを暗号化するものであり、オブジェクトメタデータの暗号化は行いません。またサーバー側で暗号化したオブジェクトには有効な署名を使用してアクセスする必要があり、匿名ユーザーはアクセスできなくなります。
> 

## ユースケース

- **プライベートデータストレージのケース：**プライベートデータのストレージについては、サーバー側での暗号化は、保存されているデータに対して行うことができます。ユーザーのプライバシーは保証され、ユーザーがアクセスした際は自動的に復号されます。
- **プライベートデータ転送のケース：**プライベートデータの転送については、COSはHTTPSを使用してデプロイしたSSL証明書を提供して暗号化機能を実現します。転送リンクレイヤー上に暗号化レイヤーを設け、データの転送過程でのハッキングや改ざんを確実に防止します。

## 暗号化方式
COSがサポートしているサーバー側の暗号化方式はSSE-COS、SSE-KMS、SSE-Cです。ユーザーはご自身に合った暗号化方式を選択し、COSに保存したデータの暗号化を行うことができます。

### SSE-COSの暗号化

SSE-COS暗号化は、COSホストキーによるサーバー側の暗号化です。Tencent Cloud COSはマスターキーをホストし、データを管理します。ユーザーはCOSによってデータの管理と暗号化を直接行います。SSE-COSは多要素による強力な暗号化を採用し、一意のキーを使用して各オブジェクトを暗号化し、同時に256ビットの高度な暗号化（AES-256）を用いてデータを暗号化するほか、マスターキーの定期的なローテーションによってキー自体の暗号化を行うことができます。

>!
>- `POST`操作を使用してオブジェクトのアップロードを行う際は、フォームのフィールドで、`x-cos-server-side-encryption`ヘッダーではなく、同一の情報を提供する必要があります。詳細については、[POST Object](https://intl.cloud.tencent.com/document/product/436/14690)をご参照ください。
>- 署名付きURLを使用してアップロードしたオブジェクトについては、SSE-COS暗号化を使用できません。COSコンソールまたはHTTPリクエストヘッダーを使用してサーバー側での暗号化を指定することのみ可能です。

#### COSコンソールの使用
コンソール上でオブジェクトのSSE-COS暗号化を行う方法について詳しくお知りになりたい場合は、[オブジェクト暗号化の設定](https://intl.cloud.tencent.com/document/product/436/30929)コンソールドキュメントをご参照ください。

#### REST APIの使用

>!
>- バケット内のオブジェクトをリストアップする際、オブジェクトが暗号化されているかどうかにかかわらず、すべてのオブジェクトのリストが返されます。
>- POSTを使用してオブジェクトのアップロード操作を行う際は、フォームのフィールドで、このリクエストヘッダーではなく、同一の情報を提供してください。詳細については、[POST Object](https://intl.cloud.tencent.com/document/product/436/14690)をご参照ください。

ユーザーが次のインターフェースをリクエストする場合は、`x-cos-server-side-encryption`ヘッダーを提供することでサーバー側の暗号化を適用することができます。詳細については、[パブリックリクエストヘッダー - SSE-COS](https://intl.cloud.tencent.com/document/product/436/7728)をご参照ください。

- [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)
- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
- [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)
- [POST Object](https://intl.cloud.tencent.com/document/product/436/14690)

### SSE-KMSの暗号化

SSE-KMS暗号化は、KMSホストキーによるサーバー側の暗号化です。KMSはTencent Cloudが推進するセキュリティ管理系サービスの1つであり、サードパーティ認証を経たハードウェアセキュリティモジュールHSM（Hardware Security Module）を使用してキーの生成と保護を行うものです。ユーザーがキーの作成と管理を手軽に行えるよう支援し、複数のアプリケーションや複数の業務でのキー管理のニーズを満たすとともに、規制とコンプライアンスの要件にも適合します。

SSE-KMS暗号化を初めて使用する際は、[KMSサービスのアクティブ化](https://intl.cloud.tencent.com/pricing/kms?lang=en&pg=)を行う必要があります。KMSサービスをアクティブ化すると、システムは自動的にデフォルトのマスターキー（CMK）1個を作成します。または[KMSコンソール](https://console.cloud.tencent.com/kms2)で自らキーを作成し、キーのポリシーと使用方法を定義することもできます。KMSでは、ユーザーがキー素材のソースを**KMS**または**外部**から自ら選択することができます。その他の情報については、[キーの作成](https://intl.cloud.tencent.com/document/product/1030/31971)および[外部キーのインポート](https://intl.cloud.tencent.com/document/product/1030/32795)をご参照ください。

>!
> - SSE-KMSはオブジェクトデータのみを暗号化し、オブジェクトメタデータは一切暗号化しません。
> - SSE-KMSは現在、北京、上海、中国香港、広州リージョンのみサポートしています。
> - SSE-KMS暗号化の使用には別途料金が発生し、KMSによって課金されます。詳細については、[KMS課金概要](https://intl.cloud.tencent.com/document/product/1030/31966)をご参照ください。
> - SSE-KMS暗号化を使用したオブジェクトには有効な署名を使用してアクセスする必要があり、匿名ユーザーはアクセスできなくなります。

#### COSコンソールの使用

コンソール上でオブジェクトのSSE-KMS暗号化を行う方法について詳しくお知りになりたい場合は、[オブジェクト暗号化の設定](https://intl.cloud.tencent.com/document/product/436/30929)コンソールドキュメントをご参照ください。

#### REST APIの使用

>!
>
>- バケット内のオブジェクトをリストアップする際、オブジェクトが暗号化されているかどうかにかかわらず、すべてのオブジェクトのリストが返されます。
>- POSTを使用してオブジェクトのアップロード操作を行う際は、フォームのフィールドで、このリクエストヘッダーではなく、同一の情報を提供してください。詳細については、[POST Object](https://intl.cloud.tencent.com/document/product/436/14690)をご参照ください。

ユーザーが次のインターフェースをリクエストする場合は、`x-cos-server-side-encryption`ヘッダーを提供することでサーバー側の暗号化を適用することができます。詳細については、[パブリックリクエストヘッダー - SSE-KMS](https://intl.cloud.tencent.com/document/product/436/7728)をご参照ください。

- [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)
- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
- [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)
- [POST Object](https://intl.cloud.tencent.com/document/product/436/14690)

#### 注意事项
**COSコンソール**を使用してSSE-KMS暗号化を行ったことがなく、**API**方式のみを使用してSSE-KMS暗号化を行っている場合は、まず[CAMロール](https://intl.cloud.tencent.com/document/product/598/19420)を作成する必要があります。具体的な作成手順は次のとおりです。
1. CAMコンソールにログインし、[ロール](https://console.cloud.tencent.com/cam/role)リストページに進みます。
2. **ロールの新規作成**をクリックし、**Tencent Cloud製品サービス**をロールエンティティとして選択します。
3. ロールをサポートするサービスは**COS**を選択し、**次のステップ**をクリックします。
4. ロールポリシーを設定します。**QcloudKMSAccessForCOSRole**を検索してチェックを入れ、**次のステップ**をクリックします。
![](https://main.qcloudimg.com/raw/b3d8ef7f3c534f33207c47b7fb7725fb.png)
5. ロールのタグキーとタグ値をマークし、**次のステップ**をクリックします。
6. 指定のロール名：COS_QcsRoleを入力します。
7. 最後に**完了**をクリックすれば作成は終了です。

### SSE-Cの暗号化

SSE-C暗号化は、ユーザー定義キーによるサーバー側の暗号化です。暗号化鍵はユーザーが提供し、COSはユーザーがオブジェクトをアップロードする際に、ユーザーが提供した暗号化鍵のキーペアを使用して、ユーザーのデータをAES-256で暗号化します。

>!
>- COSはユーザーが提供した暗号化鍵を保存せず、暗号化鍵にランダムデータを追加したHMAC値を保存します。この値はオブジェクトにアクセスするためのユーザーのリクエストの検証に使用されます。COSは、ランダムデータのHMAC値を使用して暗号化鍵の値を推測したり、暗号化されたオブジェクトの内容を復号したりすることはできません。そのため、ユーザーが暗号化鍵を紛失した場合、このオブジェクトを再取得できなくなります。
>- POST操作を使用してオブジェクトのアップロードを行う際は、フォームのフィールドで、`x-cos-server-side-encryption-*`ヘッダーではなく、同一の情報を提供する必要があります。詳細については、[POST Object](https://intl.cloud.tencent.com/document/product/436/14690)をご参照ください。
>- SSE-CはAPIでしか使用できず、コンソールでの操作はサポートされていません。

#### REST APIの使用

ユーザーが次のインターフェースをリクエストする場合は、PUTおよびPOSTリクエストについては`x-cos-server-side-encryption-*`ヘッダーを提供することでサーバー側の暗号化を適用することができます。GETおよびHEADでSSE-C暗号化を使用したオブジェクトをリクエストする場合は、`x-cos-server-side-encryption-*`ヘッダーを提供して指定のオブジェクトの復号を行う必要があります。詳細については、[パブリックリクエストヘッダー - SSE-C](https://intl.cloud.tencent.com/document/product/436/7728)をご参照ください。このヘッダーをサポートしている操作は次のとおりです。

- [GET Object](https://intl.cloud.tencent.com/document/product/436/7753)
- [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745)
- [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)
- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
- [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750)
- [POST Object](https://intl.cloud.tencent.com/document/product/436/14690)
- [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)

