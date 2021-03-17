## 操作シナリオ
サーバーからのビデオアップロードとは、AppバックエンドがビデオをVODプラットフォームにアップロードすることを指します。ここでは、サーバーAPIを使用してビデオを アップロードする方法を紹介します。

## 前提条件

#### 1. サービスのアクティブ化

VODサービスをアクティブにします。
#### 2. Tencent Cloud APIキーの取得

サーバーAPIの呼び出しに必要なセキュリティ証明（SecretIdとSecretKey）を取得します。具体的な手順は次のとおりです。
1. コンソールにログインし、【クラウド製品】>【CAM】>[【APIキー管理】](https://console.cloud.tencent.com/cam/capi)と選択して、「APIキー管理」ページに入ります。
2. Tencent Cloud APIキーを取得します。キーを作成していない場合は、【キーの作成】をクリックして、SecretIdとSecretKeyのペアを作成することができます。

## 操作手順
### 1. アップロードの開始

アップロードの開始方式は、SDKによるアップロード開始とAPIによるアップロード開始に分かれます。

#### SDKから開始するアップロード方法

ユーザー開発サイドでアップロード機能を扱いやすくするため、VODでは多様な言語のプラットフォームによるSDKを提供しています。各言語のSDKにはいずれも対応するDemoが含まれています。詳細については、以下をご参照ください。
- [PHP SDK](https://intl.cloud.tencent.com/document/product/266/33916)
- [Java SDK](https://intl.cloud.tencent.com/document/product/266/33914)
- [Python SDK](https://intl.cloud.tencent.com/document/product/266/33917)
- [Go SDK](https://intl.cloud.tencent.com/document/product/266/33919)
- [C# SDK](https://intl.cloud.tencent.com/document/product/266/33915)

#### APIから開始するアップロード方法

VODが提供するアップロードSDKにおいて、Appバックエンドの使用言語がカバーされていない場合は、Appバックエンドで自分でVODのサーバーAPIを呼び出し、ビデオのアップロードを行なう必要があります（この方式は複雑なため、推奨しません）。APIによるアップロードの作業フローチャートは次のとおりです。
![](https://main.qcloudimg.com/raw/005ec15acf74e0a428e8d328ffd2da2f.png)
SDK方式のアップロードと比べ、API方式によるアップロードは、アップロードの申請やファイルのアップロードなどの手順を自分で実行する必要があります。またファイルのアップロードもSDKの方式ほど便利ではありません。大きなファイルについては、パートアップロードなどのロジックを自分で実行する必要があります。詳細については、以下をご参照ください。

- [サーバーAPI - アップロードの申請](https://intl.cloud.tencent.com/document/product/266/34120)
- [サーバーAPI - ファイルのアップロード](https://intl.cloud.tencent.com/document/product/266/33913)
- [サーバーAPI - アップロードの確認](https://intl.cloud.tencent.com/document/product/266/34119)

#### 高度な機能

- **アップロード時のタスクフローの指定**
ビデオアップロード完了後に、[ビデオ処理タスクフロー](https://intl.cloud.tencent.com/document/product/266/33931)（例：トランスコーディング、スクリーンキャプチャなど）を自動的に開始したい場合は、サーバーAPI [アップロードの申請](https://intl.cloud.tencent.com/document/product/266/34120)を呼び出す時に、`Procedure`パラメータによって実現することが可能です。パラメータの値は、タスクフローテンプレート名とします。VODでは、[タスクフローテンプレートの作成](https://intl.cloud.tencent.com/document/product/266/14058)、さらにそのテンプレートに対する命名をサポートしています。タスクフローの開始時は、タスクフローテンプレート名によって開始したいタスクを表示します。VODが提供する多様な言語のSDKはいずれもタスクフローのパラメータの指定をサポートしています。詳細については、以下をご参照ください。
	- [PHP SDK](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)
	- [Java SDK](https://intl.cloud.tencent.com/document/product/266/33914#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)
	- [Python SDK](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)
	- [Go SDK](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)
	- [C# SDK](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)
- **アップロード時にストレージリージョンを指定**
VODが提供するストレージリージョンのデフォルト設定は重慶です。その他のリージョンにストレージしたい場合は、コンソール上でその他のストレージリージョンを自分で追加できます。詳細については、[アップロードストレージ設定](https://intl.cloud.tencent.com/document/product/266/18874)をご参照ください。設定が完了したら、サーバーAPI [アップロードの申請](https://intl.cloud.tencent.com/document/product/266/34120)を呼び出す時に、`StorageRegion`パラメータでストレージリージョン指定します。パラメータの値はストレージリージョンの[英語の略称](https://intl.cloud.tencent.com/document/product/266/9760)とします。VODが提供する多様な言語のSDKはいずれもアップロード時のストレージリージョンの指定をサポートしています。詳細については、以下をご参照ください。
	- [PHP SDK](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F)
	- [Java SDK](https://intl.cloud.tencent.com/document/product/266/33914#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F)
	- [Python SDK](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F)
	- [Go SDK](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F)
	- [C# SDK](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F)
	
### 2. イベント通知

ビデオのアップロードが完了すると、VODはAppバックエンドに [イベント通知 - ビデオアップロード完了](https://intl.cloud.tencent.com/document/product/266/33950)を開始し、Appバックエンドは、このイベントによってビデオアップロードを感知します。イベント通知を受信したい場合は、 App側で[コンソール - コールバック設定](https://console.cloud.tencent.com/vod/callback)にて、イベント通知を有効にする必要があります。[イベント通知 - ビデオアップロード完了](https://intl.cloud.tencent.com/document/product/266/33950)には主に、次の情報が含まれています。
- 新しいビデオファイルのFileIdとURL。
- VODは、ビデオアップロード時のパススルーフィールドの指定をサポートしており、イベントが完了すると、パススルーフィールドはAppバックエンドに送信されます。イベント通知には、次のフィールドが含まれています。
	- `SourceType`：このフィールドはTencent Cloudによって`ServerUpload`と定められており、アップロードがサーバーからであることを表しています。
	- `SourceContext`：ユーザー定義のパススルーフィールドです。署名の配布中にAppバックエンドに指定されます。これは署名の`sourceContext`パラメータに対応します。
- VODでは、ビデオアップロード完了時にビデオ処理を自動的に開始する機能をサポートしています。アップロード時に[ビデオ処理タスクフロー](https://intl.cloud.tencent.com/document/product/266/33931)を指定すると、イベント通知の内容にもタスクID、すなわちイベント通知内の`data.procedureTaskId`フィールドが含まれます。

詳細については、以下をご参照ください。
- [タスク管理とイベント通知](https://intl.cloud.tencent.com/document/product/266/33931)
- [イベント通知 - ビデオアップロード完了](https://intl.cloud.tencent.com/document/product/266/33950)


