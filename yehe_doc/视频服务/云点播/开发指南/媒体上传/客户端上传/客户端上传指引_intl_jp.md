## 操作シナリオ
クライアントからのビデオアップロードとは、AppのエンドユーザーがローカルビデオをVODプラットフォームにアップロードすることです。フローチャートは次のとおりです。ここでは、クライアントを使用してビデオをアップロードする方法をご説明します。
![](https://main.qcloudimg.com/raw/b92eb9f4b61aa7f3605e3a372ace494e.png)

## 前提条件

#### 1. サービスのアクティブ化

VODサービスをアクティブにします。

<span id = "p3"></span>
#### 2. TencentCloud APIキーの取得
 
サーバーAPIの呼び出しに必要なセキュリティ証明（SecretIdとSecretKey）を取得します。具体的な手順は次のとおりです。
1. コンソールにログインし、【クラウドサービス】>【CAM】>[【APIキー管理】](https://console.cloud.tencent.com/cam/capi)を選択し、「APIキー管理」ページに進みます。
2. Tencent Cloud APIキーを取得します。キーを作成していない場合は、【キーの作成】をクリックして、SecretIdとSecretKeyのペアを作成することができます。


## 操作手順
### 1. アップロード用署名の申請
クライアントは、アップロード署名をAppの署名配布サーバーに申請する必要があります。署名の生成手順については、[クライアントからのアップロード署名](https://intl.cloud.tencent.com/document/product/266/33922) をご参照ください。さまざまな言語で署名を生成する例については、以下をご参照ください。
- [PHP署名の例](https://intl.cloud.tencent.com/document/product/266/33923#php-.E7.AD.BE.E5.90.8D.E7.A4.BA.E4.BE.8B)
- [Java署名の例](https://intl.cloud.tencent.com/document/product/266/33923#java-.E7.AD.BE.E5.90.8D.E7.A4.BA.E4.BE.8B)
- [Node.js署名の例](https://intl.cloud.tencent.com/document/product/266/33923#node.js-.E7.AD.BE.E5.90.8D.E7.A4.BA.E4.BE.8B)
- [C#署名の例](https://intl.cloud.tencent.com/document/product/266/33923#c.23-.E7.AD.BE.E5.90.8D.E7.A4.BA.E4.BE.8B)
- [Python署名の例](https://intl.cloud.tencent.com/document/product/266/33923#python-.E7.AD.BE.E5.90.8D.E7.A4.BA.E4.BE.8B)

>?
>- クライアントからのアップロードは、クライアントからVODプラットフォームにビデオファイルを直接アップロードします。Appサーバーで中継する必要がないため、VODはリクエストを開始するクライアントを必ず認証する必要があります。
>- 重大なセキュリティの問題を回避するため、Appは最終的なアクセス許可を持つSecretKeyをクライアントに開示しないようにします。クライアントはアップロードを開始する前にアップロード署名を申請する必要があります。


### 2. SDKを使用したビデオのアップロード

VODは、クライアントからビデオを手軽にアップロードできるよう、顧客アクセスを容易にするマルチプラットフォームのSDKを提供しています。詳細については、以下をご参照ください。
- [AndroidのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33925)
- [iOSのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33926)
- [WebのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33924)

#### 高度な機能

- <span id = "p1"></span>**アップロード時のタスクフローを指定**
ビデオのアップロードが完了した後、 [ビデオ処理タスクフロー](https://intl.cloud.tencent.com/document/product/266/33931#.E4.BB.BB.E5.8A.A1.E6.B5.81) を自動的に開始する必要がある場合（トランスコード、スクリーンキャプチャなど）、[アップロード署名](h ttps://intl.cloud.tencent.com/document/product/266/33922#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0) を生成するときに`procedure`パラメータを設定することができます。パラメータ値は、タスクフローテンプレート名です。VODは、[タスクフローテンプレートの作成](https://intl.cloud.tencent.com/document/product/266/14058) をサポートし、テンプレートに名前を付けます。タスクフローを開始するときに、タスクフローテンプレート名を使用して開始するタスクを示すことができます。
- **アップロード時にストレージリージョンを指定**
VODが提供するストレージリージョンは、デフォルトで重慶に設定されています。他のリージョンに保存する必要がある場合は、コンソールで他のストレージリージョンを追加できます。詳細については、[アップロードストレージ設定](https://intl.cloud.tencent.com/document/product/266/18874) をご参照ください。設定が完了すると、[アップロード署名](htt ps://intl.cloud.tencent.com/document/product/266/33922#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0) を生成するときに`storageRegion`パラメータで指定できます。パラメータ値はストレージリージョンの[英語の略称](https://intl.cloud.tencent.com/document/product/266/33910) になります。
- **アップロード時のカバー付加**
VODでは、アップロードSDKインターフェースに関連するカバーへのパスを入力することで、カバー付きのビデオをアップロードできます。詳細については、以下をご参照ください。
	- [AndroidのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33925)
	- [iOSのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33926)
	- [WebのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33924)
- <span id = "p4"></span>**ワンタイム署名**
ビデオのアップロード中に、Appのバックエンドによって配布された署名は、デフォルトで有効期間中、複数回使用できます。Appにビデオアップロードのセキュリティに関する高い要件がある場合は、ワンタイム署名を指定することができます。
ワンタイム署名の使用方法：Appのバックエンドが署名を配布するときに、パラメータ`oneTimeValid`を1に指定する必要があります。詳細については、[クライアントからのアップロード署名](https://intl.cloud.tencent.com/document/product/266/33922)をご参照ください。
>ワンタイム署名は1回しか使用できません。この署名方法はより安全ですが、Appによる追加の処理が必要です。例えば、アップロードエラーが発生したときは、SDKを使用してビデオを再度アップロードすることはできません。新しいアップロード署名を申請する必要があります。
- **中断からの再開**
ビデオのアップロード中にアップロードが予期せず終了した場合、中断したポイントからファイルを再度アップロードできます。
>中断からの再開の有効時間は1日です。つまり、ビデオのアップロードが中断しても、1日以内に同じビデオを再度アップロードすると、中断したポイントからアップロードすることができます。1日を超えると、デフォルトでビデオ全体が再度アップロードされます。
>
Appで中断からの再開機能を有効にする方法は、次のとおりです。
	- [AndroidのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33925)、アップロード時に`enableResume`フィールドをTrueに設定します。
	- [iOSのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33926)、アップロード時に`enableResume`フィールドをTrueに設定します。
	- [WebのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33924)、中断からの再開は組み込まれており、ユーザーによる操作は不要です。
- **アップロードの一時停止/再開/キャンセル**
VOD SDKでは、ビデオのアップロード中に、アップロードの一時停止、再開またはキャンセルをすることができます。詳細については、以下をご参照ください。
	- [AndroidのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33925)
	- [iOSのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33926)
	- [WebのアップロードSDK](https://intl.cloud.tencent.com/document/product/266/33924)

#### よくあるご質問 
- **ビデオのアップロードが完了した後にトランスコードを自動的に開始する方法とは**？
クライアントからアップロードするための署名の`procedure`パラメータを介して、ビデオのアップロードが完了した後の処理方法を指定します。詳細については、[アップロード時のタスクフロー指定]( #p1) をご参照ください。
- **Appバックエンドはビデオのアップロード完了通知を受信したとき、どのクライアントがアップロードしたのか、どうすれば特定できますか**？
クライアントからアップロードするための署名に、`sourceContext`パラメータを追加して、ユーザーID情報を伝達できます。アップロード完了通知は、このパラメータをAppバックエンドに渡します。詳細については、[イベント通知](#p2)をご参照ください。
<span id = "p2"></span>
### 3. イベント通知

ビデオのアップロードが完了すると、VODはAppバックエンドに [イベント通知 - ビデオアップロード完了](https://intl.cloud.tencent.com/document/product/266/33950) を開始します。Appバックエンドは、このイベントを通じてビデオのアップロード動作を認識することができます。イベント通知を受信するには、Appは [コンソール - コールバック設定](https://console.cloud.tencent.com/vod/callback) に移動してイベント通知を有効にする必要があります。[イベント通知 - ビデオアップロード完了](https://intl.cloud.tencent.com/document/product/266/33950) には、主に次の情報が含まれています。
- 新しいビデオファイルのFileIdとURL。
- VODは、ビデオアップロード時のパススルーフィールドの指定をサポートしており、イベントが完了すると、パススルーフィールドはAppバックエンドに送信されます。イベント通知には、次のフィールドが含まれています。
	- `SourceType`：このフィールドはTencent Cloudによって`ServerUpload`と定められており、アップロードがサーバーからであることを表しています。
	- `SourceContext`：ユーザー定義のパススルーフィールドです。署名の配布中にAppバックエンドに指定されます。これは署名の`sourceContext`パラメータに対応します。
- VODは、ビデオのアップロードが完了したとき、自動ビデオ処理をサポートしています。アップロード時に、[ビデオ処理タスクフロー](https://intl.cloud.tencent.com/document/product/266/33931#.E4.BB.BB.E5.8A.A1.E6.B5.81) が指定されていると、タスクIDはイベント通知の（`data.procedureTaskId`フィールド）にも含まれます。

詳細については、以下をご参照ください。
- [タスク管理とイベント通知](https://intl.cloud.tencent.com/document/product/266/33931#.E7.BB.93.E6.9E.9C.E9.80.9A.E7.9F.A5)
- [イベント通知 - ビデオアップロード完了](https://intl.cloud.tencent.com/document/product/266/33950)





