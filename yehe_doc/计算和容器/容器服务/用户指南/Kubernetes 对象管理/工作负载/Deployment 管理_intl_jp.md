## 概要

Deploymentは、Podのテンプレートを宣言し、Podの実行ポリシーを制御します。状態無しのアプリケーションのデプロイに適しています。サービスニーズに応じて、Deploymentで実行されているPodのレプリカの数、スケジューリングポリシー、更新ポリシーなどを宣言できます。

## Deploymentコンソールのアクションガイド

<span id="creatDeployment"></span>
### Deploymentの作成
1. Tencent Kubernetes Engine（TKE）コンソールにログインして、左側ナビゲーションバーの【[Clusters ](https://console.cloud.tencent.com/tke2/cluster)】を選択してください。
2. Deploymentの作成を必要とするクラスターIDをクリックして、Deploymentが作成されるクラスター管理ページへ進みます。

3. 【 Create 】をクリックして、「Create a workload」ページへ進みます。
実際のニーズに応じて、Deploymentパラメータを設定します。キーパラメータの情報は以下の通りです：
 - **ワークロード名**：カスタマイズされた名称を入力します。
 - **ネームスペース**：実際のニーズに応じて選択します。
 - **タイプ**：【Deployment（Podを拡張可能にデプロイする）】を選択します。
 - **インスタンス内のコンテナ**：実際のニーズに応じて、DeploymentのPodに1つ又は複数の異なるコンテナを設定します。
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
4. 【 Create Workload 】をクリックして、作成が完了します。下図の通りです：
実行数=目的数の場合、DeploymentでのすべてのPodが作成されたことを意味します。
![](https://main.qcloudimg.com/raw/c458fdbc8d9770d8704327a9dbd16f55.png)

### Deploymentの更新

#### YAMLの更新
1. TKEコンソールにログインして、左側ナビゲーションバーの【[Clusters](https://console.cloud.tencent.com/tke2/cluster)】を選択してください。
2. Deploymentの更新を必要とするクラスターIDをクリックして、Deploymentが更新されるクラスター管理ページへ進みます。下図の通りです：
![](https://main.qcloudimg.com/raw/7e7acba7f2d84a9a0626458efb357ff0.png)
3. YAMLの更新を必要とするDeployment行では、【 More】>【Edit YAML】をクリックして、Deployment更新ページへ進みます。
5. 「Update Deployment」ページでYAMLを編集し、【 Finish 】をクリックしてYAMLが更新されます。下図の通りです：
![YAMLの更新](https://main.qcloudimg.com/raw/93c576f09ad8817abb794385f68b38ad.png)

#### Pod構成の更新

1. クラスター管理ページでは、Pod構成の更新を必要とするDeploymentのクラスターIDをクリックして、Pod構成が更新されるDeploymentのクラスター管理ページへ進みます。
2. Pod構成の更新を必要とするDeployment行では、【Updating Pod configurations】をクリックします。
3. 「Updating Pod configurations」ページでは、実際のニーズに応じて更新方法を変更し、パラメータを設定します。
4. 【Finish 】をクリックして、Pod構成が更新されます。

### Deploymentのロールバック
1. TKEコンソールにログインして、左側ナビゲーションバーの【[Clusters](https://console.cloud.tencent.com/tke2/cluster)】を選択してください。
2. Deploymentのロールバックを必要とするクラスターIDをクリックして、Deploymentがロールバックされるクラスター管理ページへ進みます。
4. ロールバックを必要とするDeploymentの名称をクリックして、Deployment情報ページへ進みます。
4. 【 Modification History】タブを選択して、ロールバックを必要とするバージョンでは、【 Rollback 】をクリックします。
6. ポップアップ表示された「Roll back a resource」プロンプトでは、【Submit 】をクリックしてロールバックが完了します。

### Pod数の調整
1. TKEコンソールにログインして、左側ナビゲーションバーの【[Clusters ](https://console.cloud.tencent.com/tke2/cluster)】を選択してください。
2. Pod数の調整を必要とするDeploymentのクラスターIDをクリックして、Pod数が調整されるDeploymentのクラスター管理ページへ進みます。

3. Pod数の調整を必要とするDeployment行では、【 Update Pod quantity 】をクリックして、Pod数の更新ページへ進みます。
4. 実際のニーズに応じてPod数を調整し、【Update Pod quantity 】をクリックして調整が完了します。

## KubectlによるDeploymentのアクションガイド

### YAMLの例<span id="YAMLSample"></span>
```Yaml
apiVersion: apps/v1beta2
kind: Deployment
metadata:
  name: nginx-deployment
  namespace: default
  labels:
    app: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx-deployment
  template:
    metadata:
      labels:
        app: nginx-deployment
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
```
- **kind**：Deploymentリソースタイプを標識します。
- **metadata**：Deploymentの名称、Namespace、Labelなどの基本情報です。
- **metadata.annotations**：Deploymentに関する追加説明であり、このパラメータを使用してTencent Cloud TKEの追加の拡張機能を設定できます。
- **spec.replicas**：Deploymentによって管理されるPod数です。
- **spec.selector**：Deployment管理Seletorによって選択されたPodのLabelです。
- **spec.template**：Deploymentによって管理されるPodの詳細なテンプレート構成です。

パラメータの詳細については、[Kubernetes Deployment 公式ドキュメント](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)で確認できます。

### KubectlによるDeploymentの作成

1. [YAMLの例](#YAMLSample)を参照して、Deployment YAMLファイルを準備します。
2. Kubectlをインストールして、クラスターに接続します。アクションの詳細については、[Kubectlによるクラスターへの接続](https://intl.cloud.tencent.com/document/product/457/30639)をご参照ください。
3. 次のコマンドを実行して、Deployment YAMLファイルを作成します。
```shell
kubectl create -f Deployment YAMLファイル名称
```
例えば、ファイル名がnginx.YamlであるDeployment YAMLファイルを作成するには、次のコマンドを実行します：
```shell
kubectl create -f nginx.yaml
```
4. 次のコマンドを実行して、作成が成功したかどうかを確認します。
```shell
kubectl get deployments
```
下記のような情報が返された場合は、作成が成功したことを示しています。
```
NAME             DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
first-workload   1         1         1            0           6h
ng               1         1         1            1           42m
```

### KubectlによるDeploymentの更新

KubectlによるDeploymentの更新には次の3つの方法が含まれています。その中で、[方法1](#Method1)および[方法2](#Method2)の両方とも、**Recreate**および**RollingUpdate**の2つの更新ポリシーをサポートします。
- Recreate更新ポリシーは、最初にすべてのPodを廃棄してから、Deploymentを再作成することです。
- RollingUpdate更新ポリシーは、DeploymentのPodを1つずつ更新するローリング更新ポリシーです。RollingUpdateは、一時停止、更新時間間隔の設定などもサポートします。

<span id="Method1"></span>
#### 方法1

次のコマンドを実行して、Deploymentを更新します。
```
kubectl edit  deployment/[name]
```
この方法は、単純なデバッグ確認に適しています。実稼働環境で直接使用することはお勧めしません。この方法を使用して、任意のDeploymentパラメータを更新できます。

<span id="Method2"></span>
#### 方法2

次のコマンドを実行して、指定されたコンテナのイメージを更新します。
```
kubectl set image deployment/[name] [containerName]=[image:tag]
```
Deploymentの他のパラメータを変更せず、ビジネスが更新されたときに、コンテナイメージのみを更新することはお勧めします。

<span id="Method3"></span>
#### 方法3

次のコマンドを実行して、指定されたリソースをローリング更新します。
```
kubectl rolling-update [NAME] -f FILE
```

### KubectlによるDeploymentのロールバック

1. 次のコマンドを実行して、Deploymentの更新履歴を確認します。
```
kubectl rollout history deployment/[name]
```
2. 次のコマンドを実行して、指定されたバージョンの詳細を確認します。
```
kubectl rollout history deployment/[name] --revision=[REVISION]
```
3. 次のコマンドを実行して、前のバージョンへロールバックします。
```
kubectl rollout undo deployment/[name]
```
ロールバックバージョン番号を指定するには、次のコマンドを実行します。
```
kubectl rollout undo deployment/[name] --to-revision=[REVISION]
```

### KubectlによるPod数の調整

#### Pod数の手動更新

次のコマンドを実行して、Pod数を手動で更新します。
```
kubectl scale deployment [NAME] --replicas=[NUMBER]
```

#### Pod数の自動更新

**前提条件**

クラスターのHPA機能をオンにします。TKEによって作成されたクラスターでは、デフォルトでHPA機能がオンになっています。

**操作手順**

次のコマンドを実行して、Deploymentの自動スケールアウトと自動スケールインを設定します。
```
kubectl autoscale deployment [NAME] --min=10 --max=15 --cpu-percent=80
```

### KubectlによるDeploymentの削除

次のコマンドを実行して、Deploymentを削除します。
```
kubectl delete deployment [NAME]
```
