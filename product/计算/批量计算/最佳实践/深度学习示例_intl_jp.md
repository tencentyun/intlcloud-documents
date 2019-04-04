## クイックスタート
本文では、scikit-learnマシンラーニングライブラリに基づいて、多層パーセプトロン（MLP、Multilayer Perceptron）BPアルゴリズムを作成するディープラーニングの例を紹介します。過去の国際サッカーの試合、チームのランキング、選手の体力の指標、およびFIFA 2018グループの結果をモデリングして、2つのチームの間で勝ち負けの確率を予測します。具体的な手順は次のとおりです。
### 一. カスタムイメージの作成
1. 作成の手順は[カスタムイメージの作成](https://intl.cloud.tencent.com/document/product/213/4942)ドキュメントを参照してください。
2. Centos 7.2 64 bitを例にして、依頼パッケージをインストールします。
```
yum -y install gcc
yum -y install python-devel
yum -y install tkinter
yum -y install python-pip
pip install --upgrade pip
pip install pandas
pip install numpy
pip install matplotlib
pip install seaborn
pip install sklearn
pip install --upgrade python-dateutil
```

### 二. パッケージのダウンロード
[プログラム圧縮パッケージのダウンロード](https://main.qcloudimg.com/raw/40b6eb7103072ca549e398ca39783f21.gz)をクリックし、ダウンロードが完了したら圧縮パッケージを[COS](https://intl.cloud.tencent.com/document/product/436)にアップロードします。パッケージのCOSアドレスを指定することで、Batchはジョブが実行される前に圧縮パッケージをCVMにダウンロードしてから、自動的に解凍して実行します。

### 三. 「fifa-predict」タスクテンプレートの作成
1. [Batchコンソール]()にログインし、左側のナビゲーションバーの【タスクテンプレート】オプションをクリックし、目標地域を選択して【新規作成】ボタンをクリックします。

2. 基本情報を構成します。例： 

  ![](https://main.qcloudimg.com/raw/27ff7efad8dd94cb875b6eaac022a23a.png)
  * 名前：fifa-predict；
  * 説明：データトレーニングと予測；
  * リソース構成：S2.SMALL1（1コア1G）、パブリックネットワークの帯域幅は従量制課金です；
  * リソース数：同時レンダリング数、例えば３台、３つのニューラルネットワークモデルを同時にトレーニングします；
  * タイムアウト時間：デフォルト；
  * 再試行回数：デフォルト；
  * イメージ：img-i64lx84hなどのカスタムイメージタグ。

3.　プログラム情報を構成します。例：

   ![](https://main.qcloudimg.com/raw/3f9d2ce72a2f180b3165e43c21319b9c.png)
  
  * 実行方式：PACKAGE；
  * パッケージアドレス：COSの場合は、`cos://barrygz-1251783334.cosgz.myqcloud.com/fifa/fifa.2018.tar.gz`；
  * Stdoutログ：フォーマットは[COS、CFSパス記入](https://cloud.tencent.com/document/product/599/13996)を参照してください；
  * Stderrログ：Stdoutログと同じ；
  * コマンドライン：`python predict.py "Japan" "Senegal"`。

4.　チームリスト：'Russia', 'Saudi Arabia', 'Egypt', 'Uruguay', 'Portugal', 'Spain', 'Morocco', 'Iran', 'France', 'Australia', 'Peru', 'Denmark', 'Argentina', 'Iceland', 'Croatia', 'Nigeria', 'Brazil', 'Switzerland', 'Costa Rica', 'Serbia', 'Germany', 'Mexico', 'Sweden', 'Korea Republic', 'Belgium', 'Panama', 'Tunisia', 'England', 'Poland', 'Senegal', 'Colombia', 'Japan'。

5.　ストレージマッピングを構成します（スキップ）。

6.　タスクのJSONファイルをプレビューして正しいことを確認し、【保存】ボタンをクリックします。

### 四. 「fifa-merge」タスクテンプレートの作成
1. [Batchコンソール]()にログインし、左側のナビゲーションバーの【タスクテンプレート】オプションをクリックし、目標地域を選択して【新規作成】ボタンをクリックします。

2. 基本情報を構成します。例：
![](https://main.qcloudimg.com/raw/a1936c208ed4ae43628729072547a015.png)
  * 名前：fifa-merge；
  * 説明：予測データのまとめ；
  * リソース構成：S2.SMALL1（1コア1G）、パブリックネットワークの帯域幅は従量制課金です；
  * リソース数：1台；
  * タイムアウト時間：デフォルト；
  * 再試行回数：デフォルト；
  * イメージ：img-i64lx84hなどのカスタムイメージタグ。

3.　プログラム情報を構成します。例：
![](https://main.qcloudimg.com/raw/4435b40995c423506ffe559c9cdb6c10.png)
  * 実行方式：PACKAGE；
  *　パッケージアドレス：COSの場合は、`cos://barrygz-1251783334.cosgz.myqcloud.com/fifa/fifa.2018.tar.gz`；
  * Stdoutログ：フォーマットは[COS、CFSパス記入](https://intl.cloud.tencent.com/document/product/599/13996)を参照してください；
  * Stderrログ：Stdoutログと同じ；
  * コマンドライン：`python merge.py /data`。

4.　ストレージマッピングを構成します。
![](https://main.qcloudimg.com/raw/63b58ffd1d778f39c938e00edaa61ddc.png)
 - 入力パスマッピング > COS/CFSパス：「fifa-predict」テンプレートのStdoutログパスを入力します。
 - 入力パスマッピング > ローカルパス：/data。

5.　タスクのJSONファイルをプレビューして正しいことを確認し、【保存】ボタンをクリックします。

### 五. ジョブの提出
1. 左側のナビゲーションバーの【ジョブ】オプションをクリックし、目標地域を選択して【新規作成】ボタンをクリックします。

2. ジョブの基本情報を構成します。例：
  * ジョブ名：fifa；
  * 優先度：デフォルト；
  * 説明：fifa 2018 model。

3. タスクフローページの左側にある**fifa-predict**と**fifa-merge**タスクを選択し、マウスを動かしてタスクを右側のキャンバスに配置します。**fifa-predict**タスクをクリックして矢印を**fifa-merge**タスクにドラッグします。
![](https://main.qcloudimg.com/raw/3dc9cf8e7ae8b2b5ae600d48cd58ee7c.png)

4. タスクフローの右側にある**タスク詳細**を開き、構成が正しいことを確認したら、【完了】ボタンをクリックします。

5. ジョブ実行情報の照合については、[情報照合]()を参照してください。
![](https://main.qcloudimg.com/raw/367517ad9dc347a8fbe46dcd9af8c38c.png)
 
6. レンダリング結果の照合については、[オブジェクト情報の確認]()を参照してください。
![](https://main.qcloudimg.com/raw/4e1a8c2b5e0320ee6f7be7f23a765e0b.png)

## 次に何ができますか？
本文では簡単なマシンラーニングの例を示します。ユーザーに最も基本的な機能だけを示すために、コンソール使用ガイドに従ってBatchのより高度な機能をテストし続けることができます。
- **豊富なCVM構成**：Batchは、豊富なCVM構成項目を提供して、ビジネスシナリオに基づいてCVM構成をカスタマイズできます。
- **リモートストレージマッピング**：Batchはストレージアクセスを最適化し、リモートストレージサービスへのアクセスをローカルファイルシステムの操作に単純化します。
- **複数モデルの同時トレーニング**：Batchは同時実行数の指定をサポートして、[環境変数](https://intl.cloud.tencent.com/document/product/599/11752)で異なる同時実行インスタンスを区別して、各インスタンスは異なるトレーニングデータを読み込んで、同時モデリングを実装します。

