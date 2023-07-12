애플리케이션의 데이터 액세스 성능을 보장하기 위해, **데이터 사전 로딩**을 통해 원격 스토리지 시스템의 데이터를 컴퓨팅 노드에 가까운 분산 캐시 엔진으로 미리 풀링할 수 있습니다. 이 데이터 세트를 소모하는 애플리케이션이 처음 실행될 때 캐시가 가져오는 가속 효과를 누릴 수 있습니다.

이를 위해, 간단한 구성을 통해 전체 데이터 사전 로딩 프로세스를 완료하고, 데이터 사전 로딩의 다양한 동작에 대해 맞춤형 제어를 진행할 수 있는 DataLoad CRD를 제공합니다.

본문은 다음 두 가지 예시를 통해 DataLoad CRD의 사용법을 설명합니다.

- DataLoad 빠른 사용
- DataLoad 고급 설정


## 전제 조건

[Fluid](https://github.com/fluid-cloudnative/fluid)(version >= 0.6.0)가 설치되어 있어야 합니다.

>? [설치](https://intl.cloud.tencent.com/document/product/436/42230) 문서를 참고하여 Fluid를 설치하십시오.
>

## 작업 환경 생성

```yaml
$ mkdir <any-path>/warmup
$ cd <any-path>/warmup
```

## DataLoad 빠른 사용

**생성 대기 중인 Dataset와 Runtime 객체 구성**
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: Dataset
metadata:
  name: spark
spec:
  mounts:
    - mountPoint: https://mirrors.bit.edu.cn/apache/spark/
      name: spark 
---
apiVersion: data.fluid.io/v1alpha1
kind: GooseFSRuntime
metadata:
  name: spark
spec:
  replicas: 2
  tieredstore:
    levels:
      - mediumtype: SSD
        path: /mnt/disk1/
        quota: 2G
        high: "0.8"
        low: "0.7"
```

>? 사용자의 테스트 편의를 위해, 본 예시 중 mountPoint는 Web UFS를, UFS는 COS를 사용합니다. [GooseFS를 통한 COS(COSN) 마운트](https://intl.cloud.tencent.com/document/product/436/41024)를 참고하시기 바랍니다.
>

kind가 `Dataset`인 리소스 객체(Resource object)를 생성합니다. 'Dataset'는 Fluid에서 정의한 CRD(Custom Resource Definition)로, Fluid에게 필요한 데이터를 찾을 위치를 알려주는 데 사용됩니다. Fluid는 CRD 객체에 정의된 'mountPoint' 속성을 GooseFS에 마운트합니다.

본 예시는 간편성을 위해 COS를 사용하여 설명합니다.

**Dataset 및 Runtime 객체 생성**

```shell
$ kubectl create -f dataset.yaml
```

**Dataset와 Runtime이 준비 완료될 때까지 대기**

```shell
$ kubectl get datasets spark
```

다음과 유사한 결과가 표시되면 Dataset 와 Runtime이 모두 준비된 것입니다.

```shell
NAME    UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
spark   1.92GiB          0.00B    4.00GiB          0.0%                Bound   4m4s
```

**생성 대기 중인 DataLoad 객체 설정**
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: DataLoad
metadata:
  name: spark-dataload
spec:
  loadMetadata: true
  dataset:
    name: spark
    namespace: default
```

'spec.dataset'은 사전 로딩해야 하는 타깃 데이터 세트를 지정합니다. 이 예시에서 데이터 사전 로딩 타깃은 'default' 네임스페이스 하위의 'spark'라는 이름의 데이터 세트입니다. 이 구성이 귀하의 실제 환경과 부합하지 않는 경우, 실제 환경에 따라 조정하시기 바랍니다.

**기본적으로 상기 DataLoad 구성은 전체 데이터 세트의 모든 데이터를 로딩하려고 시도합니다.** 더 세분화된 제어를 원하는 경우(예: 데이터 세트 하위 지정 경로의 데이터만 로딩), [DataLoad 고급 구성](https://github.com/fluid-cloudnative/fluid/blob/master/docs/en/dev/api_doc.md)을 참고하십시오.

**DataLoad 객체 생성**

```shell
$ kubectl create -f dataload.yaml
```

**생성된 DataLoad 객체 상태 조회**

```shell
$ kubectl get dataload spark-dataload
```

상기 명령은 다음과 유사한 결과를 얻게 됩니다.

```shell
NAME             DATASET   PHASE     AGE
spark-dataload   spark     Loading   2m13s
```

`kubectl describe`를 통해 이 DataLoad에 대한 자세한 정보를 얻을 수 있습니다.

```shell
$ kubectl describe dataload spark-dataload
```

다음 결과를 얻게됩니다:
```
Name:         spark-dataload
Namespace:    default
Labels:       <none>
Annotations:  <none>
API Version:  data.fluid.io/v1alpha1
Kind:         DataLoad
...
Spec:
  Dataset:
    Name:       spark
    Namespace:  default
Status:
  Conditions:
  Phase:  Loading
Events:
  Type    Reason              Age   From      Message
  ----    ------              ----  ----      -------
  Normal  DataLoadJobStarted  80s   DataLoad  The DataLoad job spark-dataload-loader-job started
```

상기 데이터 로딩 과정은 네트워크 환경에 따라 몇 분이 소요될 수 있습니다.

**데이터 로딩 과정이 완료될 때까지 대기**

```shell
$ kubectl get dataload spark-dataload
```

DataLoad의 'Phase' 상태가 'Loading'에서 'Complete'로 변경된 것을 볼 수 있습니다. 이는 전체 데이터 로딩 프로세스가 완료되었음을 나타냅니다.

```shell
NAME             DATASET   PHASE      AGE
$ spark-dataload   spark     Complete   5m17s
```

이제 Dataset 객체의 캐시 상태를 다시 확인합니다.

```shell
$ kubectl get dataset spark
```

원격 스토리지 시스템의 모든 데이터가 분산 캐시 엔진에 성공적으로 캐시되었음을 확인할 수 있습니다.

```shell
NAME    UFS TOTAL SIZE   CACHED    CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
spark   1.92GiB          1.92GiB   4.00GiB          100.0%              Bound   7m41s
```

**환경 정리**

```shell
$ kubectl delete -f .
```

## DataLoad 고급 구성

상기 예시에 표시된 데이터 사전 로딩 기능 외에도, 몇 가지 간단한 구성을 통해 데이터 사전 로딩을 보다 세부적으로 조정할 수 있습니다. 이러한 조정에는 다음이 포함됩니다.

- 로딩할 하나 이상의 데이터 세트 하위 디렉터리 지정
- 데이터가 로딩될 때의 복사본 캐시 수량 설정
- 데이터 로딩 전, 메타데이터 동기화를 먼저 수행

### 로딩할 하나 이상의 데이터 세트 하위 디렉터리 지정

데이터를 로딩할 때 전체 데이터 세트 대신 지정된 하위 디렉터리(또는 파일)를 로딩할 수 있습니다. 이에 대한 예는 다음과 같습니다.
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: DataLoad
metadata:
  name: spark-dataload
spec:
  dataset:
    name: spark
    namespace: default
  loadMetadata: true
  target:
    - path: /spark/spark-2.4.8
    - path: /spark/spark-3.0.1/pyspark-3.0.1.tar.gz
```

상기 DataLoad는 `/spark/spark-2.4.8` 디렉터리의 전체 파일 및 `/spark/spark-3.0.1/pyspark-3.0.1.tar.gz` 파일만 로딩합니다.

`spec.target.path`의 값은 `mountpoint`의 마운트 포인트 하위의 상대 경로입니다. 예를 들어 현재 마운트 포인트가 `cos://test/`이며, 다음 파일은 기존 경로에 있습니다.

```shell
cos://test/user/sample.txt
cos://test/data/fluid.tgz
```

`target.path`를 다음과 같이 정의할 수 있습니다.
```yaml
target:
  - path: /user
  - path: /data
```

### 데이터가 로딩될 때의 복사본 캐시 수량 설정

데이터를 로딩할 때 구성을 통해 로딩된 데이터 복사본 수량을 제어할 수 있습니다. 이에 대한 예는 다음과 같습니다.
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: DataLoad
metadata:
  name: spark-dataload
spec:
  dataset:
    name: spark
    namespace: default
  loadMetadata: true
  target:
    - path: /spark/spark-2.4.8
      replicas: 1
    - path: /spark/spark-3.0.1/pyspark-3.0.1.tar.gz
      replicas: 2
```

상기 DataLoad가 데이터 로딩을 진행할 때, `/spark/spark-2.4.8` 디렉터리에 있는 파일의 경우 분산 캐시 엔진에 **1개**의 데이터 캐시 복사본이 유지되는 반면, `/spark/spark-3.0.1/pyspark-3.0.1.tar.gz` 파일의 경우, **2개**의 캐시 복사본이 유지됩니다.

### 데이터 로딩 전, 메타데이터 동기화를 먼저 수행(권장)

많은 시나리오 중, 기본 스토리지 시스템의 파일은 변동 발생 가능성이 있습니다. 분산 캐시 엔진의 경우, 기본 스토리지 시스템의 변경 사항을 인식하기 위해, 파일 메타 정보를 다시 동기화해야 합니다. 따라서 데이터를 로딩하기 전에 DataLoad 객체의 `spec.loadMetadata`를 설정하여 메타데이터 동기화를 미리 완료할 수 있습니다. 예를 들면 다음과 같습니다.
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: DataLoad
metadata:
  name: spark-dataload
spec:
  dataset:
    name: spark
    namespace: default
  loadMetadata: true
  target:
    - path: /
      replicas: 1
```
