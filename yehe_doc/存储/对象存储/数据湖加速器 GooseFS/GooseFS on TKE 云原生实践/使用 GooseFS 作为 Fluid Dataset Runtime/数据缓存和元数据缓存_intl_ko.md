## 작업 시나리오

이 문서에서는 데이터 캐싱 및 메타데이터 캐싱을 위한 매개변수를 선택하는 방법을 설명합니다.

## 작업 순서

### 데이터 캐싱 활성화/비활성화

GooseFSRuntime에서 데이터 캐시 활성화는 `goosefs.worker.ufs.instream.cache.enabled: "true"`이며, 이 속성의 기본값은 true입니다.

아래와 같이 Runtime에서 `goosefs.worker.ufs.instream.cache.enabled: "false"`를 지정하여 캐시를 비활성화할 수 있습니다.
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: GooseFSRuntime
metadata:
  name: hadoop
spec:
  replicas: 1
  tieredstore:
    levels:
      - mediumtype: SSD
        path: /mnt/disk1/
        quota: 290G
        high: "0.9"
        low: "0.8"
  properties:
    goosefs.worker.ufs.instream.cache.enabled: "false"
```

### 메타데이터 캐시 활성화

GooseFSRuntime에서 메타데이터를 통해 메타데이터 정보를 캐싱할 수 있습니다. 메타데이터 캐시 활성화 수량은 `goosefs.user.metadata.cache.enabled: "true"`로 지정할 수 있습니다. 이 속성의 기본값은 false입니다.

자세한 내용은 다음과 같습니다:
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: GooseFSRuntime
metadata:
  name: hadoop
spec:
  replicas: 1
  tieredstore:
    levels:
      - mediumtype: SSD
        path: /mnt/disk1/
        quota: 290G
        high: "0.9"
        low: "0.8"
  properties:
    oosefs.worker.ufs.instream.cache.enabled: "true"
    goosefs.user.metadata.cache.enabled: "true"
```

