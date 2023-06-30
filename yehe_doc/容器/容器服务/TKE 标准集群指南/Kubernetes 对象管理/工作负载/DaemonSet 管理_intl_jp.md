## 概要

DaemonSetは主に、ノードログ収集などの常駐クラスターに存在するバックグラウンドプログラムをデプロイするために使用されます。DaemonSetは、指定されたPodがすべてまたは一部のノードで実行されていることを保証します。Podは、新しいノードがクラスターに追加されたときにも自動的にデプロイされます。Podは、ノードがクラスターから削除された後に自動的に回収されます。

## スケジューリングの説明

PodのnodeSelectorまたはaffinityパラメータが構成されている場合は、DaemonSetによって管理されるPodは、指定されたスケジューリングルールに従ってスケジューリングされます。PodのnodeSelectorまたはaffinityパラメータが構成されていない場合、Podはすべてのノードにデプロイされます。

## DaemonSetコンソールのアクションガイド

### DaemonSetの作成
1. Tencent Kubernetes Engine（TKE）コンソールにログインして、左側ナビゲーションバーの【[Cluster](https://console.cloud.tencent.com/tke2/cluster)】を選択してください。
2. DaemonSetの作成を必要とするクラスターIDをクリックして、DaemonSetが作成されるクラスター管理ページへ進みます。
3. 【Workload】>【DaemonSet】を選択して、DaemonSet情報ページへ進みます。以下の通りです：
![](https://main.qcloudimg.com/raw/ec694431e23d70a8f327fb7ef497480b.png)
4. 【 Create 】をクリックして、「 Create Workload」ページへ進みます。
実際のニーズに応じて、DaemonSetパラメータを設定します。キーパラメータの情報は以下の通りです。
 - **ワークロード名**：カスタマイズされた名称を入力します。
 - **ネームスペース**：実際のニーズに応じて選択します。
 - **タイプ**：【DaemonSet（各ホストでPodを実行する）】を選択します。
 - **インスタンス内のコンテナ**：実際のニーズに応じて、DaemonSetのPodに1つ又は複数の異なるコンテナを設定します。
    - **名称**：カスタマイズします。
    - **イメージ**：実際のニーズに応じて選択します。
    - **イメージバージョン（Tag）**：実際のニーズに応じて入力します。
    - **イメージプルポリシー**：次の3つのポリシーを提供し、ニーズに応じて選択してください。
      イメージプルポリシーが設定されていない場合は、イメージバージョンがnullまたは`latest`であるとき、Alwaysポリシーを使用し、そうでないとき、IfNotPresentポリシーを使用します。
       - **Always**：常にリモートからこのイメージをプルします。
       - **IfNotPresent**：デフォルトではローカルイメージを使用しますが、ローカルでこのイメージがない場合は、リモートからこのイメージをプルします。
       - **Never**：ローカルイメージのみを使用します。ローカルでこのイメージがない場合は、異常を報告します。
    - **CPU/メモリ制限**：[Kubernetes リソース制限](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/)に基づいて、CPUおよびメモリの制限範囲を設定することができ、サービスのロバストを向上させます。
    - 詳細設定：「**作業ディレクトリ**」、「**実行コマンド**」、「**実行パラメータ**」、「**コンテナ健康診断**」、「**特権レベル**」などのパラメータを設定できます。
5. 【Create a workload】をクリックして、作成が完了します。

### DaemonSetの更新

#### YAMLの更新
1. TKEコンソールにログインして、左側ナビゲーションバーの【[Cluster](https://console.cloud.tencent.com/tke2/cluster)】を選択してください。
2. YAMLの更新を必要とするクラスターIDをクリックして、YAMLが更新されるクラスター管理ページへ進みます。
3. 【Workload】>【DaemonSet】を選択して、DaemonSet情報ページへ進みます。
5. YAMLの更新を必要とするDaemonSet行から、【More 】>【Edit YAML】を選択して、DaemonSet更新ページへ進みます。
6. 「Update a DaemonSet」ページでYAMLを編集し、【 Finish】をクリックしてYAMLが更新されます。

#### Pod構成の更新
> DaemonSetローリング更新機能は、Kubernetes 1.6以降のバージョンでのみサポートされます。
>
1. クラスター管理ページでは、Pod構成の更新を必要とするDaemonSetのクラスターIDをクリックして、Pod構成が更新されるDaemonSetのクラスター管理ページへ進みます。
2. Pod構成の更新を必要とするDaemonSet行では、【 Update Pod Configurations】をクリックします。
3. 「 Update Pod Configurations」ページでは、実際のニーズに応じて更新方法を変更し、パラメータを設定します。
4. 【Finish 】をクリックして、Pod構成が更新されます。

## KubectlによるDaemonSetのアクションガイド


### YAMLの例<span id="YAMLSample"></span>
```Yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: fluentd-elasticsearch
  namespace: kube-system
  labels:
    k8s-app: fluentd-logging
spec:
  selector:
    matchLabels:
      name: fluentd-elasticsearch
  template:
    metadata:
      labels:
        name: fluentd-elasticsearch
    spec:
      tolerations:
      - key: node-role.kubernetes.io/master
        effect: NoSchedule
      containers:
      - name: fluentd-elasticsearch
        image: k8s.gcr.io/fluentd-elasticsearch:1.20
        resources:
          limits:
            memory: 200Mi
          requests:
            cpu: 100m
            memory: 200Mi
        volumeMounts:
        - name: varlog
          mountPath: /var/log
        - name: varlibdockercontainers
          mountPath: /var/lib/docker/containers
          readOnly: true
      terminationGracePeriodSeconds: 30
      volumes:
      - name: varlog
        hostPath:
          path: /var/log
      - name: varlibdockercontainers
        hostPath:
          path: /var/lib/docker/containers
```
>上記のYAMLの例は`https://kubernetes.io/docs/concepts/workloads/controllers/daemonset`から引用されています。作成中にコンテナイメージのプルが失敗する場合があります。このドキュメントでDaemonSetの構成を紹介するためにのみ使用されます。

- **kind**：DaemonSetリソースタイプを標識します。
- **metadata**：DaemonSetの名称、Labelなどの基本情報です。
- **metadata.annotations**：DaemonSetに関する追加説明であり、このパラメータを使用してTencent Cloud TKEの追加の拡張機能を設定できます。
- **spec.template**：DaemonSetによって管理されるPodの詳細なテンプレート構成です。

詳細については、[Kubernetes DaemonSet 公式ドキュメント](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)で確認できます。

### KubectlによるDaemonSetの作成

1. [YAMLの例](#YAMLSample)を参照して、StatefulSet YAMLファイルを準備します。
2. Kubectlをインストールして、クラスターに接続されます。アクションの詳細については、[Kubectlによるクラスターへの接続](https://intl.cloud.tencent.com/document/product/457/30639)をご参照ください。
3. 次のコマンドを実行して、DaemonSet YAMLファイルを作成します。
```shell
kubectl create -f DaemonSet YAMLファイル名称
```
例えば、ファイル名がfluentd-elasticsearch.yamlであるStatefulSet YAMLファイルを作成するには、次のコマンドを実行します：
```shell
kubectl create -f fluentd-elasticsearch.yaml
```
4. 次のコマンドを実行して、作成が成功したかどうかを確認します。
```shell
kubectl get DaemonSet
```
下記のような情報が返された場合は、作成が成功したことを示しています。
```
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE SELECTOR       AGE
frontend   0         0         0         0            0           app=frontend-node   16d
```

### KubectlによるDaemonSetの更新

次のコマンドを実行して、DaemonSetの更新ポリシータイプを確認します。
```
kubectl get ds/<daemonset-name> -o go-template='{{.spec.updateStrategy.type}}{{"\n"}}'
```
DaemonSetには、次の2つの更新ポリシータイプが含まれています：
- OnDelete：デフォルトの更新ポリシー。この更新ポリシーでDaemonSetを更新した後、新しいDaemonSet Podを作成する前に、古いDaemonSet Podを手動で削除する必要があります。
- RollingUpdate：Kubernetes 1.6以降のバージョンをサポートします。この更新ポリシーでDaemonSetテンプレートを更新した後、古いDaemonSet Podが終了し、ローリング更新方式で新しいDaemonSet Podを作成します。

#### 方法1

次のコマンドを実行して、DaemonSetを更新します。
```
kubectl edit DaemonSet/[name]
```
この方法は、単純なデバッグ確認に適しています。実稼働環境で直接使用することはお勧めしません。この方法を使用して、任意のDaemonSetパラメータを更新できます。

#### 方法2

次のコマンドを実行して、指定されたコンテナのイメージを更新します。
```
kubectl set image ds/[daemonset-name][container-name]=[container-new-image]
```
DaemonSetの他のパラメータを変更せず、ビジネスが更新されたときに、コンテナイメージのみを更新することはお勧めします。

### KubectlによるDaemonSetのロールバック

1. 次のコマンドを実行して、DaemonSetの更新履歴を確認します。
```
kubectl rollout history daemonset /[name]
```
2. 次のコマンドを実行して、指定されたバージョンの詳細を確認します。
```
kubectl rollout history daemonset /[name] --revision=[REVISION]
```
3. 次のコマンドを実行して、前のバージョンへロールバックします。
```
kubectl rollout undo daemonset /[name]
```
ロールバックバージョン番号を指定するには、次のコマンドを実行できます。
```
kubectl rollout undo daemonset /[name] --to-revision=[REVISION]
```

### KubectlによるDaemonSetの削除
次のコマンドを実行して、DaemonSetを削除します。
```
kubectl delete  DaemonSet [NAME]
```
