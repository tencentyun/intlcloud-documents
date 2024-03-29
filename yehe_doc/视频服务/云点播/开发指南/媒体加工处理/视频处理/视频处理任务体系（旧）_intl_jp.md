ビデオ処理タスク開始後、タスクを完了して結果を出力するまでに一定の時間（数分から数時間）を必要とし、このタスクは基本的にオフラインタスクに該当します。VODは、ビデオ処理タスクの特徴に基づき、業務サイドが同期的にタスクを開始し、かつ非同期的に結果の通知を受信し、タスクの実行結果を認識できる「同期開始+非同期認識」のタスクシステムを提供します。
![](https://main.qcloudimg.com/raw/8941db2138127cc702ead3f856b5b074.png)

- タスクの開始：業務サイドがビデオ処理タスクを送信すると、VODは直ちに業務サイドにタスクIDを返し、しばらく待ってから、実行が開始されます。
- 結果の通知：タスクが完了すると、VODは直ちに業務サイドに結果の通知を開始します。通知にはタスクIDと実施の結果が含まれます。
- タスクの確認：業務サイドがタスクを送信後、任意の時間にタスクIDを介して、タスクの実行ステータスと結果を同期し、確認することが可能です。

## パラメータテンプレート

ビデオトランスコーディングパラメータにはコンテナ形式、エンコード形式、ビットレート、解像度、フレームレートなど数10個のパラメータが含まれるなど、ビデオ処理のパラメータは、通常、かなり複雑です。ビデオ処理タスクのパラメータを簡略化するため、VODはテンプレートIDで識別されるさまざまな統合パラメータテンプレート（[トランスコードテンプレート](https://intl.cloud.tencent.com/document/product/266/33938#.E8.BD.AC.E7.A0.81.E6.A8.A1.E6.9D.BF) など）を提供しています。
- プリセットのパラメータテンプレート：一般的なビデオ処理パラメータセットについては、VODはプリセットパラメータテンプレートと呼ばれる一連のパラメータテンプレートをプリセットします。テンプレートリストについては、[プリセットのパラメータテンプレートリスト](https://www.tencentcloud.com/document/product/266/52735)をご参照ください。
- カスタムパラメータテンプレート：コンソールまたはサーバーサイドのAPIを介してパラメータテンプレートをカスタマイズすることができます。

## タスクフロー
VODでは、次のビデオ処理操作はいずれも独立タスクに該当します。
- ビデオをLD画質のMP4にトランスコードする
- ビデオをSD画質のMP4にトランスコードする
- ビデオに対し10秒間隔でスクリーンキャプチャのサンプリングを行う
- ビデオに対しAIによるポルノ検出を行う
- ビデオに対しインテリジェントクラシフィケーションを行う

複数の独立タスクを同時に処理する場合は、複数のタスクIDが生成されるため、複数のタスクの結果通知を受信して処理する必要があります。複数のタスクの開始と通知を簡略化するために、VODではタスクフローを提供します。タスクフローは実質的に複数のサブタスクを含む「親タスク」であり、タスクフローを開始することは、タスクフローに含まれるすべてのサブタスクを開始することを意味します。
![](https://main.qcloudimg.com/raw/eb772f0b31003f3c3325312e3c1584a5.png)
図に示すとおり、タスクフローには3つのサブタスクが含まれ、タスクフローは最後のサブタスク（サブタスク3）が完了すると終了します。タスクフローの結果通知はタスクフロー終了時、および各サブタスク完了時にトリガーされ、業務サイドは任意のサブタスクの実行結果をリアルタイムで認識できます。

VODのビデオ処理タスクの大部分は、特殊な「タスク」と見なされる「タスクフロー」の形式で実行されます。VODはさらに、 [タスクフローテンプレートの作成](https://intl.cloud.tencent.com/document/product/266/14058) とテンプレートの命名をサポートしています。タスクフローを開始する場合に、タスクフローテンプレート名を用いて、開始するタスクを示す ことができます。

<span id="OriginatingTask"></span>

## タスクの開始

ビデオ処理タスクの開始方法には、「サーバーAPIから開始する」、「コンソールから開始する」および「アップロード時に実行するタスクを指定する」という3つの方法があります。

#### サーバーAPIから開始する方法

サーバーAPIを介して、VODのビデオにタスクを直接開始したり、ビデオを編集したり、編集によって生成された新しいビデオに対して実行するタスクを指定したりできます。
- [ビデオ処理](https://intl.cloud.tencent.com/document/product/266/34125)
- [指定URLのビデオにビデオ処理を開始](https://intl.cloud.tencent.com/document/product/266/34123)
- [タスクフローテンプレートによるビデオ処理を実施](https://intl.cloud.tencent.com/document/product/266/34124)
- [ビデオ編集](https://intl.cloud.tencent.com/document/product/266/34126)

#### コンソールから開始する方法

コンソールを介して、VODのビデオに対するタスクを開始することができます。開始方法については、 [ビデオの処理](https://intl.cloud.tencent.com/document/product/266/33892) をご参照ください。

#### アップロード時に実行するタスクを指定する方法

VODは、クライアントからのアップロード、サーバーからのアップロード、コンソールからのアップロードという3つの動画アップロード方法を提供しています。これらのアップロード方式はいずれも動画ファイルのアップロード後に実行するタスクを指定することができます。

- クライアントからのアップロード： [クライアントからのアップロード署名](https://intl.cloud.tencent.com/document/product/266/33922#p3) の`procedure`パラメータを介して、ビデオのアップロード後に実行するタスクを指定することができます。
- サーバーからのアップロード： [アップロードの申請](#https://intl.cloud.tencent.com/document/product/266/34120#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0) の`procedure`パラメータを介して、ビデオのアップロード後に実行するタスクを指定することができます。
- コンソールからのアップロード：コンソールを介してビデオをアップロードし、【アップロードと同時にビデオに対する処理操作を実行】を選択し、ビデオのアップロード後に実行するタスクを指定します。具体的な操作については、 [ビデオのアップロード](https://intl.cloud.tencent.com/document/product/266/33890)をご参照ください。

<span id="ResultNotification"></span>

## 結果の通知

業務サイドは、ビデオ処理を開始した後、「結果通知」によってタスクの実行結果を非同期に認識する必要があります。
ビデオ処理の結果通知には、主に次のタイプがあります。

- [タスクフロー状態の変更](https://intl.cloud.tencent.com/document/product/266/33953)
- [ビデオ編集の完了](https://intl.cloud.tencent.com/document/product/266/33954)

ビデオ処理の結果通知はVODの「イベント通知」に該当し、「HTTP通常コールバック」と「信頼できるコールバック」の2つの受信タイプがあります。イベント通知の受信方法などの情報については、 [イベントの通知](https://intl.cloud.tencent.com/document/product/266/33948) をご参照ください。

<span id="TaskQuery"></span>

## タスクの確認

業務サイドは、結果通知によってタスクの実行結果を認識するだけでなく、さらにタスクIDを介してタスクの実行ステータスを定刻にポーリングするタスクを確認することができます。現在、サーバーAPIからのタスクの実行ステータスと実行結果の確認については、VODではタスクリストの取得と [タスクの詳細確認](https://intl.cloud.tencent.com/document/product/266/34129) の2つのみを提供しています。
