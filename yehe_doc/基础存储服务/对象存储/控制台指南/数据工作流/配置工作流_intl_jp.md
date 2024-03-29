## 概要

データワークフローによって、ビデオ処理フローを必要に応じてスピーディーかつフレキシブルに構築することができます。各ワークフローを、バケットに入力するパスにバインドし、ビデオファイルがそのパスに**アップロード**されると、そのメディアワークフローが**自動的にトリガー**され、指定された処理操作が実行され、処理結果がターゲットバケットの指定されたパスに自動的に保存されます。

データワークフローでは、**オーディオビデオトランスコーディング（高速高画質トランスコーディング、ブロードキャストグレードフォーマットのトランスコーディングを含む）**、**ビデオフレームキャプチャ**、**ビデオアニメーション画像生成**、**インテリジェントカバー**、**オーディオビデオスプライシング**、**音声分離**、**ハイライトコレクション**、**アダプティブビットレートストリーミング**、**SDRtoHDR** 、**ビデオエンハンスメント**、**超解像度**、**オーディオビデオセグメンテーション**、**関数のカスタマイズ**、**画像処理**などの機能を実現できます。

>! 
> - ワークフローは現在、3gp、asf、avi、dv、flv、f4v、m3u8、m4v、mkv、mov、mp4、mpg、mpeg、mts、ogg、rm、rmvb、swf、vob、wmv、webm、mp3、aac、flac、amr、m4a、wma、wav形式のファイル処理をサポートしています。メディア処理のリクエストを開始する場合、完全なファイル名とファイル形式を入力しなければ、形式を認識できず処理されませんので、ご注意ください。
> - 現在、ワークフロー機能ではアップロード中のビデオファイルの操作のみをサポートしています。クラウド上のデータに対してメディア処理操作を行いたい場合は、[タスク](https://intl.cloud.tencent.com/document/product/436/46409)機能をご利用ください。
> 

## 操作手順

### ワークフローの作成

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインします。
2. 左側ナビゲーションバーで**バケットリスト**をクリックし、バケットリスト管理ページに進みます。
3. メディア処理を行いたいバケットを見つけ、そのバケット名をクリックし、バケット管理ページに進みます。
4. 左側ナビゲーションバーで、**データワークフロー**を選択し、**ワークフロー**をクリックしてワークフロー管理ページに進みます。
5. **ワークフローの作成**をクリックし、ワークフロー作成ページに進みます。
6. ワークフロー作成ページで、以下の情報を設定します。
![](https://qcloudimg.tencent-cloud.cn/raw/c2bec7689878536a9ddfc52c63fe5991.png)
  - **ワークフロー名**：入力必須項目です。中国語、アルファベットの大文字と小文字[A～Z、a～z]、数字[0～9]、アンダーバー(\_)、ハイフン(-)のみサポートし、長さは128文字以下とします。
  - **入力バケット**：デフォルトのアイテムで、現在のバケットです。
  - **入力パス**：オプション項目です。`/`で始まり、`/`で終わります。入力しない場合はバケットに入力したすべてのパスが有効になります。ワークフローを有効化すると、ビデオファイルをこのパスにアップロードした時点で、メディアワークフローが自動的にトリガーされるようになります。
  - **形式のマッチング**：デフォルトのオーディオビデオファイル、画像ファイルフィルタリングルールまたはカスタムルールを選択するか、またはすべてのファイルを選択し、バケット内のすべてのオブジェクトに対して処理を行うこともできます。
  - **キュー**：入力必須項目です。サービスをアクティブ化すると、システムが自動的にユーザーキューを作成します。ユーザーがタスクを送信すると、タスクはまずキューに入れられ、優先度および送信順に基づいて順次実行されます。キュー情報は**共通設定**で確認することができます。
  - **コールバック設定**：キューのコールバック、すなわちコールバックURLを使用して、キューとのバインドを行うことができます。変更が必要な場合は指定したキューのリストに進んで変更するか、またはコールバックURLをカスタマイズしてください。
  - **ワークフローの設定**：右側の「+」をクリックして入力し、**オーディオビデオトランスコーディング（高速高画質トランスコーディング、ブロードキャストグレードフォーマットのトランスコーディングを含む）**、**ビデオフレームキャプチャ**、 **ビデオアニメーション画像生成**、**インテリジェントカバー**、**オーディオビデオスプライシング**、**音声分離**、**ハイライトコレクション**、**hlsアダプティブマルチビットレート**、**SDRtoHDR** 、**ビデオエンハンスメント**、**超解像度**、**オーディオビデオセグメンテーション**、**関数のカスタマイズ**、**画像処理**ノードを追加します。各ワークフローにつき、少なくとも1つ以上のタスクノードを設定します。タスクノードの設定では、ターゲットバケット、ターゲットファイル名（詳細については[ワークフロー変数の説明](#1)をご参照ください）、ターゲットパス、選択するタスクテンプレートを設定する必要があります。テンプレートの説明と設定の詳細については[テンプレート](https://intl.cloud.tencent.com/document/product/436/46411)ドキュメントをご参照ください。
<dx-tabs>
::: オーディオビデオトランスコーディング
![](https://qcloudimg.tencent-cloud.cn/raw/6a07affd8bcc7a14fd23123a4daf1216.png)
:::
::: ビデオフレームキャプチャ
![](https://qcloudimg.tencent-cloud.cn/raw/d449a140aa6aa30409cbd0d4ba517ac3.png)
:::
::: ビデオアニメーション画像生成
![](https://qcloudimg.tencent-cloud.cn/raw/b936967d85e4abd21d2003a552b8ce21.png)
:::
::: インテリジェントカバー
![](https://qcloudimg.tencent-cloud.cn/raw/00fcf5b908905eadb0e4e0920fd69358.png)

説明：インテリジェントカバーは、Tencent Cloudの高度なAIテクノロジーによってビデオの内容を理解し、最適なキーフレーム3枚をインテリジェントに計算して出力する機能です。
:::
::: オーディオビデオスプライシング
![](https://qcloudimg.tencent-cloud.cn/raw/0ff1ed35b1f65f404b84435faa2ccf0f.png)
:::
</dx-tabs>
<dx-tabs>
::: 音声分離
![](https://qcloudimg.tencent-cloud.cn/raw/01ae516306970ab7e0878699843483ad.png)
:::
::: ハイライトコレクション
![](https://qcloudimg.tencent-cloud.cn/raw/d320ea46e01a3969811deecf3ee245ff.png)

:::
::: アダプティブビットレートストリーミング
![](https://qcloudimg.tencent-cloud.cn/raw/b6f7821676471e7f505dd4f4e0c09574.png)
説明：マルチビットレート、マルチオーディオトラックの複数のファイルをパッケージ化して1つのファイルにすることで、マルチビットレートアダプティブなHLSまたはDASHビデオファイルを一度に生成します。
:::
::: SDRtoHDR
![](https://qcloudimg.tencent-cloud.cn/raw/51ba2ccf5a680c5217a08cfdbaccc146.png)
:::
::: ビデオエンハンスメント

:::
</dx-tabs>
<dx-tabs>
::: 超解像度

:::
::: オーディオビデオセグメンテーション
![](https://qcloudimg.tencent-cloud.cn/raw/2fd5506dabedfbc051a13bb019ca601f.png)

:::
::: 関数のカスタマイズ

:::
:::画像処理

:::
::: オーディオビデオ情報（判断ノード）

説明：オーディオビデオ情報ノードは入力ファイルのアスペクト比、ファイル時間などの情報を判断し、次のノードの前提実行条件とすることができます。
:::
</dx-tabs>
7. 上記を正しく設定し、**保存**をクリックすると、先ほど作成したワークフローを確認することができます。

ワークフローはデフォルトでは無効状態です。このワークフローに対応するステータスボタンをクリックすると、ワークフローを有効化できます。ワークフローを有効化すると、5分以内に有効になります。ワークフローが有効になると、その後にアップロードしたビデオファイルには自動的にメディア処理操作が行われ、処理が完了すると、新しく生成されたファイルが指定のファイルパスに出力されます。

### ワークフローの管理

ワークフロー管理ページに進み、作成済みのワークフローのリストを確認します。

ワークフローリストにはワークフロー名、ワークフローID、入力パス、作成時間、有効状態などの情報が表示されます。ワークフロー名、ワークフローIDによる検索、および指定されたワークフローに対する詳細の確認・編集・削除操作をサポートします。

 - **有効化ボタン**：ワークフローの開始後、入力バケットの対応するパスにアップロードされたビデオファイルは、ワークフローに従って自動的に処理されます。この有効化ボタンを再度クリックすると、ワークフローを一時停止することができます。ワークフローを一時停止すると、対応するパスにアップロードされたビデオファイルに対する自動処理は行われなくなります。
>? ワークフローはデフォルトでは無効状態です。このワークフローに対応するステータスボタンをクリックすると、ワークフローを有効化できます。ワークフローを有効化すると、5分以内に有効になります。
>
 - **詳細**：現在のワークフロー設定の詳細を確認します。
 - **実行インスタンスの確認**：ワークフローの実行状態、実行時間などの情報を時間単位で確認します。
 - **その他**：   
   - 操作バーで、**その他 > 編集**をクリックし、「ワークフローの編集」ページに進むと、そのページでワークフロー設定を変更することができます。
   - 操作バーで、**その他 > 削除**をクリックすると、そのワークフローを削除できます。

>! ワークフローが有効状態の時は、それに対する編集と削除操作を行うことができません。
>

### 実行インスタンスの確認

各ビデオファイルのワークフローの実行が終わると、実行インスタンスが生成されます。実行インスタンスページにはソースファイルアドレス、ワークフローの実行状態、実行時間などの情報が表示されます。

1. ワークフロー管理ページに進み、ターゲットのワークフローを見つけ、操作バーで**実行インスタンスの確認**をクリックし、実行インスタンスリストページに進みます。

2. リストページでターゲットのインスタンスを見つけ、操作バーで**詳細**をクリックし、インスタンス詳細ページに進みます。

3. インスタンス詳細ページで、ワークフローの各ノードのタスクID、実行状態、開始/終了時間などの情報を確認できます。


### ワークフローのトリガー

ワークフローの作成が完了すると、ファイルをバケットにアップロードする際にワークフローが自動的にトリガーされますが、バケット内に保存されているファイルに対してただちにワークフローをトリガーすることも可能です。

1. ワークフロー管理ページに進み、ターゲットのワークフローを見つけ、**その他 > ワークフローのトリガー**をクリックし、ワークフロートリガーページに進みます。
2. ワークフロートリガーページで、ワークフローをトリガーしたいファイルを選択し、**保存**をクリックすると、ワークフローがすぐにトリガーされて実行されます。
   その後は実行インスタンスページでワークフローの実行状態を確認できます。
   ![](https://qcloudimg.tencent-cloud.cn/raw/8e5bdd5477861a20499f91eb85d49fb7.png)


<span id="1"></span>

## ワークフロー変数の説明


ワークフローは変数を使用したターゲットファイル名およびターゲットパスのレンダリングをサポートしています。現在サポートしている変数は次のとおりです。

| 変数名        | 意味                         |
| :-------------- | :--------------------------- |
| InputName       | 入力ファイルのファイル名（拡張子なし） |
| InputNameAndExt | 入力ファイルのファイル名（拡張子あり）   |
| InputPath       | ファイルの入力パス               |
| RunId           | 実行インスタンスID                  |
| Ext             | ターゲットファイルの形式               |
| Number          | ターゲットファイルの番号               |

#### 事例


ユーザーの入力ファイルのファイル名がtest1.mp4、test2.mp4であり、FLVコンテナ形式に変換（すなわち、最終的なファイル名がそれぞれtest1.flv、test2.flvとなるように）したい場合は、ターゲットファイル名のパラメータ形式を`${InputName}.${Ext}`に設定する必要があります。

ターゲットファイル名のパラメータ形式を`${InputNameAndExt}_${RunId}.${Ext}`に設定したとします。

ワークフローの実行時に2つの実行インスタンス（例えば実行インスタンスIDがそれぞれ000001と000002）が生成された場合、最終的なターゲットファイル名はtest1.mp4_000001.flvとtest2.mp4_000002.flvになります。



