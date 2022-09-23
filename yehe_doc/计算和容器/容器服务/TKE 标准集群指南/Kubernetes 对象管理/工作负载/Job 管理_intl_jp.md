## 概要

Jobコンソールは、実行が終了するまで実行ルールに従って実行されている1-NのPodを作成します。Jobは、BatchComputeやデータ分析などのシナリオで使用できます。繰り返し実行の回数、並列性およびリスタートポリシーを設定することにより、ビジネス要件を満たします。
Jobが実行された後、新しいPodの作成またはPodの削除は行いません。「ログ」では、完了したPodのログを確認できます。Jobが削除されると、Jobによって作成されたPodも削除され、Jobによって作成されたPodのログを表示できなくなります。

## Jobコンソールのアクションガイド

### Jobの作成

1. [Tencent Kubernetes Engineコンソール](https://console.cloud.tencent.com/tke2)にログインします。
2. 左側ナビゲーションバーでは、【 Cluster】をクリックして、クラスター管理ページへ進みます。
3. Jobの作成を必要とするクラスターIDをクリックして、Jobが作成されるクラスター管理ページへ進みます。
4. 「Workload」 > 「Job」を選択して、Job情報ページへ進みます。以下の通りです。
![Job](https://main.qcloudimg.com/raw/b33fcb5fe7f6491ef71b53f21ed82051.png)
5. 【Create】をクリックして、「 Create Workload」ページへ進みます。下図の通りです：
![Create a workload](https://main.qcloudimg.com/raw/e3e76bf1eeae83380d0f4b3f4e940934.png)
6. 実際のニーズに応じて、Jobパラメータを設定します。キーパラメータの情報は以下の通りです：
 - ワークロード名：カスタマイズします。
 - ネームスペース：実際のニーズに応じて選択します。
 - タイプ：「Job（シングルタスク）」を選択します。
 - Jobの設定：実際のニーズに応じて、JobのPodに1つ又は複数の異なるコンテナを設定します。
    - 繰り返し回数：Jobによって管理されるPodを繰り返し実行する必要がある回数を設定します。
    - 並列性：Jobを並列に実行するPodの数を設定します。
    - 失敗リスタートポリシー：Podではコンテナが異常終了した後のリスタートポリシーを設定します。
       - Neverオプション：Podではすべてのコンテナが終了するまで、コンテナがリスタートされません。
       - OnFailureオプション：Podが実行し続けて、コンテナがリスタートされます。
 - インスタンス内のコンテナ：実際のニーズに応じて、JobのPodに1つ又は複数の異なるコンテナを設定します。
    - 名称：カスタマイズします。
    - イメージ：実際のニーズに応じて選択します。
    - イメージバージョン：実際のニーズに応じて入力します。
    - CPU/メモリ制限：[Kubernetes リソース制限](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/)に基づいて、CPUおよびメモリの制限範囲を設定することができ、サービスのロバストを向上させます。
    - 詳細設定：「**作業ディレクトリ**」、「**実行コマンド**」、「**実行パラメータ**」、「**コンテナ健康診断**」、「**特権レベル**」などのパラメータを設定できます。
7. 【Create Workload】をクリックして、作成が完了します。

### Job状態の確認

1. [Tencent Kubernetes Engineコンソール](https://console.cloud.tencent.com/tke2)にログインします。
2. 左側ナビゲーションバーでは、【Cluster】をクリックして、クラスター管理ページへ進みます。
3. Job状態の確認を必要とするクラスターIDをクリックして、Job状態が確認されるクラスター管理ページへ進みます。
4. 「Workload」 > 「Job」を選択して、Job情報ページへ進みます。下図の通りです：
![Job](https://main.qcloudimg.com/raw/522504f451b3234997b7c413724bdb04.png)
5. 状態の確認を必要とするJob名称をクリックして、Jobの詳細を確認できます。

### Jobの削除

Jobが実行された後、新しいPodの作成またはPodの削除は行いません。「ログ」では、完了したPodのログを確認できます。Jobが削除されると、Jobによって作成されたPodも削除され、Jobによって作成されたPodのログを表示できなくなります。

## KubectlによるJobのアクションガイド

[](id:YAMLSample)
### YAMLの例

```Yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: pi
spec:
  completions: 2
  parallelism: 2
  template:
    spec:
      containers:
      - name: pi
        image: perl
        command: ["perl",  "-Mbignum=bpi", "-wle", "print bpi(2000)"]
      restartPolicy: Never
  backoffLimit: 4
```
- kind：Jobのリソースタイプを標識します。
- metadata：Jobの名称、Labelなどの基本情報です。
- metadata.annotations：Jobに関する追加説明であり、このパラメータを使用してTencent Cloud TKEの追加の拡張機能を設定できます。
- spec.completions：Jobによって管理されるPodを繰り返し実行する回数です。
- spec.parallelism：Jobを並列に実行するPodの数です。
- spec.template：Jobによって管理されるPodの詳細なテンプレート構成です。

### Jobの作成

1. [YAMLの例](#YAMLSample)を参照して、Job YAMLファイルを準備します。
2. Kubectlをインストールして、クラスターに接続されます。アクションの詳細については、[Kubectlによるクラスターへの接続](https://intl.cloud.tencent.com/document/product/457/30639)をご参照ください。
3. Job YAMLファイルを作成します。
```
kubectl create -f Job YAMLファイル名称
```
例えば、ファイル名がpi.yamlであるJob YAMLファイルを作成するには、次のコマンドを実行します。
```shell
kubectl create -f pi.yaml
```
4. 次のコマンドを実行して、作成が成功したかどうかを確認します。
```shell
kubectl get job
```
下記のような情報が返された場合は、作成が成功したことを示しています。
```
NAME      DESIRED   SUCCESSFUL   AGE
job       1         0            1m
```

### Jobの削除
次のコマンドを実行して、Jobを削除します。
```
kubectl delete job [NAME]
```



