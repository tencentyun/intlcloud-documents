## クイックスタート
本文では、Batchコンソールを使用してジョブを提出し、3ds Max 2018のイメージレンダリングを完了し、レンダリングされたイメージをエクスポートする方法について紹介します。具体的な手順は次のとおりです。
### 一. カスタムイメージの作成
1.　カスタムWindowsイメージを作成します。

2.　3ds Max 2018のインストールプロセスについては、[公式ホームページ](https://www.autodesk.com/products/3ds-max/overview)を参照してください。

>注意：
- ソフトウェアのダウンロードをブロックしないように、Windowsファイアウォールを一時的に無効化してください。
- グラフィックカードの初期化に失敗しないように、[グラフィックカード選択ガイド](https://knowledge.autodesk.com/zh-hans/support/3ds-max/learn-explore/caas/CloudHelp/cloudhelp/2015/CHS/3DSMax/files/GUID-3D6B4C8E-8C0D-4A9C-BFB0-2463803268CE-htm.html)を参照して、適切なグラフィックカードの種類を選択してください。特別な理由がない場合は、「Nitrous Software」を選択することをお勧めします。

### 二. レンダリングファイルの準備
レンダリング素材の主なストレージ方式は2つがあります。[COS](https://intl.cloud.tencent.com/document/product/436)と[CFS](https://intl.cloud.tencent.com/document/product/582)です。マウントパラメータを構成することで、Batchはレンダリングジョブが実行される前にCOSまたはCFSをローカルにマウントし、レンダラーはローカルファイルにアクセスしているかのように、COSまたはCFSにアクセスできます。

- レンダリング素材のサイズが小さい場合は、すべての素材をgzipパッケージに圧縮してCOSにアップロードすることをお勧めします。[オブジェクトのアップロード](https://intl.cloud.tencent.com/document/product/436/6233)を参照してください。
- レンダリング素材のサイズが大きい場合は、CFSに保存することをお勧めします。

### 三. タスクテンプレートの作成
1. [Batchコンソール]()にログインし、左側のナビゲーションバーの【タスクテンプレート】オプションをクリックし、目標地域を選択して【新規作成】ボタンをクリックします。

2. 基本情報を構成します。例：

![](https://main.qcloudimg.com/raw/cf2f94cec702e0d42abe34b6e0d38bde.jpg)
  * 名前：rendering
  * 説明：3ds Max 2018 Demo
  * リソース構成：S1.LARGE8（4コア8G）
  * リソース数：同時レンダリング数、1台など
  * タイムアウト時間：デフォルト
  * 再試行回数：デフォルト
  * イメージ：img-i64lx84hなどのカスタムイメージタグ

3.　プログラム情報を構成します。例：

  ![](https://main.qcloudimg.com/raw/ef7c95752cfb266f855ea0e69436d245.jpg)
  
  * 実行方式：PACKAGE
  * パッケージアドレス：COSの場合は、`cos://barrygz-1251783334.cos.ap-guangzhou.myqcloud.com/render/max.tar.gz`
  * Stdoutログ：フォーマットは[COS、CFSパス記入](https://cloud.tencent.com/document/product/599/13996)を参照してください
  * Stderrログ：Stdoutログと同じ
  * コマンドライン：`3dsmaxcmd Demo.max -outputName:c:\\render\\image.jpg`

4.　ストレージマッピングを構成します。
![](https://main.qcloudimg.com/raw/f5e1836e79852eb5d4c49b917bb870f8.jpg)
  * 出力パスマッピング-ローカルパス：`C:\\render\\`
  * 出力パスマッピング-COS CFSパス：フォーマットは[COS、CFSパス記入](https://cloud.tencent.com/document/product/599/13996)を参照してください

5.　タスクのJSONファイルをプレビューして正しいことを確認し、【保存】ボタンをクリックします。

### 四. ジョブの提出
1. 左側のナビゲーションバーの【ジョブ】オプションをクリックし、目標地域を選択して【新規作成】ボタンをクリックします。

2. ジョブの基本情報を構成します。例：
  ![](https://main.qcloudimg.com/raw/7f19ede7710ec960fc4586297213d1fc.jpg)
  * ジョブ名：max
  * 優先度：デフォルト
  * 説明：3ds Max 2018 Demo

3. タスクフローページの左側にある**rendering**タスクを選択し、マウスを動かしてタスクを右側のキャンバスに配置します。

4. タスクフローの右側にある**タスク詳細**を開き、構成が正しいことを確認したら、【完了】ボタンをクリックします。
![](https://main.qcloudimg.com/raw/00df21802b524cd684f43b68155e3483.jpg)

5. ジョブ実行情報の照合については、[情報照合](https://cloud.tencent.com/document/product/599/14567)を参照してください。

6. レンダリングプロセスをデモします。
![](https://main.qcloudimg.com/raw/4a0743f3a49045f59c0580deda1529f9.png)

7. レンダリング結果の照合については、[オブジェクト情報の確認](https://cloud.tencent.com/document/product/436/13326)を参照してください。
![](https://main.qcloudimg.com/raw/7997d36d8d08e0733fb372dfc6513034.jpg)

## 次に何ができますか？
本文では簡単なレンダリングの例を示します。これはシングルインスタンスジョブで、ユーザーに最も基本的な機能だけを示すために、コンソール使用ガイドに従ってBatchのより高度な機能をテストし続けることができます。
- **豊富なCVM構成**：Batchは、豊富なCVM構成項目を提供して、ビジネスシナリオに基づいてCVM構成をカスタマイズできます。
- **リモートストレージマッピング**：Batchはストレージアクセスを最適化し、リモートストレージサービスへのアクセスをローカルファイルシステムの操作に単純化します。
- **マルチイメージの同時レンダリング**：Batchは同時レンダリング数の指定をサポートして、[環境変数](https://intl.cloud.tencent.com/document/product/599/11752)で異なるレンダリングインスタンスを区別して、各レンダリングインスタンスは異なるレンダリング素材を読み込んで、同時レンダリングを実装します。

