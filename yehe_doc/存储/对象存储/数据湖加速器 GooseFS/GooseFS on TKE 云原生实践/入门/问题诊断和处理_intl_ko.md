## Fluid 설치 및 사용 관련 문제

### Helm을 사용한 fluid 설치 시 실패가 발생하는 이유는 무엇입니까?

[Fluid 설치 문서](https://intl.cloud.tencent.com/document/product/436/42230)에 따라 Fluid 컴포넌트가 정상적으로 작동하는지 확인할 것을 권장합니다.

Fluid 설치 문서는 'Helm 3'을 예로 들어 배포합니다. 'Helm 3' 이전 버전으로 Fluid를 배포하여 'CRD가 정상적으로 실행되지 않음' 상황이 발생하는 경우, 이는 'Helm 3' 및 그 이후 버전이 'helm install' 중에 자동으로 CRD를 설치했기 때문일 수 있습니다(이전 버전의 Helm은 해당 없음). 자세한 내용은 [Helm 공식 문서](https://helm.sh/docs/chart_best_practices/custom_resource_definitions/)를 참고하십시오.

이러한 경우 CRD를 수동 설치해야 합니다.

```bash
$ kubectl create -f fluid/crds
```

### Runtime을 삭제할 수 없는 이유는 무엇입니까?

관련 Pod 실행 상태 및 Runtime Events를 확인하십시오. 활성 Pod가 여전히 Fluid에서 생성한 Volume을 사용하는 한, Fluid는 삭제 작업을 완료하지 않습니다.

다음 명령어를 통해 이러한 활성 Pod를 빠르게 찾을 수 있습니다. 실사용 시 `<dataset_name>` 및 `<dataset_namespace>`를 실제 상황에 맞게 교체합니다.

```bash
kubectl describe pvc <dataset_name> -n <dataset_namespace> | \
	awk '/^Mounted/ {flag=1}; /^Events/ {flag=0}; flag' | \
	awk 'NR==1 {print $3}; NR!=1 {print $1}' | \
	xargs -I {} kubectl get po {} | \
	grep -E "Running|Terminating|Pending" | \
	cut -d " " -f 1
```


### Runtime이 생성한 PVC 마운트 작업 생성 시, `driver name fuse.csi.fluid.io not found in the list of registered CSI drivers` 오류가 발생하는 이유는 무엇입니까?

1. 작업이 스케줄링된 노드 소재 kubelet 구성이 기본값 `/var/lib/kubelet`인지 확인합니다.
2. Fluid의 CSI 컴포넌트가 정상인지 명령어를 통해 확인합니다.
다음 명령어를 통해 Pod를 빠르게 찾을 수 있습니다. 실사용 시 `<node_name>` 및 `<fluid_namespace>`를 실제 상황에 맞게 교체합니다.
```bash
kubectl get pod -n <fluid_namespace> | grep <node_name>

# <pod_name>은 이전 단계의 pod 이름입니다.
kubectl logs <pod_name> node-driver-registrar -n <fluid_namespace>
kubectl logs <pod_name> plugins -n <fluid_namespace>
```
 - 상기 단계의 Log에 오류가 없으면, csidriver 객체가 있는지 확인하십시오.
```
kubectl get csidriver
```
 - csidriver 객체가 존재하는 경우 csi 등록 노드에 `<node_name>`이 포함되어 있는지 확인하십시오.
```
kubectl get csinode | grep <node_name>
```

상기 명령에 대한 출력이 없으면, 작업이 스케줄링된 노드 소재 kubelet 구성이 기본값 `/var/lib/kubelet`인지 확인하십시오. Fluid의 CSI 컴포넌트는 고정된 주소의 socket을 통해 kubelet에 등록되기 때문에, 기본값은 `--csi-address=/var/lib/kubelet/csi-plugins/fuse.csi.fluid.io/csi.sock -- kubelet-registration-path=/var/lib/kubelet/csi-plugins/fuse.csi.fluid.io/csi.sock`입니다.


### fluid를 업데이트한 후, `kubectl get`을 사용하여 업데이트 전에 생성된 dataset을 쿼리할 때, 새로 생성된 dataset에 비해 일부 필드가 누락된 것으로 나타나는 이유는 무엇입니까?

fluid 업그레이드 프로세스 중에 CRD를 업데이트했을 수 있으므로 이전 버전에서 생성한 dataset는 CRD의 신규 추가된 필드를 공란으로 설정합니다. 예를 들어 v0.4 및 그 이전 버전에서 업그레이드했다면, 그 당시 dataset에는 FileNum 필드가 없었기 때문에, Fluid를 업데이트한 후 'kubectl get' 명령어를 사용하면 dataset 의 FileNum을 찾을 수 없게 됩니다.

dataset를 다시 구축할 수 있으며 새로 생성된 dataset는 이러한 필드를 정상적으로 표시합니다.


### 애플리케이션에서 PVC를 사용할 때 Volume Attachment 시간 초과 문제가 발생하는 이유는 무엇입니까?

Volume Attachment 시간 초과 문제는 Kubelet이 CSI Driver를 요청할 때 CSI Driver로부터 응답을 수신하지 못하여 발생하는 문제입니다. 이 문제는 Fluid의 CSI Driver가 설치되지 않았거나 kubelet에 CSI Driver에 대한 액세스 권한이 없기 때문에 발생합니다.

Kubelet은 CSI Driver를 콜백하므로, Fluid에 CSI Driver를 설치하지 않거나 Kubelet에 CSI Driver 조회 권한이 없으면, CSI Plugin이 올바르게 트리거되지 않습니다.

`kubectl get csidriver` 명령을 사용하여 CSI Driver가 설치되었는지 확인합니다.
- 설치되지 않은 경우 `kubectl apply -f chart/fluid/fluid/templates/csi/driver.yaml` 명령을 사용하여 설치한 다음 PVC가 애플리케이션에 성공적으로 마운트되는지 확인합니다.
- 그래도 해결되지 않으면 `export KUBECONFIG=/etc/kubernetes/kubelet.conf && kubectl get csidriver`를 사용하여 Kubelet이 CSI Driver 조회 권한을 가질 수 있는지 확인하십시오.




