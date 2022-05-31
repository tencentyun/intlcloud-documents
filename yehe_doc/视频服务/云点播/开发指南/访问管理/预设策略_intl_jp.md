CAMは、実質的にはサブアカウントをポリシーにバインドするか、またはポリシーをサブアカウントに付与します。開発者は、コンソールのプリセットポリシーを直接使用して、いくつかの簡単な承認操作を行うことができます。複雑な権限付与の操作については、 [カスタムポリシー](https://intl.cloud.tencent.com/document/product/266/33972)をご参照ください。

現在、VODは以下のプリセットポリシーを提供しています：

|        ポリシー名         |       ポリシーの説明      |
| :---------------------: | :------------------: |
|   QcloudVODFullAccess   | VODへの完全な読み取り／書き込みアクセス権限 |
| QcloudVODReadonlyAccess |  VODへの読み取り専用アクセス権限  |

## プリセットポリシー使用例


### VODへの完全な権限を持つサブユーザーの作成

1. [ルートアカウント](https://intl.cloud.tencent.com/document/product/598/32633)として、CAMコンソールの[【ユーザーリスト】](https://console.cloud.tencent.com/cam)にアクセスし、【ユーザーの作成】をクリックします。
   ![](https://main.qcloudimg.com/raw/e700947b468ef25d4bf70ad1fecc6348.png)
2. 「ユーザーの作成」ページでサブユーザータイプの【カスタム作成】を選択し、「サブユーザーの作成」ページに進みます。
   ![](https://qcloudimg.tencent-cloud.cn/raw/24a4e0e0b9461bdcbc0b4ea50e3e1267.png)
3. ユーザー情報を入力します。
   - ユーザー名を入力し、【プログラムアクセス】と【Tencent Cloudコンソールアクセス】にチェックを入れ 、その他オプションを必要に応じて設定します。
   - 【次のステップ】をクリックし、ページのプロンプトに従って本人確認を完了します。
     ![](https://qcloudimg.tencent-cloud.cn/raw/389813710fb711d28bb80f2f9979cd10.png)
4. ユーザー権限を設定します。
   - プリセットポリシー`QcloudVODFullAccess`を検索してチェックを入れます。
   - 【次のステップ】をクリックします。
<img src="https://qcloudimg.tencent-cloud.cn/raw/597de21489df26315d604469d6906ec2.png" width="704">
5. 「情報と権限のチェック」フィールドの下にある【完了】をクリックして、サブユーザーの作成を完了します。成功ページで、サブユーザーのログインリンクとセキュリティ証明書をダウンロードして保管します。そこには、次のような情報が含まれます。
   ![](https://main.qcloudimg.com/raw/cc223f380730f8dbfe81caa799be2dfc.png)
<table>
     <tr>
         <th nowrap="nowrap">情報</th>  
         <th nowrap="nowrap">ソース</th>  
         <th nowrap="nowrap">作用</th>  
         <th nowrap="nowrap">保存が必須かどうか</th>  
     </tr>
	 <tr>      
         <td>ログインリンク</td>   
	     <td>ページでコピー</td>   
	     <td nowrap="nowrap">コンソールにログインするのに有用、ルートアカウントを入力する手順を省略</td>   
	     <td>いいえ</td>
     </tr> 
	 <tr>      
         <td nowrap="nowrap">ユーザー名 </td>   
	     <td>セキュリティ証明書CSVファイル</td>   
	     <td>コンソールにログインする時に入力</td>   
	     <td>はい</td>
     </tr> 
	 <tr>      
         <td>パスワード</td>   
	     <td>セキュリティ証明書CSVファイル </td>   
	     <td >コンソールへのログイン時に記入</td>   
	     <td >はい</td>
     </tr> 
		  <tr>      
         <td>SecretId</td>   
	     <td>セキュリティ証明書CSVファイル</td>   
	     <td >サーバーAPI呼び出し時に使用します。詳細は <a href="https://intl.cloud.tencent.com/document/product/598/32675">アクセスキー</a> をご参照ください< /td>   
	     <td >はい</td>
     </tr> 
	     <tr>      
         <td>SecretKey</td>   
	     <td>セキュリティ証明書CSVファイル</td>   
	     <td >サーバーAPI呼び出し時に使用します。詳細は <a href="https://intl.cloud.tencent.com/document/product/598/32675">アクセスキー</a> をご参照ください</td>   
	     <td >はい</td>
     </tr> 
</table>

上記のログインリンクとセキュリティ証明書によって、このサブユーザーを使用すると、VODですべての操作を実行できます（VODコンソールへのアクセス、VODサーバーAPIの呼び出しなど）。
>?サブユーザー作成の一般的なプロセスについては、CAMの [サブユーザーの作成](https://intl.cloud.tencent.com/document/product/598/13674) ドキュメントをご参照ください。

### <span id="p2"></span>既存のサブユーザーへのVODの完全な権限の付与

1. [ルートアカウント](https://intl.cloud.tencent.com/document/product/598/32633)として、CAMコンソールの[【ユーザーリスト】](https://console.cloud.tencent.com/cam)にアクセスし、権限を付与したいサブアカウントをクリックします。
   ![](https://main.qcloudimg.com/raw/86a75ce62dde0ba4c061975181186974.png)
2. 下図に示すように「ユーザー詳細」ページの権限タブで【ポリシーの追加】をクリックします（実際の操作では、サブアカウントの既存のアクセス許可に応じて、ページ情報が異なる場合があります。サブアカウントの権限が空でない場合は、【ポリシーの関連付け 】をクリックします）。
   ![](https://main.qcloudimg.com/raw/e775e39eec0292f31a78d5a2332d6d09.png)
3. 【ポリシーリストからポリシーの関連付けを選択】を選択し、プリセットポリシー`QcloudVODFullAccess`を検索しチェックします。その後、プロンプトに従い承認プロセスを完了してください。

### サブユーザーへのVODの完全な権限の解除

1. [ルートアカウント](https://intl.cloud.tencent.com/document/product/598/32633)として、CAMコンソールの[【ユーザーリスト】](https://console.cloud.tencent.com/cam)にアクセスし、権限を解除したいサブアカウントをクリックします。
   ![](https://main.qcloudimg.com/raw/86a75ce62dde0ba4c061975181186974.png)
2. 「ユーザー詳細」ページの権限タブでプリセットポリシー`QcloudVODFullAccess`を検索し、右側の【解除】をクリックします。プロンプトに従って承認解除プロセスを完了してください。
   <img src="https://main.qcloudimg.com/raw/4d221c52efe40913031355c877f28a47.png" width="704">
