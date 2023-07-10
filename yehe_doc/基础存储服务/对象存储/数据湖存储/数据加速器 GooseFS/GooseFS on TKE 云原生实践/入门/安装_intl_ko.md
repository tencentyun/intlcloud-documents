## 설치 및 사용 프로세스

### 1. 네임스페이스 생성

```shell
$ kubectl create ns fluid-system
```


### 2. fluid 다운로드

Fluid 공식 웹사이트 [Fluid Releases](https://github.com/fluid-cloudnative/fluid/releases)에서 Fluid 0.6.0 이상 버전을 다운로드할 수 있습니다. 기본적으로 최신 버전을 권장합니다.


### 3. Helm을 사용한 Fluid 설치

```shell
$ helm install --set runtime.goosefs.enabled=true fluid fluid-0.8.0.tgz
```

### 4. Fluid의 실행 상태 확인

```shell
$ kubectl get pod -n fluid-system
NAME                                         READY   STATUS    RESTARTS   AGE
csi-nodeplugin-fluid-2mfcr                   2/2     Running   0          108s
csi-nodeplugin-fluid-l7lv6                   2/2     Running   0          108s
dataset-controller-5465c4bbf9-5ds5p          1/1     Running   0          108s
goosefsruntime-controller-654fb74447-cldsv     1/1     Running   0          108s
```

이 중, csi-nodeplugin-fluid-xx의 수량은 k8s 클러스터의 노드 수량과 같아야 합니다.

이제 Fluid는 성공적으로 설치되었습니다. 이미지를 사용자 정의하고, 시스템 crd를 업그레이드하려면 다음 설명(선택 사항)을 참고하십시오.

### 5. 사용자 정의 이미지

`fluid-0.8.0.tgz`를 압축 해제하고 기본 `values.yaml` 파일을 수정합니다.
```yaml
runtime:
  mountRoot: /runtime-mnt
  goosefs:
    runtimeWorkers: 3
    portRange: 26000-32000
    enabled: false
    init:
      image: fluidcloudnative/init-users:v0.8.0-116a5be
    controller:
      image: fluidcloudnative/goosefsruntime-controller:v0.8.0-116a5be
    runtime:
      image: ccr.ccs.tencentyun.com/qcloud/goosefs:v1.2.0
    fuse:
      image: ccr.ccs.tencentyun.com/qcloud/goosefs:v1.2.0
```

`goosefs` 관련 기본 `image` 콘텐츠를 수정할 수 있습니다(예: 자신의 `repo`에 놓기 등). 수정이 완료되면 `helm package fluid`를 재사용하여 패키징하고, 다음 명령어를 사용하여 `fluid` 버전을 업데이트합니다.
```shell
helm upgrade --install fluid fluid-0.8.0.tgz
```

### 6. crd 업데이트

```shell
$ kubectl get crd      
NAME                                             CREATED AT
databackups.data.fluid.io                        2021-03-02T13:12:31Z
dataloads.data.fluid.io                          2021-04-14T11:14:58Z
datasets.data.fluid.io                           2021-03-02T13:12:31Z
goosefsruntimes.data.fluid.io                    2021-04-13T13:31:38Z
```

예를 들어, 시스템에 있는 기존 'goosefsruntime'의 crd를 업데이트합니다.

먼저 기존 crd를 삭제합니다.

```shell
kubectl delete crd goosefsruntimes.data.fluid.io
```

그 다음 `fluid-0.8.0.tgz`를 압축 해제합니다.

```shell
$ ls -l fluid/
total 32
total 32
-rw-r--r--  1 xieydd  staff   489  5 15 16:14 CHANGELOG.md
-rw-r--r--  1 xieydd  staff  1061  7 22 00:08 Chart.yaml
-rw-r--r--  1 xieydd  staff  2560  5 15 16:14 VERSION
drwxr-xr-x  8 xieydd  staff   256  7 20 15:06 crds
drwxr-xr-x  7 xieydd  staff   224  5 24 14:18 templates
-rw-r--r--  1 xieydd  staff  1665  7 22 00:08 values.yaml
```

마지막으로 새 crd를 만듭니다.

```shell
kubectl apply -f crds/data.fluid.io_goosefsruntimes.yaml
```
