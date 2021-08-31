>!ここでは主に**Tencent Real-Time CommunicationTRTC **のCloud Access Management（CAM）機能関連コンテンツについて紹介します。他製品のCAM関連コンテンツについては、[CAMサポート製品](https://intl.cloud.tencent.com/document/product/598/10588)をご参照ください。

TRTCのCAMは、実質的にはサブアカウントをポリシーにバインドするか、またはポリシーをサブアカウントに付与します。開発者は、コンソールのプリセットポリシーを直接使用して、いくつかの簡単な承認操作を行うことができます。複雑な権限付与の操作については、[カスタムポリシー](https://intl.cloud.tencent.com/document/product/647/39551)をご参照ください。

TRTCは現在、次のようなプリセットポリシーを提供しています。

|        ポリシー名         |       ポリシーの説明      |
| --------------------- | ------------------ |
|   QcloudTRTCFullAccess   | TRTCへの完全な読み取り/書き込みアクセス権限 |
| QcloudTRTCReadonlyAccess |  TRTCへの読み取り専用アクセス権限  |

## プリセットポリシー使用例


### TRTCへの完全な読み取り/書き込みアクセス権限を有するサブアカウントの作成[](id:new)

1. Tencent Cloud[ルートアカウント](https://intl.cloud.tencent.com/document/product/598/32633)として、CAMコンソールの[【ユーザーリスト】](https://console.cloud.tencent.com/cam)にアクセスし、【ユーザーの作成】をクリックします。
2. 「ユーザーの作成」ページで【カスタム作成】を選択し、「サブユーザーの作成」ページに進みます。
	
	>? CAM[サブユーザーのカスタム作成](https://intl.cloud.tencent.com/document/product/598/13674)の操作ガイドに従って、「ユーザー権限の設定」までの手順を完了してください。
3. 「ユーザー権限の設定」ページにおいて、次の事項を実施します。
   1. プリセットポリシー`QcloudTRTCFullAccess`を検索してチェックを入れます。
   2. 【次のステップ】をクリックします。
4. 「情報と権限のチェック」フィールドの下にある【完了】をクリックして、サブユーザーの作成を完了します。成功ページで、サブユーザーのログインリンクとセキュリティ証明書をダウンロードして保管します。そこには、次のような情報が含まれます。
<table>
     <tr>
         <th nowrap="nowrap">情報</th>  
         <th nowrap="nowrap">ソース</th>  
         <th nowrap="nowrap">機能</th>  
         <th nowrap="nowrap">保存が必須かどうか</th>  
     </tr>
	 <tr>      
         <td>ログインリンク</td>   
	     <td>ページでコピー</td>   
	     <td nowrap="nowrap">コンソールにログインするのに有用、ルートアカウントを入力する手順を省略</td>   
	     <td>いいえ</td>
     </tr> 
	 <tr>      
         <td nowrap="nowrap">ユーザー名</td>   
	     <td>セキュリティ証明書CSVファイル</td>   
	     <td>コンソールにログインする時に入力</td>   
	     <td>はい</td>
     </tr> 
	 <tr>      
         <td>パスワード</td>   
	     <td>セキュリティ証明書CSVファイル </td>   
	     <td >コンソールへのログイン時に入力</td>   
	     <td >はい</td>
     </tr> 
		  <tr>      
         <td>SecretId</td>   
	     <td>セキュリティ証明書CSVファイル</td>   
	     <td >サーバーAPI呼び出し時に使用します。詳細は<a href="https://intl.cloud.tencent.com/document/product/598/32675">アクセスキー</a> をご参照ください< /td>   
	     <td >はい</td>
     </tr> 
	     <tr>      
         <td>SecretKey</td>   
	     <td>セキュリティ証明書CSVファイル</td>   
	     <td >サーバーAPI呼び出し時に使用します。詳細は<a href="https://intl.cloud.tencent.com/document/product/598/32675">アクセスキー</a> をご参照ください</td>   
	     <td >はい</td>
     </tr> 
</table>
5. 前述のログインリンクとセキュリティ証明書を許可された当事者に提供します。許可された当事者は、サブユーザーを使用して、TRTCコンソールへのアクセスやTRTCサーバーAPIのリクエストなど、TRTCでのすべての操作を実行できます。

### TRTCへの完全な読み取り/書き込みアクセス権限を既存のサブアカウントに付与[](id:FullRW)

1. Tencent Cloud[ルートアカウント](https://intl.cloud.tencent.com/document/product/598/32633)として、CAMコンソールの[【ユーザーリスト】](https://console.cloud.tencent.com/cam)にアクセスし、権限を付与したいサブアカウントをクリックします。
2. 「ユーザー詳細」ページの権限フィールドで、【ポリシーの追加】をクリックします。サブアカウントの権限が空でない場合は、【ポリシーの関連付け】をクリックします。
3. 【ポリシーリストからポリシーの関連付けを選択】を選択し、プリセットポリシー`QcloudTRTCFullAccess`を検索しチェックを入れます。その後、ページのプロンプトに従って承認プロセスを完了してください。

### サブアカウントのTRTCへの完全な読み取り/書き込みアクセス権限を解除[](id:new)


1. Tencent Cloud[ルートアカウント](https://intl.cloud.tencent.com/document/product/598/32633)として、CAMコンソールの[【ユーザーリスト】](https://console.cloud.tencent.com/cam)にアクセスし、権限を解除したいサブアカウントをクリックします。
2. 「ユーザー詳細」ページの権限タブでプリセットポリシー`QcloudTRTCFullAccess`を検索し、右側の【解除】をクリックします。プロンプトに従って承認解除プロセスを完了してください。
