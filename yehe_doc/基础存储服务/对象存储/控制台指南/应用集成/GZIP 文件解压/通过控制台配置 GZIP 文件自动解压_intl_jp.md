## 概要

GZIPファイル解凍機能は、Cloud Object Storage（COS）が[Serverless Cloud Function（SCF）](https://intl.cloud.tencent.com/document/product/583)をベースとしてユーザーに提供するデータ処理ソリューションです。ユーザーは、バケットにGZIPファイル解凍ルールを追加し、GZIP圧縮ファイルをCOSにアップロードする時に、自動トリガーのCOSを、プリセットしたSCFにすることで、ファイルを指定のバケットおよびパスに自動解凍できます。

ユーザーは次の2つの方法で、GZIPファイルの解凍機能を使用することができます。
- コンソールによる使用：コンソールでGZIPファイルの解凍関数を設定します。設定完了後、バケットに新規アップロードされたGZIPファイルに対して、自動解凍が行われます。
- APIによる使用：APIを呼び出すことによって、GZIPファイルの解凍操作が自動でトリガーされます。

このドキュメントでは、主にコンソールからどのようにGZIPファイル解凍機能を使用するかについてご説明します。APIによる使用方式は、[APIによるGZIPファイルの解凍](https://intl.cloud.tencent.com/document/product/436/46202)をご参照ください。


## 注意事項

- GZIPファイルの解凍は、.gz、.tgz形式のファイルの解凍をサポートしており、圧縮パッケージ内の1つのファイルのサイズは、5GBを超えないものとします。圧縮パッケージ内の1つのファイルが5Gより大きい場合、解凍は失敗します。
- 以前にCOSコンソールでバケットにGZIPファイル解凍ルールを追加したことがある場合は、[SCFコンソール](https://console.cloud.tencent.com/scf/list?rid=1&ns=default)で、作成したGZIPファイル解凍関数を確認することができます。このGZIPファイル解凍関数を削除すると、ルールが有効にならない場合がありますので削除**しないで**ください。
- GZIPファイル解凍は、広州、上海、北京、成都、中国香港、シンガポール、ムンバイ、トロント、シリコンバレーなど、SCFがリリースされているすべてのリージョンでサポートされています。その他のサポートリージョンについては、[SCF製品ドキュメント](https://intl.cloud.tencent.com/document/product/583)をご参照ください。
- 圧縮パッケージのディレクトリまたはファイル名には、UTF-8またはGB 2312エンコーディングを厳格に使用してください。厳格に使用しない場合、解凍後にファイル名やディレクトリ名が文字化けしたり、解凍が中断されたりすることなどがあります。エラーが発生した場合は、作成した関数の右側にある**ログの確認**をクリックし、SCFコンソールにジャンプしてログエラーの詳細を確認することができます。
- CASタイプのファイルは、解凍をサポートしていません。CASタイプの圧縮パッケージを解凍する必要がある場合は、あらかじめ復元してから行ってください。復元操作の詳細については、[アーカイブオブジェクトの復元](https://intl.cloud.tencent.com/document/product/436/30961)をご参照ください。
- 1つの圧縮パッケージの解凍にかかる最大処理時間は900秒で、900秒を過ぎて未完了の解凍タスクがあると失敗します。COSの解凍機能の制限に関する説明は、SCFサービスに基づいています。その他の制限に関する説明については、[SCFの制限の説明](https://intl.cloud.tencent.com/document/product/583/11637)をご参照ください。
- COSのGZIP解凍機能は、SCFサービスに依存しています。ユーザーには、SCFサービス[無料利用枠](https://intl.cloud.tencent.com/document/product/583/12282)が提供されていますが、無料利用枠を超える部分については、[SCF製品価格](https://intl.cloud.tencent.com/document/product/583/12281)に従って課金されます。解凍機能を使用する場合、圧縮パッケージが大きいほど、消費するリソースも多くなります。解凍の回数が多いほど、消費する呼び出し回数も多くなります。

## 操作手順

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインします。
2. 左側ナビゲーションバーで**バケットリスト**をクリックし、バケットリスト管理ページに進みます。
3. GZIPファイル解凍ルールを追加したいバケットを見つけ、そのバケット名をクリックし、バケット管理ページに進みます。
4. 左側ナビゲーションバーで**関数の計算**を選択し、**GZIPファイル解凍関数**をクリックすると、GZIPファイル解凍関数の設定ページに進みます。
> ! SCFをアクティブにしていない場合は、[SCFコンソール](https://console.cloud.tencent.com/scf)に移動してSCFサービスをアクティブ化し、プロンプトに従ってサービス権限承認を行えば完了です。
> 
5. **関数の追加**をクリックし、ポップアップウィンドウに以下の情報を設定します。 

 - **関数名**：関数名は、関数の一意の識別名として、作成後に変更することはできません。[SCFコンソール](https://console.cloud.tencent.com/scf/list?rid=1&ns=default)でこの関数を確認できます。
 - **イベントタイプ**：イベントとは、Serverless Cloud Functionをトリガーする操作のことです。アップロード操作を例にとると、アップロード方法は`PUT Object`インターフェースまたは`POST Object`インターフェースを呼び出して行います。選択したイベントが**Putメソッドによって作成**された場合、`PUT Object`インターフェースを介してアップロードされた圧縮パッケージのみが解凍をトリガーします。
> ! ファイルが、シンプルアップロード、マルチパートアップロード、地域間コピーなど、複数のチャネルでバケットにアップロードされる場合は、**すべて作成**イベントの選択をお勧めします。
> 
 - **トリガー条件**：圧縮パッケージをパスにアップロードする時に、SCFをトリガーする条件のことです。指定されたプレフィックスを選択した場合は、圧縮パッケージが指定されたプレフィックスパスにアップロードされたときにのみ、SCFをトリガーします。プレフィックスを指定しないことを選択した場合は、圧縮されたパッケージが、バケット内の任意の場所にアップロードされたときにトリガーされます。
> ! 設定されたターゲットファイルのプレフィックスとトリガー条件の間に包含関係がある場合、循環トリガーとなることがありますので、可能な限りこの状況を回避するようにしてください。例えば、ターゲットプレフィックスが`prefix`で、トリガー条件が`pre`の場合、`pref` を持つ圧縮パッケージをアップロードすると、循環解凍がトリガーされます。
> 
 - **SCF権限承認**：解凍には、SCFがバケットから圧縮パッケージを読み取り、解凍したファイルを指定した場所にアップロードするための承認が必要です。そのため、この権限を追加する必要があります。
6. **次のステップ**をクリックし、ポップアップウィンドウに以下の情報を設定します。 

 - **解凍形式**：現在サポートされている圧縮形式のことで、現在は.gz、.tgz形式の圧縮パッケージの解凍がサポートされています。
 - **配布バケット**：解凍されたファイルを格納するバケットを選択します。
 - **配布パス**：マッチしたファイルをこのターゲットディレクトリに解凍します。循環トリガーによる不要な課金を防ぐため、プレフィックスとは異なるターゲットディレクトリの設定をお勧めします。
 - **追加のプレフィックス**：
   - 圧縮パッケージ名：圧縮パッケージは、圧縮パッケージ名のディレクトリに解凍することができます。
   - 圧縮パッケージが配置されているディレクトリ：圧縮パッケージは、圧縮パッケージが配置されているディレクトリ名が付けられたディレクトリに解凍することができます。
   - 圧縮パッケージの完全パス：圧縮パッケージは、完全圧縮パッケージパス名のプレフィックスに解凍することができます。
   - 無：圧縮パッケージ内のファイルは、送信先のパスに直接解凍されます。
>? 事例：
> ファイル名を123とした圧縮パッケージを、バケットbucket1-125000000のtestディレクトリにアップロードし、解凍後に配布するバケットをbucket2-1250000000とし、配布パスをルートディレクトリとします。ユーザーが追加のプレフィックスを選択する場合、次のアクションが生じます。
> - 圧縮パッケージ名：解凍後のファイルの保存パス：bucket2-1250000000/123
> - 圧縮パッケージが配置されているディレクトリ：解凍後のファイルの保存パス：bucket2-1250000000/test
> - 圧縮パッケージの完全パス：解凍後のファイルの保存パス：bucket2-1250000000/test/123
> - 無：解凍後のファイルの保存パス：bucket2-1250000000
> 
7. 設定が正しいことを確認し、**確定**をクリックすると、関数が追加されたことを確認できます。

   新規作成した関数に対しては、次のような操作が可能です。
 - **ログの確認**をクリックして、GZIPファイルの解凍の履歴を確認します。解凍でエラーが発生した場合は、**ログの確認**をクリックしてSCFコンソールにすぐにジャンプし、ログエラーの詳細を確認することもできます。
 - **詳細**をクリックして、GZIPファイルの解凍の具体的な設定ルールを確認します。
 - **その他**>**編集**とクリックして、GZIPファイルの解凍ルールを変更します。
 - **その他**>**削除**とクリックして、使用しないGZIPファイルの解凍ルールを削除します。
