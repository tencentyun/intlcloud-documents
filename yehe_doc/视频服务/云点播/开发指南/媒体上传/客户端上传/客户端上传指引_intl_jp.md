## 操作シナリオ
クライアントからのビデオアップロードとは、AppのエンドユーザーがローカルビデオをVODプラットフォームにアップロードすることです。フローチャートは次のとおりです。ここでは、クライアントを使用してビデオをアップロードする方法をご説明します。
![](https://main.qcloudimg.com/raw/b92eb9f4b61aa7f3605e3a372ace494e.png)

## 前提条件

#### 1. サービスのアクティブ化

VODサービスをアクティブ化します。詳細については、[購入ガイドライン](https://intl.cloud.tencent.com/document/product/266/39506)をご参照ください。

#### [](id:p3)2. Tencent Cloud APIキーの取得
 
サーバーAPIの呼び出しに必要なセキュリティ証明（SecretIdとSecretKey）を取得します。具体的な手順は次のとおりです。
1. コンソールにログインし、【クラウド製品】>【CAM】>[【APIキー管理】](https://console.cloud.tencent.com/cam/capi)を選択し、「APIキー管理」ページに進みます。
2. Tencent Cloud APIキーを取得します。キーを作成していない場合は、【キーの作成】をクリックして、SecretIdとSecretKeyのペアを作成することができます。
  
## 操作手順
### 1. アップロード用署名の申請
クライアントは、アップロード署名をAppの署名配布サーバーに申請する必要があります。署名の生成手順については、[クライアントからのアップロード署名](https://intl.cloud.tencent.com/document/product/266/33922) をご参照ください。さまざまな言語で署名を生成する例については、以下をご参照ください。
- [PHP署名の例](https://intl.cloud.tencent.com/document/product/266/33923)
- [Java署名の例](https://intl.cloud.tencent.com/document/product/266/33923)
- [Node.js署名の例](https://intl.cloud.tencent.com/document/product/266/33923)
- [C#署名の例](https://intl.cloud.tencent.com/document/product/266/33923)
- [Python署名の例](https://intl.cloud.tencent.com/document/product/266/33923)

>?
>- クライアントからのアップロードは、クライアントからVODプラットフォームにビデオファイルを直接アップロードします。Appサーバーで中継する必要がないため、VODはリクエストを開始するクライアントを必ず認証する必要があります。
>- 重大なセキュリティの問題を回避するため、Appは最終的なアクセス許可を持つSecretKeyをクライアントに開示しないようにします。クライアントはアップロードを開始する前にアップロード署名を申請する必要があります。


### 2. SDKを使用したビデオのアップロード

VODは、クライアントからビデオを手軽にアップロードできるよう、顧客アクセスを容易にするマルチプラットフォームのSDKを提供しています。詳細については、以下をご参照ください。
- [AndroidのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33925)
- [iOSのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33926)
- [WebのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33924)

#### よくあるご質問 
- **ビデオのアップロード完了後、どのようにしてトランスコードを自動的に開始しますか。
クライアントからアップロードするための署名の`procedure`パラメータを介して、ビデオのアップロードが完了した後の処理方法を指定します。詳細については、[アップロード時のタスクフロー指定]( #p1) をご参照ください。
- **Appバックエンドはビデオのアップロード完了通知を受信したとき、どのクライアントがアップロードしたのか、どうすれば特定できますか**。
クライアントからアップロードするための署名に、`sourceContext`パラメータを追加して、ユーザーID情報を伝達できます。アップロード完了通知は、このパラメータをAppバックエンドに渡します。詳細については、[イベントの通知](#p2)をご参照ください。

### [](id:p2)3. イベントの通知

ビデオのアップロードが完了すると、VODはAppバックエンドに [イベント通知 - ビデオアップロード完了](https://intl.cloud.tencent.com/document/product/266/33950) を開始します。Appバックエンドは、このイベントを通じてビデオのアップロード動作を認識することができます。イベント通知を受信するには、Appは [コンソール - コールバック設定](https://console.cloud.tencent.com/vod/callback) に移動してイベント通知を有効にする必要があります。[イベント通知 - ビデオアップロード完了](https://intl.cloud.tencent.com/document/product/266/33950) には、主に次の情報が含まれています。
- 新しいビデオファイルのFileIdとURL。
- VODは、ビデオアップロード時のパススルーフィールドの指定をサポートしており、イベントが完了すると、パススルーフィールドはAppバックエンドに送信されます。イベント通知には、次のフィールドが含まれています。
	- `SourceType`：このフィールドはTencent Cloudにより`ServerUpload`に固定されています。アップロードソースがサーバーからのアップロードであることを意味します。
	- `SourceContext`：ユーザー定義のパススルーフィールドです。署名の配布中にAppバックエンドに指定されます。これは署名の`sourceContext`パラメータに対応します。
- VODでは、ビデオアップロード完了時にビデオ処理を自動的に開始する機能をサポートしています。アップロード時に[ビデオ処理タスクフロー](https://intl.cloud.tencent.com/document/product/266/33931)を指定すると、イベント通知の内容にタスクID、すなわちイベント通知の中の`data.procedureTaskId`フィールドが添付されてきます。

詳細については、以下をご参照ください。
- [タスク管理とイベント通知](https://intl.cloud.tencent.com/document/product/266/33931)
- [イベント通知 - ビデオアップロード完了](https://intl.cloud.tencent.com/document/product/266/33950)

## 高度な機能

- ### [](id:p1) アップロード時のタスクフローの指定
開発者がビデオのアップロード完了後に[ビデオ処理タスクフロー](https://intl.cloud.tencent.com/document/product/266/33931)（例：トランスコード、スクリーンキャプチャなど）を自動的に開始したい場合は、[アップロード署名](https://intl.cloud.tencent.com/document/product/266/33922)の生成時に`procedure`パラメータによって実現することができ、パラメータの値をタスクフローテンプレート名にします。VODでは[タスクフローテンプレートの作成](https://intl.cloud.tencent.com/document/product/266/14058)およびテンプレートの命名をサポートし、タスクフローの開始時に、タスクフローテンプレート名によって開始が必要なタスクを示すことができます。
- ### アップロード時のストレージリージョンの指定
VODがデフォルトで提供するストレージリージョンは、シンガポール に設定されています。その他のエリアに保存したい場合は、コンソール上でご自身でその他ストレージリージョンを追加することができます。詳細については、[アップロードストレージ設定](https://intl.cloud.tencent.com/document/product/266/18874)をご参照ください。設定完了後、[アップロード署名](https://intl.cloud.tencent.com/document/product/266/33922)の生成時に`storageRegion`パラメータによって指定でき、パラメータの値をストレージリージョンの[英語の略称](https://intl.cloud.tencent.com/document/product/266/9760)にします。
- ### アップロード時のカバー追加
VODでは、アップロードSDKインターフェースに関連するカバーへのパスを入力することで、カバー付きのビデオをアップロードできます。詳細については、以下をご参照ください。
	- [AndroidのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33925)
	- [iOSのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33926)
	- [WebのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33924)
- ### [](id:p4)ワンタイム署名
ビデオのアップロード中に、Appのバックエンドによって配布された署名は、デフォルトで有効期間中、複数回使用できます。Appにビデオアップロードのセキュリティに関する高い要件がある場合は、ワンタイム署名を指定することができます。
ワンタイム署名の使用方法：Appのバックエンドが署名を配布するときに、パラメータ`oneTimeValid`を1に指定する必要があります。詳細については、[クライアントからのアップロード署名](https://intl.cloud.tencent.com/document/product/266/33922)をご参照ください。
>?ワンタイム署名は1回しか使用できないため、この署名方式はより安全にはなりますが、Appで規定外のエラー処理が必要となります。例えば、アップロードにエラーが発生した場合、簡単にSDKを再利用してビデオをアップロードできず、アップロード署名も再度申請する必要があります。
- ### 中断からの再開
ビデオのアップロード中にアップロードが予期せず終了した場合、中断したポイントからファイルを再度アップロードできます。
>?中断からの再開の有効期限は1日です。つまり同じビデオのアップロードが中断された場合、1日以内に再度アップロードすると中断ポイントからそのままアップロードできます。1日を超えるとデフォルトでは、完全なビデオを再度アップロードします。
>
Appで中断からの再開機能を有効にする方法は、次のとおりです。
	- [AndroidのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33925)、アップロード時に`enableResume`フィールドをTrueに設定します。
	- [iOSのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33926)、アップロード時に`enableResume`フィールドをTrueに設定します。
	- [WebのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33924)、中断からの再開は組み込まれており、ユーザーによる操作は不要です。
- ### アップロードの一次停止/再開/キャンセル
VOD SDKでは、ビデオのアップロード中に、アップロードの一時停止、再開またはキャンセルをすることができます。詳細については、以下をご参照ください。
	- [AndroidのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33925)
	- [iOSのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33926)
	- [WebのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33924)
