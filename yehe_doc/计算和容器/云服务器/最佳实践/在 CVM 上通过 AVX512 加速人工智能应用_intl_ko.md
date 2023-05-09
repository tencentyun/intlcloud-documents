## 작업 시나리오
Tencent Cloud의 6 시리즈 인스턴스 S6, M5, C4, IT5, D3에는 스마트 Intel<sup>®</sup> Xeon<sup>®</sup> 2 시리즈 확장 가능 프로세서 Cascade Lake가 탑재되었습니다. 더 많은 명령어 집합 및 특성을 제공하여 AI 애플리케이션 가속에 사용할 수 있습니다. 대량의 하드웨어 강화 기술이 통합되어 있으며, AVX-512(고급 벡터 확장)는 AI 추론 과정에 강력한 병렬 컴퓨팅 기능을 제공하여 보다 향상된 딥러닝 효과를 얻을 수 있습니다.

본 문서는 S5와 M5 인스턴스를 예시로 CVM에서 AVX512를 통해 AI 애플리케이션을 가속화하는 방법을 소개합니다.

## 권장 모델[](id:RecommendedSelection)
CVM의 다양한 인스턴스 사양은 여러 가지 애플리케이션 개발에 사용할 수 있습니다. [표준형 S6](https://intl.cloud.tencent.com/document/product/213/11518),[표준형 S5](https://intl.cloud.tencent.com/document/product/213/11518) 및 [메모리형 M5](https://intl.cloud.tencent.com/document/product/213/11518)는 머신러닝 또는 딥러닝에 적합합니다. 이 인스턴스에는 Intel<sup>®</sup> Xeon<sup>®</sup> 2 시리즈 프로세서가 탑재되어 있으며, Intel<sup>®</sup> DL boost 학습 기능을 적용할 수 있습니다. 권장 사양은 다음과 같습니다.
<table>
<tr>
<th>플랫폼 유형</th><th>인스턴스 사양</th>
</tr>
<tr>
<td>딥러닝 학습 플랫폼</td>
<td> 84vCPU의 표준형 S5 인스턴스 또는 48vCPU의 메모리형 M5 인스턴스</td>
</tr>
<tr>
<td>딥러닝 추론 플랫폼</td>
<td>8/16/24/32/48vCPU의 표준형 S5 인스턴스 또는 메모리형 M5 인스턴스</td>
</tr>
<tr>
<td>머신러닝 학습 또는 추론 플랫폼</td>
<td>48vCPU의 표준형 S5 인스턴스 또는 24vCPU의 메모리형 M5 인스턴스</td>
</tr>
</table>

 ## 장점
Intel<sup>®</sup> Xeon<sup>®</sup> 확장 가능 프로세서를 사용한 머신러닝 또는 딥러닝 워크로드 실행에는 다음과 같은 장점이 있습니다.
- 대규모 메모리형 워크로드, 의료 영상, GAN, 지진 분석, 유전자 시퀀서 등의 시나리오에서 사용하는 3D-CNN 토폴로지 처리에 적합합니다.
- 간단한 `numactl` 명령어를 사용해 효율적으로 코어를 제어할 수 있으며, 소량의 실시간 추론에도 사용할 수 있습니다.
- 강력한 생태 시스템 지원으로 대형 클러스터에서 분산형 학습을 직접 진행할 수 있어 별도의 대용량 스토리지와 고가의 캐시 메커니즘 없이 대규모 아키텍처 학습을 진행할 수 있습니다.
- 동일한 클러스터에서 다수의 워크로드(예: HPC, BigData, AI 등)를 지원하여 더 우수한 TCO를 획득할 수 있습니다.
- SIMD 가속을 통해 다양한 실제 딥러닝 응용 프로그램의 컴퓨팅 요구사항을 충족합니다.
- 동일한 인프라를 직접 학습 및 추론에 사용할 수 있습니다.

## 작업 순서
### 인스턴스 생성
CVM 인스턴스 생성에 대한 자세한 내용은 [구매 페이지를 통한 인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참고하십시오. 인스턴스 사양은 [권장 모델](#RecommendedSelection) 및 실제 비즈니스 시나리오에 따라 아래 이미지와 같이 선택하십시오.
![](https://main.qcloudimg.com/raw/ceb104790caba9f281f4515f00d32585.png)
>?자세한 인스턴스 사양 매개변수의 소개는 [인스턴스 스펙](https://intl.cloud.tencent.com/document/product/213/11518)을 참고하십시오.

#### 로그인 인스턴스
CVM 인스턴스에 로그인합니다. 자세한 내용은 [표준 방식으로 Linux 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5436)을 참고하십시오.

### 배포 예시
실제 비즈니스 시나리오에 따라 다음의 예시를 참고하여 AI 플랫폼을 배포하고, 머신러닝 또는 딥러닝 작업을 진행할 수 있습니다.

<dx-accordion>
::: 예시1:\sIntel<sup>®</sup>을\s사용해\s딥러닝\s프레임워크\sTensorFlow*\s최적화
스마트 Intel<sup>®</sup> Xeon<sup>®</sup> 2 시리즈 확장 가능 프로세서 Cascade Lake에서 PyTorch와 IPEX는 자동으로 AVX-512 명령어 집합을 최적화하여 연산 능력을 최대로 높입니다.

TensorFlow\*는 대규모 머신러닝 및 딥러닝에 사용되는 인기 프레임워크 중 하나입니다. 해당 예시를 참고하여 인스턴스의 학습 능력과 추론 능력을 높일 수 있습니다. 프레임워크 배포에 대한 자세한 정보는 [Intel<sup>®</sup> Optimization for TensorFlow\* Installation Guide](https://software.intel.com/content/www/us/en/develop/articles/intel-optimization-for-tensorflow-installation-guide.html)를 참고하십시오. 작업 순서는 다음과 같습니다.

#### TensorFlow\* 프레임워크 배포
1. CVM에 Python을 설치합니다. 본 문서는 Python 3.7을 예시로 합니다.
2. 다음 명령어를 실행하여 Intel<sup>®</sup>에 최적화된 TensorFlow\* 버전인 intel-tensorflow를 설치합니다.
<dx-alert infotype="explain" title="">
최신 기능 획득 및 최적화를 위해 **2.4.0 이상 버전** 사용을 권장합니다.
</dx-alert> 
```
pip install intel-tensorflow
```

#### 실행 시 매개변수 최적화 설정
실행 시 매개변수 최적화 방식을 선택합니다. 일반적으로 다음 두 가지 실행 인터페이스를 사용하여 서로 다른 최적화 설정을 채택합니다. 실제 필요에 따라 선택할 수 있습니다. 매개변수 최적화 설정에 대한 자세한 설명은 [General Best Practices for Intel<sup>®</sup> Optimization for TensorFlow](https://github.com/IntelAI/models/blob/master/docs/general/tensorflow/GeneralBestPractices.md)를 참고하십시오.
 - **Batch inference**: BatchSize > 1로 설정하고, 초당 처리 가능한 입력 텐서의 총수를 측정합니다. 일반적으로 Batch Inference 방식은 동일한 CPU socket의 모든 물리 코어를 사용해 최적의 성능을 구현합니다.
 - **On-line Inference**(실시간 추론): BS = 1로 설정하고, 단일 입력 텐서(배치 1개의 크기는 1) 처리에 소요되는 시간을 측정합니다. 실시간 추론 방식은 여러 인스턴스의 동시 실행을 통해 최적의 처리량을 구현합니다.

작업 순서는 다음과 같습니다.
1. 다음 명령어를 실행하여 시스템의 물리 코어 개수를 확인합니다.
```
lscpu | grep "Core(s) per socket" | cut -d':' -f2 | xargs
```
2. 최적화 매개변수를 설정합니다. 다음 방식 중 한 가지를 선택할 수 있습니다.
 - 환경 실행 매개변수를 설정합니다. 환경 변수 파일에 다음 설정을 추가합니다.
```
 export OMP_NUM_THREADS= # <physicalcores>
 export KMP_AFFINITY="granularity=fine,verbose,compact,1,0"
 export KMP_BLOCKTIME=1
 export KMP_SETTINGS=1
 export TF_NUM_INTRAOP_THREADS= # <physicalcores>
 export TF_NUM_INTEROP_THREADS=1
 export TF_ENABLE_MKL_NATIVE_FORMAT=0
```
 - 코드에 환경 변수 설정을 추가합니다. 실행 중인 Python 코드에 다음의 환경 변수 설정을 추가합니다.
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

#### TensorFlow\* 딥러닝 모델의 추론 실행
[Image Recognition with ResNet50, ResNet101 and InceptionV3](https://github.com/IntelAI/models/blob/master/docs/image_recognition/tensorflow/Tutorial.md)를 참고하여 기타 머신러닝/딥러닝 모델의 추론을 실행할 수 있습니다. 본 문서는 benchmark를 예시로 ResNet50의 inference benchmark를 실행하는 방법을 소개합니다. 자세한 내용은 [ResNet50 (v1.5)](https://github.com/IntelAI/models/blob/master/benchmarks/image_recognition/tensorflow/resnet50v1_5/README.md)을 참고하십시오.

#### TensorFlow\* 딥러닝 모델의 학습 실행
본 문서는 ResNet50의 training benchmark를 실행하는 방법을 소개합니다. 자세한 내용은 [FP32 Training Instructions](https://github.com/IntelAI/models/blob/master/benchmarks/image_recognition/tensorflow/resnet50v1_5/README.md#fp32-training-instructions)를 참고하십시오.

#### TensorFlow 성능 안내

성능 데이터는 [Improving TensorFlow* Inference Performance on Intel® Xeon® Processors](https://www.intel.com/content/www/us/en/artificial-intelligence/posts/improving-tensorflow-inference-performance-on-intel-xeon-processors.html)를 참고하십시오. 실제 모드 및 물리 설정에 따라 성능 데이터에 차이가 있을 수 있습니다. 다음 성능 데이터는 참고용입니다.
 - **딜레이 성능**:
    batch size가 1일 때 이미지 분류, 타깃 검증에 사용하는 일부 모델을 선별하여 테스트를 진행하면, AVX512 최적화 버전이 제공하는 추론 성능이 최적화하지 않은 버전보다 뚜렷하게 향상된 것을 확인할 수 있습니다. 예를 들어, 딜레이 성능을 최적화한 ResNet 50의 딜레이는 기존 대비 45% 낮아집니다.
 - **처리량 성능**:
    batch size를 확대 설정해 처리량 성능을 테스트할 수 있습니다. 이미지 분류, 타깃 검증에 사용하는 일부 모델을 선별하여 테스트를 진행하면, 처리량 성능 데이터가 뚜렷하게 향상된 것을 확인할 수 있습니다. 최적화한 ResNet 50의 성능은 기존 대비 1.98배 향상됩니다.

:::
::: 예시2:\s딥러닝\s프레임워크\sPyTorch*\s배포

#### 설치 순서
1. CVM에 Python3.6 이상의 버전을 설치합니다. 본 문서는 Python 3.7을 예시로 합니다.
2. [Intel<sup>®</sup> Extension for PyTorch 공식 홈페이지 github repo](https://github.com/intel/intel-extension-for-pytorch#installation)의 설치 가이드에서 제공하는 정보에 따라 PyTorch 및 Intel<sup>®</sup> Extension for PyTorch(IPEX)를 컴파일 및 설치합니다.

#### 실행 시 매개변수 최적화 설정

스마트 Intel<sup>®</sup> Xeon<sup>®</sup> 2 시리즈 확장 가능 프로세서 Cascade Lake에서 PyTorch와 IPEX는 자동으로 AVX-512 명령어 집합을 최적화하여 연산 능력을 최대로 높입니다.

이 단계에 따라 실행 시 매개변수 최적화 방식을 설정할 수 있습니다. 매개변수 최적화 설정에 대한 자세한 설명은 [Maximize Performance of Intel® Software Optimization for PyTorch* on CPU](https://software.intel.com/content/www/us/en/develop/articles/how-to-get-better-performance-on-pytorchcaffe2-with-intel-acceleration.html)를 참고하십시오.
 - **Batch inference**: BatchSize > 1로 설정하고, 초당 처리 가능한 입력 텐서의 총수를 측정합니다. 일반적으로 Batch Inference 방식은 동일한 CPU socket의 모든 물리 코어를 사용해 최적의 성능을 구현합니다.
 - **On-line Inference**(실시간 추론): BatchSize = 1로 설정하고, 단일 입력 텐서(배치 1개의 크기는 1) 처리에 소요되는 시간을 측정합니다. 실시간 추론 방식은 여러 인스턴스의 동시 실행을 통해 최적의 처리량을 구현합니다.

작업 순서는 다음과 같습니다.

1. 다음 명령어를 실행하여 시스템의 물리 코어 개수를 확인합니다.
```
lscpu | grep "Core(s) per socket" | cut -d':' -f2 | xargs
```
2. 최적화 매개변수를 설정합니다. 다음 방식 중 한 가지를 선택할 수 있습니다.
 - 환경 실행 매개변수를 설정하고, GNU OpenMP* Libraries를 사용합니다. 환경 변수 파일에 다음 설정을 추가합니다.
```
export OMP_NUM_THREADS=physicalcores
export GOMP_CPU_AFFINITY="0-<physicalcores-1>"
export OMP_SCHEDULE=STATIC
export OMP_PROC_BIND=CLOSE
```
 - 환경 실행 매개변수를 설정하고, Intel OpenMP* Libraries를 사용합니다. 환경 변수 파일에 다음 설정을 추가합니다.
```
export OMP_NUM_THREADS=physicalcores
export LD_PRELOAD=<path_to_libiomp5.so>
export KMP_AFFINITY="granularity=fine,verbose,compact,1,0"
export KMP_BLOCKTIME=1
export KMP_SETTINGS=1
```


#### PyTorch* 딥러닝 모델의 추론 및 학습 최적화 실행에 대한 권장사항

- 모델 추론 실행 시 Intel<sup>®</sup> Extension for PyTorch를 사용해 성능을 높일 수 있습니다. 예시 코드는 다음과 같습니다.
```
import intel_pytorch_extension
...
net = net.to('xpu')       # Move model to IPEX format
data = data.to('xpu')     # Move data  to IPEX format
...
output = net(data)        # Perform inference with IPEX
output = output.to('cpu') # Move output back to ATen format
```
- 추론 및 학습 성능은 jemalloc을 사용하여 최적화할 수 있습니다. jemalloc은 범용 `malloc(3)`으로 구현되며, 시스템에 메모리 할당자 제공을 위해 파편화 방지 및 확장 가능한 동시 지원을 강조합니다. jemalloc은 표준 할당자 기능을 뛰어넘는 여러 가지 자가 점검, 메모리 관리 및 조절 기능을 제공합니다. 자세한 내용은 [jemalloc](https://github.com/jemalloc/jemalloc/wiki) 및 [예시 코드](https://github.com/mingfeima/op_bench-py/blob/master/run.sh)를 참고하십시오.
- 여러 socket의 분산형 학습에 대한 자세한 내용은 [PSSP-Transformer의 분산형 CPU 학습 스크립트](https://github.com/mingfeima/pssp/blob/master/pssp-transformer/dist_train_cpu.sh)를 참고하십시오.

#### 성능 결과

인텔의 Intel<sup>®</sup> Xeon<sup>®</sup> 2 시리즈 확장 가능 프로세서 Cascade Lake를 기반으로 한 2*CPU(28코어/CPU) 및 384G 메모리 시나리오에서 각 모델의 성능 테스트 데이터는 [성능 테스트 데이터](https://software.intel.com/content/www/us/en/develop/articles/intel-and-facebook-collaborate-to-boost-pytorch-cpu-performance.html)를 참고하십시오. 실제 모델 및 물리적 설정에 따라 성능 데이터에 차이가 있을 수 있으며, 본 문서에서 제공하는 테스트 데이터는 참고용입니다.

:::
::: 예시3:\sIntel<sup>®</sup>AI\s저정밀\s최적화\s툴을\s사용한\s가속


Intel<sup>®</sup> 저정밀 최적화 툴은 오픈 소스 Python 라이브러리이며, 간단하고 편리하며 신경망 프레임워크 간의 저정밀 양자화 추론 인터페이스를 제공합니다. 해당 인터페이스를 간편하게 호출하여 모델 양자화로 생산성을 높이고, 3 시리즈 Intel<sup>®</sup> Xeon<sup>®</sup> DL Boost 확장 가능 프로세서 플랫폼에서 저정밀 모델의 추론 성능을 가속화합니다. 사용 방법에 대한 자세한 내용은 [Intel<sup>®</sup> 저정밀 양자화 툴 코드 리포지토리](https://github.com/Intel/lpot/)를 참고하십시오.

#### 지원하는 신경망 프레임워크 버전
Intel<sup>®</sup> 저정밀 최적화 툴 지원:
Intel<sup>®</sup>에 최적화된 TensorFlow* `v1.15.0`, `v1.15.0up1`, `v1.15.0up2`, `v2.0.0`, `v2.1.0`, `v2.2.0`, `v2.3.0`, `v2.4.0`。
Intel<sup>®</sup>에 최적화된 PyTorch `v1.5.0+cpu`, `v1.6.0+cpu`
Intel<sup>®</sup>에 최적화된 MXNet `v1.6.0`, `v1.7.0` 및 ONNX-Runtime `v1.6.0`

#### 프레임워크 구현
Intel<sup>®</sup> 저정밀 최적화 툴을 사용한 프레임워크 구현 순서도는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/6062f647b40e2900354fbc73d8a4248a.jpg)

#### 워크플로
Intel<sup>®</sup> 저정밀 최적화 툴의 워크플로 순서도는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/acbc366d69819b443064ba5df58608fc.png)

#### 양자화 모델 성능 및 정밀도 예시

인텔의 Intel<sup>®</sup> Xeon<sup>®</sup> 2 시리즈 확장 가능 프로세서 Cascade Lake에서 일부 Intel<sup>®</sup> 저정밀 최적화 툴 양자화 모델의 성능 및 정밀도는 다음과 같습니다.

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
표에서 PyTorch와 Tensorflow는 모두 Intel에 최적화된 프레임워크 기반입니다. 지원되는 양자화 모델의 전체 리스트는 [온라인 문서](https://github.com/intel/lpot/blob/master/docs/full_model_list.md)를 참고하십시오.
</dx-alert>



#### Intel<sup>®</sup> 저정밀 최적화 툴 설치 및 사용 예시 

1. 순서에 따라 다음 명령어를 실행하고, anaconda를 사용해 lpot라는 이름의 python3.x 가상 환경을 구축합니다. 본 문서는 python 3.7을 예시로 합니다.
```plaintext
conda create -n lpot python=3.7
conda activate lpot
```
2. lpot를 설치합니다. 다음 두 가지 방식으로 설치할 수 있습니다.
    - 다음 명령어를 실행하여 바이너리 파일에서 설치합니다.
``` plaintext
pip install lpot
```
    - 다음 명령어를 실행하여 소스 코드에서 설치합니다.
```plaintext
 git clone https://github.com/intel/lpot.git
 cd lpot
 pip install –r requirements.txt
 python setup.py install
```
3. TensorFlow ResNet50 v1.0를 양자화합니다. 본 문서는 ResNet50 v1.0을 예시로 해당 툴을 사용해 양자화하는 방법을 소개합니다.
    1. 데이터 세트를 준비합니다.
다음 명령어를 실행하여 ImageNet validation 데이터 세트를 다운로드 및 압축 해제합니다.
```plaintext
mkdir –p img_raw/val && cd img_raw
wget http://www.image-net.org/challenges/LSVRC/2012/dd31405981
ef5f776aa17412e1f0c112/ILSVRC2012_img_val.tar
tar –xvf ILSVRC2012_img_val.tar -C val
```
다음 명령어를 실행하여 image 파일을 label 분류에 따른 서브 디렉터리로 이동합니다.
```plaintext
cd val
wget -qO -https://raw.githubusercontent.com/soumith/
imagenetloader.torch/master/valprep.sh | bash
```
다음 명령어를 실행하여 스크립트 prepare_dataset.sh 를 사용해 원시 데이터를 TFrecord 포맷으로 전환합니다.
```plaintext
cd examples/tensorflow/image_recognition
bash prepare_dataset.sh --output_dir=./data --raw_dir=/PATH/TO/img_raw/val/ 
--subset=validation
```
데이터 세트 관련 자세한 내용은 [Prepare Dataset](https://github.com/intel/lpot/tree/master/examples/tensorflow/image_recognition#2-prepare-dataset)를 참고하십시오.
    2. 다음 명령어를 실행해 모델을 준비합니다.
```plaintext
wget https://storage.googleapis.com/intel-optimized-tensorflow/
 models/v1_6/resnet50_fp32_pretrained_model.pb
```
    3. 다음 명령어를 실행하여 Tuning을 실행합니다.
`examples/tensorflow/image_recognition/resnet50_v1.yaml` 파일을 수정해 `quantization\calibration`, `evaluation\accuracy`, `evaluation\performance` 세 부분의 데이터 세트 경로를 사용자의 실제 로컬 경로로 지정합니다. 이는 데이터 세트 준비 단계에서 생성한 TFrecord 데이터가 있는 위치입니다. 자세한 내용은 [ResNet50 V1.0](https://github.com/intel/lpot/tree/master/examples/tensorflow/image_recognition#1-resnet50-v10)을 참고하십시오.
```plaintext
cd examples/tensorflow/image_recognition
bash run_tuning.sh --config=resnet50_v1.yaml \
--input_model=/PATH/TO/resnet50_fp32_pretrained_model.pb \
--output_model=./lpot_resnet50_v1.pb
```
    4. 다음 명령어를 실행하여 Benchmark를 실행합니다.
```plaintext
bash run_benchmark.sh --input_model=./lpot_resnet50_v1.pb
--config=resnet50_v1.yaml
```
출력 결과는 다음과 같습니다. 성능 데이터는 참고용입니다.
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
::: 예시4:\sIntel<sup>®</sup>\sDistribution\sof\sOpenVINO™\sToolkit\s를\s사용해\s추론\s가속
Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit는 컴퓨터의 시각화 및 기타 딥 러닝 애플리케이션 배포를 가속화할 수 있는 툴 패키지입니다. Intel 플랫폼의 다양한 가속기(CPU, GPU, FPGA, Movidius의 VPU 포함)를 통한 딥러닝 및 이종 하드웨어의 직접 실행을 지원합니다.

Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit는 TensorFlow\*, PyTorch\* 등을 통해 학습된 모델을 최적화할 수 있습니다. 모델 옵티마이저, 추론 엔진, Open Model Zoo, 학습 후 최적화 툴(Post-training Optimization Tool) 등 배포 툴 패키지를 포함합니다.

- **모델 옵티마이저(Model optimizer)**: Caffe\*, TensorFlow\*, PyTorch\*, Mxnet\* 등 다양한 프레임워크 학습 모델을 중간 표현(IR)으로 전환합니다.
- **추론 엔진(Inference Engine)**: 전환된 IR을 CPU, GPU, FPGA, VPU와 같은 하드웨어에서 실행하면 자동으로 하드웨어의 가속 패키지를 호출해 추론 성능을 가속화합니다.

[Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit 공식 홈페이지](https://software.intel.com/content/www/us/en/develop/tools/openvino-toolkit.html) 또는 [온라인 문서](https://docs.openvinotoolkit.org/latest/index.html)에서 자세한 정보를 확인할 수 있습니다.

#### 워크플로
Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit 툴 패키지 워크플로 순서도는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/98afcac361352773801fbe863d21b912.png)

#### Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit 추론 성능
The Intel® Distribution of OpenVINO™ 툴은 다양한 Intel 프로세서 및 가속 하드웨어에서 최적화 구현을 제공합니다. 이 툴은 Intel<sup>®</sup> Xeon<sup>®</sup> 확장 가능 프로세서 플랫폼에서 Intel<sup>®</sup> DL Boost 및 AVX-512 명령어 집합을 사용해 추론 네트워크 가속을 진행합니다. 

 #### Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit를 사용한 딥러닝 개발 패키지(DLDT)
 다음 자료를 참고하십시오.
- [Intel<sup>®</sup> 딥러닝 배포 툴 패키지 소개](https://docs.openvinotoolkit.org/downloads/cn/I03030-9-Introduction%20to%20Intel_%20Deep%20Learning%20Deployment%20Toolkit%20-%20OpenVINO_%20Toolkit.pdf)
-  [이미지 분류 C++ 예시(비동기화 모드)](https://docs.openvinotoolkit.org/downloads/cn/I03030-10-Image%20Classification%20Cpp%20Sample%20Async%20-%20OpenVINO_%20Toolkit.pdf)
-  [객체 검증 C++ 예시(SSD)](https://docs.openvinotoolkit.org/downloads/cn/I03030-11-Object%20Detection%20Cpp%20Sample%20SSD%20-%20OpenVINO_%20Toolkit.pdf)
-  [자동 음성인식 C++ 예시](https://docs.openvinotoolkit.org/downloads/cn/I03030-12-Automatic%20Speech%20Recognition%20Cpp%20%20Sample%20-%20OpenVINO_%20Toolkit.pdf)
-  [동작인식 Python* 예시](https://docs.openvinotoolkit.org/downloads/cn/I03030-13-Action%20Recognition%20Python%20Demo%20-%20OpenVINO_%20Toolkit.pdf)
-  [교차로 카메라 C++ 예시](https://docs.openvinotoolkit.org/downloads/cn/I03030-14-Crossroad%20Camera%20Cpp%20%20Demo%20-%20OpenVINO_%20Toolkit.pdf)
- [포즈 예측 C++ 예시](https://docs.openvinotoolkit.org/downloads/cn/I03030-15-Human%20Pose%20Estimation%20Cpp%20Demo%20-%20OpenVINO_%20Toolkit.pdf)

#### Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit 기본 테스트
자세한 내용은 [Linux* 지향 Intel<sup>®</sup> OpenVINO™ 툴 패키지 배포 버전 설치](https://docs.openvinotoolkit.org/downloads/cn/I03030-5-Install%20Intel_%20Distribution%20of%20OpenVINO_%20toolkit%20for%20Linux%20-%20OpenVINO_%20Toolkit.pdf)를 참고하십시오.

:::
</dx-accordion>

