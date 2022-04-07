## 概要

StatefulSetは主に、状態ありのアプリケーションを管理するために使用されます。作成されたPodには、仕様に従って作成された持続的な識別子があります。識別子は、Podの移行または破棄のリスタート後も保持されます。持続的なストレージを必要とするとき、識別子を使用してストレージボリュームを1対1でマッピングできます。アプリケーションが持続的な識別子を必要としない場合は、Deploymentを使用してアプリケーションをデプロイすることはお勧めします。

## StatefulSetコンソールのアクションガイド

<span id="createStatefulSet"></span>

### StatefulSetの作成

1. Tencent Kubernetes Engine（TKE）コンソールにログインして、左側ナビゲーションバーの【[ Clusters](https://console.cloud.tencent.com/tke2/cluster)】を選択してください。
2. StatefulSetの作成を必要とするクラスターIDをクリックして、StatefulSetが作成されるクラスター管理ページへ進みます。
3. 【Workload】>【StatefulSet】を選択して、StatefulSet管理ページへ進みます。下図の通りです：
![](https://main.qcloudimg.com/raw/88ece12d8464711824eadfb35db0c050.png)
4. 【Create 】をクリックして、「 Create Workload」ページへ進みます。
実際のニーズに応じて、StatefulSetパラメータを設定します。キーパラメータの情報は以下の通りです：
 - **ワークロード名**：カスタマイズされた名称を入力します。
 - **ネームスペース**：実際のニーズに応じて選択します。
 - **タイプ**：【StatefulSet（状態セット有りの実行Pod）】を選択します。
 - **インスタンス内のコンテナ**：実際のニーズに応じて、StatefulSetのPodに1つ又は複数の異なるコンテナを設定します。
    - **名称**：カスタマイズします。
    - **イメージ**：実際のニーズに応じて選択します。
    - **イメージバージョン（Tag）**：実際のニーズに応じて入力します。
    - **イメージプルポリシー**：次の3つのポリシーを提供し、ニーズに応じて選択してください。
       イメージプルポリシーが設定されていない場合は、イメージバージョンがnullまたは`latest`であるとき、Alwaysポリシーを使用し、そうでないとき、IfNotPresentポリシーを使用します。
        - **Always**：常にリモートからこのイメージをプルします。
        - **IfNotPresent**：デフォルトではローカルイメージを使用しますが、ローカルでこのイメージがない場合は、リモートからこのイメージをプルします。
        - **Never**：ローカルイメージのみを使用します。ローカルでこのイメージがない場合は、異常を報告します。
    - **CPU/メモリ制限**：[Kubernetes リソース制限](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/)に基づいて、CPUおよびメモリの制限範囲を設定することができ、サービスのロバストを向上させます。
    - **詳細設定**：「**作業ディレクトリ**」、「**実行コマンド**」、「**実行パラメータ**」、「**コンテナ健康診断**」および「**特権レベル**」などのパラメータを設定できます。
 - **インスタンスの数**：実際のニーズに応じて調整方法を選択し、インスタンスの数を設定します。
5. 【 Create a workload 】をクリックして、作成が完了します。

### StatefulSetの更新

#### YAMLの更新
1. TKEコンソールにログインして、左側ナビゲーションバーの【[Clusters](https://console.cloud.tencent.com/tke2/cluster)】を選択してください。
2. YAMLの更新を必要とするクラスターIDをクリックして、YAMLが更新されるクラスター管理ページへ進みます。
3. 【Workload】>【StatefulSet】を選択して、StatefulSet情報ページへ進みます。
4. YAMLの更新を必要とするStatefulSet行から、【More】>【Edit YAML 】を選択して、StatefulSet更新ページへ進みます。
5. 「Update StatefulSet」ページでYAMLを編集し、【 Finish】をクリックしてYAMLが更新されます。

#### Pod構成の更新
1. クラスター管理ページでは、Pod構成の更新を必要とするStatefulSetのクラスターIDをクリックして、Pod構成が更新されるStatefulSetのクラスター管理ページへ進みます。
2. Pod構成の更新を必要とするStatefulSet行では、【Update Pod Configurations.】をクリックします。
3. 「Update Pod Configurations.」ページでは、実際のニーズに応じて更新方法を変更し、パラメータを設定します。
4. 【 Finish】をクリックして、Pod構成が更新されます。

## KubectlによるStatefulSetのアクションガイド

<span id="YAMLSample"></span>

### YAMLの例

```Yaml
apiVersion: v1
kind: Service  ## ネットワークドメインをコントロールするためのHeadless Serviceを作成する
metadata:
  name: nginx
  namespace: default
  labels:
    app: nginx
spec:
  ports:
  - port: 80
    name: web
  clusterIP: None
  selector:
    app: nginx
---
apiVersion: apps/v1
kind: StatefulSet ### NginxのStatefulSetを作成する
metadata:
  name: web
  namespace: default
spec:
  selector:
    matchLabels:
      app: nginx
  serviceName: "nginx"
  replicas: 3 # by default is 1
  template:
    metadata:
      labels:
        app: nginx
    spec:
      terminationGracePeriodSeconds: 10
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
          name: web
        volumeMounts:
        - name: www
          mountPath: /usr/share/nginx/html
  volumeClaimTemplates:
  - metadata:
      name: www
    spec:
      accessModes: [ "ReadWriteOnce" ]
      storageClassName: "cbs"
      resources:
        requests:
          storage: 10Gi
```
- **kind**：StatefulSetのリソースタイプを標識します。
- **metadata**：StatefulSetの名称、Labelなどの基本情報です。
- **metadata.annotations**：StatefulSetに関する追加説明であり、このパラメータを使用してTencent Cloud TKEの追加の拡張機能を設定できます。
- **spec.template**：StatefulSetによって管理されるPodの詳細なテンプレート構成です。
- **spec.volumeClaimTemplates**：PVC&PVを作成するテンプレートを提供します。

パラメータの詳細については、[Kubernetes StatefulSet 公式ドキュメント](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)で確認できます。

### StatefulSetの作成

1. [YAMLの例](#YAMLSample)を参照して、StatefulSet YAMLファイルを準備します。
2. Kubectlをインストールして、クラスターに接続されます。アクションの詳細については、[Kubectlによるクラスターへの接続](https://intl.cloud.tencent.com/document/product/457/30639)をご参照ください。
3. 次のコマンドを実行して、StatefulSet YAMLファイルを作成します。
```shell
kubectl create -f StatefulSet YAMLファイル名称
```
例えば、ファイル名がweb.yamlであるStatefulSet YAMLファイルを作成するには、次のコマンドを実行します：
```shell
kubectl create -f web.yaml
```
4. 次のコマンドを実行して、作成が成功したかどうかを確認します。
```shell
kubectl get StatefulSet
```
下記のような情報が返された場合は、作成が成功したことを示しています。
```
NAME      DESIRED   CURRENT   AGE
test      1         1         10s
```

### StatefulSetの更新

次のコマンドを実行して、StatefulSetの更新ポリシータイプを確認します。
```
kubectl get ds/<daemonset-name> -o go-template='{{.spec.updateStrategy.type}}{{"\n"}}'
```
StatefulSetには、次の2つの更新ポリシータイプが含まれています：
- OnDelete：デフォルトの更新ポリシー。この更新ポリシーでStatefulSetを更新した後、新しいStatefulSet Podを作成する前に、古いStatefulSet Podを手動で削除する必要があります。
- RollingUpdate：Kubernetes 1.7以降のバージョンをサポートします。この更新ポリシーでStatefulSetテンプレートを更新した後、古いStatefulSet Podが終了し、ローリング更新方式で新しいStatefulSet Pod（Kubernetes 1.7以降のバージョン）を作成します。

#### 方法1

次のコマンドを実行して、StatefulSetを更新します。
```
kubectl edit StatefulSet/[name]
```
この方法は、単純なデバッグ確認に適しています。実稼働環境で直接使用することはお勧めしません。この方法を使用して、任意のStatefulSetパラメータを更新できます。

#### 方法2

次のコマンドを実行して、指定されたコンテナのイメージを更新します。
```
kubectl patch statefulset <NAME> --type='json' -p='[{"op": "replace", "path": "/spec/template/spec/containers/0/image", "value":"<newImage>"}]'
```
StatefulSetの他のパラメータを変更せず、ビジネスが更新されたときに、コンテナイメージのみを更新することはお勧めします。

更新されたStatefulSetがローリング更新ポリシーである場合は、次のコマンドを実行して更新状態を表示できます。
```
kubectl rollout status sts/<StatefulSet-name>
```

### StatefulSetの削除

次のコマンドを実行して、StatefulSetを削除します。
```
kubectl delete  StatefulSet [NAME] --cascade=false
```
--cascade=falseパラメータは、KubernetesがStatefulSetのみを削除し、Podを削除しないことを意味します。Podを削除するには、次のコマンドを実行します：
```
kubectl delete  StatefulSet [NAME]
```
StatefulSetに関するアクションの詳細については、[Kubernetes公式ガイド](https://kubernetes.io/docs/tutorials/stateful-application/basic-stateful-set/#scaling-a-statefulset)で確認できます。

