## 操作シナリオ
Tencent Cloudの第6世代S6および第5世代インスタンスS5、M5、C4、IT5、D3は、第2世代インテリジェントIntel <sup>®</ sup>Xeon<sup>®</ sup>スケーラブルプロセッサCascadeLakeを全面的に採用しています。より多くの命令セットや機能を提供して、人工知能のアプリケーションのアクセラレーションに使用するとともに、多数のハードウェア拡張技術を統合することができます。中でも、AVX-512（アドバンスト・ベクトル・エクステンション）は、AI推論プロセスに強力な並列コンピューティング機能を提供し、ユーザーのディープラーニングの効果をより高めることができます。

ここではS5、M5インスタンスを例として、CVMでAVX512を介して人工知能アプリケーションをアクセラレーションする方法を説明します。

## モデル選択時の推奨事項[](id:RecommendedSelection)
CVMのさまざまなインスタンス仕様は、さまざまなアプリケーション開発に用いることができます。中でも[標準型 S6](https://intl.cloud.tencent.com/document/product/213/11518)、[標準型S5](https://intl.cloud.tencent.com/document/product/213/11518)および[メモリ型M5](https://intl.cloud.tencent.com/document/product/213/11518)は、 機械学習やディープラーニングに適しています。これらのインスタンスには、Intel<sup>®</sup> DL boost学習機能に適応する第2世代Intel<sup>®</sup> Xeon<sup>®</sup>プロセッサが搭載されています。推奨される構成は下表のとおりです。
<table>
<tr>
<th>プラットフォームタイプ</th><th>インスタンス仕様</th>
</tr>
<tr>
<td>ディープラーニングトレーニングプラットフォーム</td>
<td> 84vCPUの標準型S5インスタンスまたは48vCPUのメモリ型M5インスタンス。</td>
</tr>
<tr>
<td>ディープラーニング推論プラットフォーム</td>
<td>8/16/24/32/48vCPUの標準型S5インスタンスまたはメモリ型M5インスタンス。 </td>
</tr>
<tr>
<td>機械学習トレーニングまたは推論プラットフォーム</td>
<td>48vCPUの標準型S5インスタンスまたは24vCPUのメモリ型M5インスタンス。</td>
</tr>
</table>

 ## 有する利点
Intel<sup>®</sup> Xeon<sup>®</sup>スケーラブルプロセッサを使用して機械学習またはディープラーニングのワークロードを実行する場合、以下の利点があります。
- 大容量メモリ型ワークロード、医用画像、GAN、地震解析、遺伝子シーケンシングなどのシナリオで使用される3D-CNNトポロジーの処理に適しています。
- シンプルな`numactl`コマンドを使用した柔軟なコア制御をサポートしており、小さなバッチのリアルタイム推論にも適しています。
- 強力なエコシステムをサポートしており、大型クラスターで分散型トレーニングを直接実行できるため、大容量ストレージの追加や高価なキャッシュメカニズムを必要とする大規模なアーキテクチャトレーニングを回避することができます。
- 同じクラスター内で複数のワークロード（HPC、BigData、AIなど）をサポートしており、より優れたTCOを取得できます。
- SIMDによってアクセラレーションし、ディープラーニングのアプリケーションプログラムに関する多くの実質的なコンピューティング要件を満たします。
- 同じインフラストラクチャをトレーニングと推論に直接使用できます。

## 操作手順
### インスタンスを作成
CVMインスタンスを作成します。詳細については、[購入画面でインスタンスを作成](https://intl.cloud.tencent.com/document/product/213/4855)をご参照ください。そのうち、インスタンス仕様は、[モデル選択時の推奨事項](#RecommendedSelection) と実際の業務シナリオに従って選択する必要があります。下図のとおりです。
![](https://main.qcloudimg.com/raw/ceb104790caba9f281f4515f00d32585.png)
>?インスタンス仕様のパラメータについては、[インスタンス仕様](https://intl.cloud.tencent.com/document/product/213/11518)をご参照ください。

### インスタンスへのログイン
CVMインスタンスにログインします。詳細については、[標準方式を使用してLinuxインスタンス（推奨）にログイン](https://intl.cloud.tencent.com/document/product/213/5436)をご参照ください。

### デプロイ例
実際の業務シナリオに基づき、次の例を参照して人工知能プラットフォームをデプロイし、機械学習またはディープラーニングタスクを実行することができます。

<dx-accordion>
::: 例1：\sIntel<sup>®</sup>を使用して、ディープラーニングフレームワークを最適化します\sTensorFlow*
第2世代Intel<sup>®</sup>Xeon<sup>®</sup>スケーラブルプロセッサCascade LakeのPyTorchおよびIPEXでは、演算性能を最大限にアップさせるため、AVX-512命令セットの最適化が自動的に有効になります。

TensorFlow\*は、大規模な機械学習とディープラーニングに用いる、人気のフレームワークの1つです。この例を参照して、インスタンスのトレーニングと推論性能を向上させることができます。フレームワークのデプロイに関する情報については、[Intel<sup>®</sup> Optimization for TensorFlow\* Installation Guide](https://software.intel.com/content/www/us/en/develop/articles/intel-optimization-for-tensorflow-installation-guide.html)をご参照ください。操作手順は次のとおりです。

#### TensorFlow\*フレームワークのデプロイ
1. CVMにPythonをインストールします。ここでは、Python3.7を例とします。
2. 以下のコマンドを実行して、Intel<sup>®</sup>に最適化されたTensorFlow\*バージョンのintel-tensorflowをインストールします。
<dx-alert infotype="explain" title="">
最新の機能と最適化を利用するため、**2.4.0およびそれ以降のバージョン**を使用することをお勧めします。
</dx-alert> 
```
pip install intel-tensorflow
```

#### ランタイム最適化パラメータを設定
ランタイムパラメータの最適化方法を選択します。 通常、以下の2つの実行インターフェースを使用して、異なる最適化設定を採用します。実際のニーズに応じて選択できます。パラメータ最適化の設定に関する説明については、[General Best Practices for Intel<sup>®</sup> Optimization for TensorFlow](https://github.com/IntelAI/models/blob/master/docs/general/tensorflow/GeneralBestPractices.md)をご参照ください。
 - **Batch inference**：BatchSize >1に設定し、1秒あたりに処理できる入力テンソルの総数を測定します。通常の状況では、Batch Inference方式は、同じCPU socketですべての物理コアを使用することによって最高のパフォーマンスを実現できます。
 - **On-line Inference**（リアルタイム推論とも呼びます）：BS = 1に設定し、単一の入力テンソルの処理（バッチサイズは1）に必要な時間を測定します。リアルタイム推論スキームでは、マルチインスタンスを同時実行して、最高のスループットを得ることができます。

操作手順は次のとおりです。
1. 以下のコマンドを実行して、システム内の物理コアの数を取得します。
```
lscpu | grep "Core(s) per socket" | cut -d':' -f2 | xargs
```
2. 最適化パラメータを設定します。以下のいずれかの方法を選択できます。
 - 環境の実行パラメータを設定します。環境変数ファイルに、以下の構成を追加します。
```
 export OMP_NUM_THREADS= # <physicalcores>
 export KMP_AFFINITY="granularity=fine,verbose,compact,1,0"
 export KMP_BLOCKTIME=1
 export KMP_SETTINGS=1
 export TF_NUM_INTRAOP_THREADS= # <physicalcores>
 export TF_NUM_INTEROP_THREADS=1
 export TF_ENABLE_MKL_NATIVE_FORMAT=0
```
 - コードに環境変数設定を追加します。実行中のPythonコードに、以下の環境変数設定を追加します：
```
import os
os.environ["KMP_BLOCKTIME"] = "1"
os.environ["KMP_SETTINGS"] = "1"
os.environ["KMP_AFFINITY"]= "granularity=fine,verbose,compact,1,0"
if FLAGS.num_intra_threads > 0:
    os.environ["OMP_NUM_THREADS"]= # <physical cores>
os.environ["TF_ENABLE_MKL_NATIVE_FORMAT"] = "0"
config = tf.ConfigProto()
config.intra_op_parallelism_threads = # <physical cores>
config.inter_op_parallelism_threads = 1
tf.Session(config=config)
```

#### TensorFlow\*ディープラーニングモデルの推論を実行する
[Image Recognition with ResNet50, ResNet101 and InceptionV3](https://github.com/IntelAI/models/blob/master/docs/image_recognition/tensorflow/Tutorial.md)を参照して、他の機械学習/ディープラーニングモデルの推論を実行してください。ここでは、benchmarkを例として、ResNet50のinference benchmarkを実行する方法を説明します。詳細については、[ResNet50 (v1.5)](https://github.com/IntelAI/models/blob/master/benchmarks/image_recognition/tensorflow/resnet50v1_5/README.md)をご参照ください。

#### TensorFlow\*ディープラーニングモデルのトレーニングを実行する
ここでは、ResNet50のtraining benchmarkを実行する方法を説明します。詳細については、[FP32 Training Instructions](https://github.com/IntelAI/models/blob/master/benchmarks/image_recognition/tensorflow/resnet50v1_5/README.md#fp32-training-instructions)をご参照ください。

#### TensorFlowの性能デモンストレーション

パフォーマンスデータについては、[Improving TensorFlow* Inference Performance on Intel® Xeon® Processors](https://www.intel.com/content/www/us/en/artificial-intelligence/posts/improving-tensorflow-inference-performance-on-intel-xeon-processors.html)をご参照ください。実際のモードと物理構成によって、パフォーマンスデータはある程度異なります。以下のパフォーマンスデータはあくまでも参考です。
 - **レイテンシー性能**：
    テストを通じて、batch sizeが1の場合に画像分類とターゲット検出に適したモデルをいくつか選択すると、AVX512最適化バージョンでは、最適化されていないバージョンと比べて推論性能が明らかに向上していることがわかります。例えば、レイテンシーに関しては、最適化されたResNet 50のレイテンシーは元の45%まで低減します。
 - **スループット性能**：
    batch sizeを大きくしてスループット性能をテストし、画像分類やターゲット検出に適したモデルをいくつか選択してテストします。スループット性能データも明らかに向上していることがわかります。最適化後、ResNet 50のパフォーマンスは元の1.98倍までアップします。

:::
::: 例2：ディープラーニングフレームワークをデプロイする\sPyTorch*
#### デプロイ手順
1. CVMにPython3.6以降のバージョンをインストールします。ここでは、Python3.7を例とします。
2. [Intel<sup>®</sup> Extension for PyTorc 公式github repo](https://github.com/intel/intel-extension-for-pytorch#installation)に移動し、インストールガイドに記載されている情報に従って、PyTorchおよびntel<sup>®</sup> Extension for PyTorch (IPEX)のコンパイルとインストールを行います。

#### ランタイム最適化パラメータを設定

第2世代Intel<sup>®</sup>Xeon<sup>®</sup>スケーラブルプロセッサCascade LakeのPyTorchおよびIPEXでは、演算性能を最大限にアップさせるため、AVX-512命令セットの最適化が自動的に有効になります。

この手順に従って、ランタイムパラメータの最適化方法を設定できます。パラメータ最適化の設定手順の詳細については、[Maximize Performance of Intel® Software Optimization for PyTorch* on CPU](https://software.intel.com/content/www/us/en/develop/articles/how-to-get-better-performance-on-pytorchcaffe2-with-intel-acceleration.html)をご参照ください。
 - **Batch inference**：BatchSize >1に設定し、1秒あたりに処理できる入力テンソルの総数を測定します。通常の状況では、Batch Inference方式は、同じCPU socketですべての物理コアを使用することによって最高のパフォーマンスを実現できます。
 - **On-line Inference**（リアルタイム推論とも呼びます）：BatchSize = 1に設定し、単一の入力テンソルの処理（バッチサイズは1）に必要な時間を測定します。リアルタイム推論スキームでは、マルチインスタンスを同時実行して、最高のスループットを得ることができます。

操作手順は次のとおりです。

1. 以下のコマンドを実行して、システム内の物理コアの数を取得します。
```
lscpu | grep "Core(s) per socket" | cut -d':' -f2 | xargs
```
2. 最適化パラメータを設定します。以下のいずれかの方法を選択できます。
 - 環境の実行パラメータを設定し、GNU OpenMP* Librariesを使用します。環境変数ファイルに、以下の構成を追加します。
```
export OMP_NUM_THREADS=physicalcores
export GOMP_CPU_AFFINITY="0-<physicalcores-1>"
export OMP_SCHEDULE=STATIC
export OMP_PROC_BIND=CLOSE
```
 - 環境の実行パラメータを設定し、Inte OpenMP* Librariesを使用します。環境変数ファイルに、以下の構成を追加します。
```
export OMP_NUM_THREADS=physicalcores
export LD_PRELOAD=<path_to_libiomp5.so>
export KMP_AFFINITY="granularity=fine,verbose,compact,1,0"
export KMP_BLOCKTIME=1
export KMP_SETTINGS=1
```


#### PyTorch*ディープラーニングモデルの推論の実行とトレーニングの最適化の提案

- モデル推論を実行する場合、Intel<sup>®</sup> Extension for PyTorchを使用してパフォーマンスを向上させることができます。サンプルコードは次のとおりです。
```
import intel_pytorch_extension
...
net = net.to('xpu')       # Move model to IPEX format
data = data.to('xpu')     # Move data  to IPEX format
...
output = net(data)        # Perform inference with IPEX
output = output.to('cpu') # Move output back to ATen format
```
- 推論とトレーニングでは、jemallocを使用してパフォーマンスを最適化できます。jemallocとは、断片化の回避やスケール可能な並行処理に対応していることを強調する、`malloc(3)`の汎用実装であり、システムにメモリアロケータを提供することを目的としています。jemallocは、標準のアロケータ機能を超える多くのイントロスペクション、メモリ管理、および変更機能を提供しています。 詳細については、[jemalloc](https://github.com/jemalloc/jemalloc/wiki)および[サンプルコード](https://github.com/mingfeima/op_bench-py/blob/master/run.sh)をご参照ください。
- 複数のsocketを使用した分散型トレーニングの詳細については、[PSSP-Transformerの分散型CPUトレーニングスクリプト](https://github.com/mingfeima/pssp/blob/master/pssp-transformer/dist_train_cpu.sh)をご参照ください。

#### パフォーマンス結果

Intelの第2世代Intel<sup>®</sup>Xeon<sup>®</sup>スケーラブルプロセッサCascade Lakeをベースとする、2*CPU（28コア/CPU）および384Gメモリシナリオにおける、さまざまなモデルテストのパフォーマンスデータについては、[パフォーマンステストデータ](https://software.intel.com/content/www/us/en/develop/articles/intel-and-facebook-collaborate-to-boost-pytorch-cpu-performance.html)をご参照ください。実際のモデルや物理構成が異なるため、パフォーマンスデータにも差異が生じます。ここに記載されているテストデータは、あくまでも参考です。


:::
::: 例3：\sIntel<sup>®</sup>AI\sの低精度最適化ツールを使用してアクセラレーションする


Intel<sup>®</sup> 低精度最適化ツールは、オープンソースのPythonライブラリです。これは、シンプルで使いやすい、ニューラルネットワークフレームワーク間の低精度定量的推論インターフェースを提供することを目的としています。ユーザーは、インターフェースを呼び出すだけでモデルを定量化し、生産性を向上させることによって、第3世代Intel<sup>®</sup> Xeon<sup>®</sup> DL Boostスケーラブルプロセッサプラットフォームでの推論性能をアクセラレーションすることができます。使用法の詳細については、[Intel<sup>®</sup> 低精度定量化ツールコードライブラリ](https://github.com/Intel/lpot/)をご参照ください。

#### サポートされているニューラルネットワークフレームワークバージョン
Intel<sup>®</sup>低精度最適化ツールは以下をサポートしています。
Intel<sup>®</sup> 最適化したTensorFlow* `v1.15.0`、`v1.15.0up1`、`v1.15.0up2`、 `v2.0.0`、`v2.1.0`、`v2.2.0`、`v2.3.0`および`v2.4.0`。
Intel<sup>®</sup> 最適化したPyTorch `v1.5.0+cpu`および`v1.6.0+cpu`。
Intel<sup>®</sup> 最適化したMXNet `v1.6.0`、`v1.7.0`およびONNX-Runtime `v1.6.0`。

#### 実装フレームワーク
Intel<sup>®</sup> 低精度最適化ツールの実装フレームワーク略図は次のとおりです。
![](https://main.qcloudimg.com/raw/6062f647b40e2900354fbc73d8a4248a.jpg)

#### ワークフロー
Intel<sup>®</sup> 低精度最適化ツールのワークフローチャートは次のとおりです。
![](https://main.qcloudimg.com/raw/acbc366d69819b443064ba5df58608fc.png)

#### 定量的モデルのパフォーマンスと精度の例

Intel<sup>®</sup> 低精度最適化ツールによって定量化されたモデルの第2世代Intel<sup>®</sup>Xeon<sup>®</sup>スケーラブルプロセッサCascade Lakeにおいて得られるパフォーマンスと精度の一部は次のとおりです。

<table class="docutils">
<thead>
  <tr>
    <th rowspan="2">Framework</th>
    <th rowspan="2">Version</th>
    <th rowspan="2">Model</th>
    <th colspan="3">Accuracy</th>
    <th>Performance speed up</th>
  </tr>
  <tr>
    <td>INT8 Tuning Accuracy</td>
    <td>FP32 Accuracy Baseline</td>
    <td>Acc Ratio [(INT8-FP32)/FP32]</td>
    <td>Realtime Latency Ratio[FP32/INT8]</td>
  </tr>
</thead>
<tbody>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>resnet50v1.5</td>
    <td>76.92%</td>
    <td>76.46%</td>
    <td>0.60%</td>
    <td>3.37x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>resnet101</td>
    <td>77.18%</td>
    <td>76.45%</td>
    <td>0.95%</td>
    <td>2.53x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>inception_v1</td>
    <td>70.41%</td>
    <td>69.74%</td>
    <td>0.96%</td>
    <td>1.89x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>inception_v2</td>
    <td>74.36%</td>
    <td>73.97%</td>
    <td>0.53%</td>
    <td>1.95x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>inception_v3</td>
    <td>77.28%</td>
    <td>76.75%</td>
    <td>0.69%</td>
    <td>2.37x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>inception_v4</td>
    <td>80.39%</td>
    <td>80.27%</td>
    <td>0.15%</td>
    <td>2.60x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>inception_resnet_v2</td>
    <td>80.38%</td>
    <td>80.40%</td>
    <td>-0.02%</td>
    <td>1.98x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>mobilenetv1</td>
    <td>73.29%</td>
    <td>70.96%</td>
    <td>3.28%</td>
    <td>2.93x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>ssd_resnet50_v1</td>
    <td>37.98%</td>
    <td>38.00%</td>
    <td>-0.05%</td>
    <td>2.99x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>mask_rcnn_inception_v2</td>
    <td>28.62%</td>
    <td>28.73%</td>
    <td>-0.38%</td>
    <td>2.96x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>vgg16</td>
    <td>72.11%</td>
    <td>70.89%</td>
    <td>1.72%</td>
    <td>3.76x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>vgg19</td>
    <td>72.36%</td>
    <td>71.01%</td>
    <td>1.90%</td>
    <td>3.85x</td>
  </tr>
</tbody>
</table>

<table class="docutils">
<thead>
  <tr>
    <th rowspan="2">Framework</th>
    <th rowspan="2">Version</th>
    <th rowspan="2">Model</th>
    <th colspan="3">Accuracy</th>
    <th>Performance speed up</th>
  </tr>
  <tr>
    <td>INT8 Tuning Accuracy</td>
    <td>FP32 Accuracy Baseline</td>
    <td>Acc Ratio [(INT8-FP32)/FP32]</td>
    <td>Realtime Latency Ratio[FP32/INT8]</td>
  </tr>
</thead>
<tbody>
  <tr>
    <td>pytorch</td>
    <td>1.5.0+cpu</td>
    <td>resnet50</td>
    <td>75.96%</td>
    <td>76.13%</td>
    <td>-0.23%</td>
    <td>2.46x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.5.0+cpu</td>
    <td>resnext101_32x8d</td>
    <td>79.12%</td>
    <td>79.31%</td>
    <td>-0.24%</td>
    <td>2.63x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_base_mrpc</td>
    <td>88.90%</td>
    <td>88.73%</td>
    <td>0.19%</td>
    <td>2.10x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_base_cola</td>
    <td>59.06%</td>
    <td>58.84%</td>
    <td>0.37%</td>
    <td>2.23x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_base_sts-b</td>
    <td>88.40%</td>
    <td>89.27%</td>
    <td>-0.97%</td>
    <td>2.13x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_base_sst-2</td>
    <td>91.51%</td>
    <td>91.86%</td>
    <td>-0.37%</td>
    <td>2.32x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_base_rte</td>
    <td>69.31%</td>
    <td>69.68%</td>
    <td>-0.52%</td>
    <td>2.03x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_large_mrpc</td>
    <td>87.45%</td>
    <td>88.33%</td>
    <td>-0.99%</td>
    <td>2.65x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_large_squad</td>
    <td>92.85</td>
    <td>93.05</td>
    <td>-0.21%</td>
    <td>1.92x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_large_qnli</td>
    <td>91.20%</td>
    <td>91.82%</td>
    <td>-0.68%</td>
    <td>2.59x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_large_rte</td>
    <td>71.84%</td>
    <td>72.56%</td>
    <td>-0.99%</td>
    <td>1.34x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_large_cola</td>
    <td>62.74%</td>
    <td>62.57%</td>
    <td>0.27%</td>
    <td>2.67x</td>
  </tr>
</tbody>
</table>

<dx-alert infotype="explain" title="">
表のPyTorchとTensorflowはどちらも、Intelをベースとして最適化されたフレームワークです。完全にサポートされている定量的モデルのリストについては、[オンラインドキュメント](https://github.com/intel/lpot/blob/master/docs/full_model_list.md)をご参照ください。
</dx-alert>



#### Intel<sup>®</sup>低精度最適化ツールのインストールと使用例 

1. 以下のコマンドを順番に実行し、anacondaを使用してlpotという名前のpython3.x仮想環境を構築します。ここでは、python 3.7を例とします。
```plaintext
conda create -n lpot python=3.7
conda activate lpot
```
2. lpotをインストールするには、以下の2つの方法があります。
    - 以下のコマンドを実行して、バイナリーファイルからインストールします。
``` plaintext
pip install lpot
```
    - 以下のコマンドを実行して、ソースからインストールします。
```plaintext
 git clone https://github.com/intel/lpot.git
 cd lpot
 pip install –r requirements.txt
 python setup.py install
```
3. TensorFlow ResNet50 v1.0を定量化します。ここでは、ResNet50 v1.0を例として、このツールを使用して定量化する方法を説明します。
    1. データセットの準備をします。
以下のコマンドを実行して、ImageNet validationデータセットをダウンロードして解凍します。
```plaintext
mkdir –p img_raw/val && cd img_raw
wget http://www.image-net.org/challenges/LSVRC/2012/dd31405981
ef5f776aa17412e1f0c112/ILSVRC2012_img_val.tar
tar –xvf ILSVRC2012_img_val.tar -C val
```
以下のコマンドを実行して、imageファイルをlabelで分類されたサブディレクトリに移動します。
```plaintext
cd val
wget -qO -https://raw.githubusercontent.com/soumith/
imagenetloader.torch/master/valprep.sh | bash
```
​以下のコマンドを実行して、スクリプト prepare_dataset.shを使用して、元のデータをTFrecord形式に変換します。
```plaintext
cd examples/tensorflow/image_recognition
bash prepare_dataset.sh --output_dir=./data --raw_dir=/PATH/TO/img_raw/val/ 
--subset=validation
```
​データセットの詳細情報については、[Prepare Dataset](https://github.com/intel/lpot/tree/master/examples/tensorflow/image_recognition#2-prepare-dataset)をご参照ください。
    2. 以下のコマンドを実行して、モデルを準備します。
```plaintext
wget https://storage.googleapis.com/intel-optimized-tensorflow/
 models/v1_6/resnet50_fp32_pretrained_model.pb
```
    3. 以下のコマンドを実行して、Tuningを実行します。
ファイル `examples/tensorflow/image_recognition/resnet50_v1.yaml`を変更して、`quantization\calibration`、`evaluation\accuracy`、`evaluation\performance` という3つの部分のデータセットパスがユーザーのローカルの実際のパス、つまりデータセットの準備段階で生成されたTFrecordデータが所在する場所を指すようにします。詳細については、[ResNet50 V1.0](https://github.com/intel/lpot/tree/master/examples/tensorflow/image_recognition#1-resnet50-v10)をご参照ください。
```plaintext
cd examples/tensorflow/image_recognition
bash run_tuning.sh --config=resnet50_v1.yaml \
--input_model=/PATH/TO/resnet50_fp32_pretrained_model.pb \
--output_model=./lpot_resnet50_v1.pb
```
    4. 以下のコマンドを実行して、Benchmarkを実行します。
```plaintext
bash run_benchmark.sh --input_model=./lpot_resnet50_v1.pb
--config=resnet50_v1.yaml
```
​出力結果は次のとおりです。パフォーマンスデータはあくまでも参考です：
```shell
 accuracy mode benchmarkresult:
 Accuracy is 0.739
 Batch size = 32
 Latency: 1.341 ms
 Throughput: 745.631 images/sec
 performance mode benchmark result:
 Accuracy is 0.000
 Batch size = 32
 Latency: 1.300 ms
 Throughput: 769.302 images/sec
```
:::
::: 例4：\sIntel<sup>®</sup>\sDistribution\sof\sOpenVINO™\sToolkit\sを使用して推論のアクセラレーションを行う
Intel<sup>®</sup> Distribution of OpenVINO™ Toolkitとは、コンピュータビジョンやその他のディープラーニングアプリケーションのデプロイを高速化できるツールキットであり、Intelプラットフォームのさまざまなアクセラレーター（CPU、GPU、FPGAおよびMovidiusのVPUを含む）をサポートしてディープラーニングを行うとともに、異種ハードウェアを直接サポートすることができます。

Intel<sup>®</sup> Distribution of OpenVINO™ Toolkitは、TensorFlow\*、PyTorch\*などを介してトレーニングされたモデルを最適化できます。これには、モデルオプティマイザー、推論エンジン、Open Model Zoo、トレーニング後の最適化ツール（Post-training Optimization Tool）など、一連のデプロイツールが含まれます。

- **モデルオプティマイザー（Model optimizer）**：Caffe\*、TensorFlow\* 、PyTorch\*およびMxnet\*など、さまざまなフレームワークによってトレーニングされたモデルを中間表現(IR)に変換します。
- **推論エンジン（Inference Engine）**：変換されたIRをCPU、GPU、FPGAおよびVPUなどのハードウェアに配置して実行し、ハードウェアアクセラレーションキットを自動的に呼び出して推論性能のアクセラレーションを行います。

[Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit公式ウェブサイト](https://software.intel.com/content/www/us/en/develop/tools/openvino-toolkit.html)に移動するか、または[オンラインドキュメント](https://docs.openvinotoolkit.org/latest/index.html)をご覧いただけば、詳細情報が確認できます。

#### ワークフロー
Intel<sup>®</sup> Distribution of OpenVINO™ Toolkitツールキットのワークフローチャートは次のとおりです。
![](https://main.qcloudimg.com/raw/98afcac361352773801fbe863d21b912.png)

#### Intel<sup>®</sup> Distribution of OpenVINO™ Toolkitの推論性能
The Intel® Distribution of OpenVINO™ツールは、さまざまなIntelプロセッサと高速ハードウェアで最適化を実装します。Intel <sup>®</ sup>Xeon<sup>®</ sup>スケーラブルプロセッサプラットフォームでは、Intel <sup>®</ sup> DLBoostおよびAVX-512命令セットを使用して推論ネットワークをアクセラレーションします。
 #### Intel<sup>®</sup> Distribution of OpenVINO™ Toolkitディープラーニング開発キット（DLDT）の使用
 以下の資料をご参照ください
- [Intel<sup>®</sup>ディープラーニングデプロイツールキットの概要](https://docs.openvinotoolkit.org/downloads/cn/I03030-9-Introduction%20to%20Intel_%20Deep%20Learning%20Deployment%20Toolkit%20-%20OpenVINO_%20Toolkit.pdf)
-  [画像分類C++の例（非同期モード）](https://docs.openvinotoolkit.org/downloads/cn/I03030-10-Image%20Classification%20Cpp%20Sample%20Async%20-%20OpenVINO_%20Toolkit.pdf)
-  [オブジェクト検出C++の例（SSD）](https://docs.openvinotoolkit.org/downloads/cn/I03030-11-Object%20Detection%20Cpp%20Sample%20SSD%20-%20OpenVINO_%20Toolkit.pdf)
-  [自動音声認識C++の例](https://docs.openvinotoolkit.org/downloads/cn/I03030-12-Automatic%20Speech%20Recognition%20Cpp%20%20Sample%20-%20OpenVINO_%20Toolkit.pdf)
-  [動作認識Python*デモンストレーション](https://docs.openvinotoolkit.org/downloads/cn/I03030-13-Action%20Recognition%20Python%20Demo%20-%20OpenVINO_%20Toolkit.pdf)
-  [クロスロードカメラC++デモンストレーション](https://docs.openvinotoolkit.org/downloads/cn/I03030-14-Crossroad%20Camera%20Cpp%20%20Demo%20-%20OpenVINO_%20Toolkit.pdf)
- [姿勢推定C++デモンストレーション](https://docs.openvinotoolkit.org/downloads/cn/I03030-15-Human%20Pose%20Estimation%20Cpp%20Demo%20-%20OpenVINO_%20Toolkit.pdf)

#### Intel<sup>®</sup> Distribution of OpenVINO™ Toolkitのベンチマークテスト
詳細については、[Linux*用Intel<sup>®</sup> OpenVINO™ツールキットディストリビューション版のインストール](https://docs.openvinotoolkit.org/downloads/cn/I03030-5-Install%20Intel_%20Distribution%20of%20OpenVINO_%20toolkit%20for%20Linux%20-%20OpenVINO_%20Toolkit.pdf)をご参照ください。

:::
</dx-accordion>

