## 概要

CronJobオブジェクトは、crontab（cron table）ファイルの行に類似します。指定されたスケジュールに従って定期的にJobを実行して、フォーマットはCronをご参照ください。
Cronのフォーマットは次のように説明されます。
```
# ファイルフォーマットの説明
#  ——分（0 - 59）
# |  ——時（0 - 23）
# | |  ——日（1 - 31）
# | | |  ——月（1 - 12）
# | | | |  ——曜日（0 - 6）
# | | | | |
# * * * * *
```

## CronJobコンソールのアクションガイド

### CronJobの作成

1. [Tencent Kubernetes Engineコンソール](https://console.cloud.tencent.com/tke2)にログインします。
2. 左側ナビゲーションバーでは、【Cluster】をクリックして、クラスター管理ページへ進みます。
3. CronJobの作成を必要とするクラスターIDをクリックして、CronJobが作成されるクラスター管理ページへ進みます。
4. 「Workload」 > 「CronJob」を選択して、CronJob情報ページへ進みます。以下の通りです：
![CronJob](https://main.qcloudimg.com/raw/881d1fd3e52cfc6fa421f22820c09419.png)
5. 【 Create】をクリックして、「Create workload」ページへ進みます。以下の通りです：
![Workloadの新規作成](https://main.qcloudimg.com/raw/cc40dbd25618e72c92e47b0397443e7d.png)
6. 実際のニーズに応じて、CronJobパラメータを設定します。キーパラメータの情報は以下の通りです：
 - ワークロード名：カスタマイズします。
 - ネームスペース：実際のニーズに応じて選択します。
 - タイプ：「CronJob（Cronのスケジュールに従って定時に実行する）」を選択します。
 - 実行ポリシー：Cronフォーマットに基づいてタスクを設定する定期的な実行ポリシーです。
 - Jobの設定
    - 繰り返し回数：Jobによって管理されるPodを繰り返し実行する必要がある回数です。
    - 並列性：Jobを並列に実行するPodの数です。
    - 失敗リスタートポリシー：Podではコンテナが異常終了した後のリスタートポリシーです。
        - Never：Podではすべてのコンテナが終了するまで、コンテナがリスタートされません。
        - OnFailure：Podが実行し続けて、コンテナがリスタートされます。
 - インスタンス内のコンテナ：実際のニーズに応じて、CronJobのPodに1つ又は複数の異なるコンテナを設定します。
    - 名称：カスタマイズします。
    - イメージ：実際のニーズに応じて選択します。
    - イメージバージョン：実際のニーズに応じて入力します。
    - CPU/メモリ制限：[Kubernetes リソース制限](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/)に基づいて、CPUおよびメモリの制限範囲を設定することができ、サービスのロバストを向上させます。
    - 詳細設定：「**作業ディレクトリ**」、「**実行コマンド**」、「**実行パラメータ**」、「**コンテナ健康診断**」、「**特権レベル**」などのパラメータを設定できます。
7. 【Create  workload】をクリックして、作成が完了します。

### CronJob状態の確認

1. [Tencent Kubernetes Engineコンソール](https://console.cloud.tencent.com/tke2)にログインします。
2. 左側ナビゲーションバーでは、【Cluster】をクリックして、クラスター管理ページへ進みます。
3. CronJob状態の確認を必要とするクラスターIDをクリックして、CronJob状態が確認されるクラスター管理ページへ進みます。
4. 「Workload」 > 「CronJob」を選択して、CronJob情報ページへ進みます。以下の通りです：
![CronJob](https://main.qcloudimg.com/raw/adee4e9199660c39f61fc091273d3999.png)
5. 状態の確認を必要とするCronJob名称をクリックして、CronJobの詳細を確認できます。

## KubectlによるCronJobのアクションガイド

<span id="YAMLSample"></span>
### YAMLの例

```Yaml
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: hello
spec:
  schedule: "*/1 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: hello
            image: busybox
            args:
            - /bin/sh
            - -c
            - date; echo Hello from the Kubernetes cluster
          restartPolicy: OnFailure
```
- kind：CronJobリソースタイプを標識します。
- metadata：CronJobの名称、Labelなどの基本情報です。
- metadata.annotations：CronJobに関する追加説明であり、このパラメータを使用してTencent Cloud TKEの追加の拡張機能を設定できます。
- spec.schedule：CronJobによって実行されるCronのポリシーです。
- spec.jobTemplate：Cronによって実行されるJobのテンプレートです。

### CronJobの作成

#### 方法1

1. [YAMLの例](#YAMLSample)を参照して、CronJob YAMLファイルを準備します。
2. Kubectlをインストールして、クラスターに接続されます。アクションの詳細については、[Kubectlによるクラスターへの接続](https://cloud.tencent.com/document/product/457/8438)をご参照ください。
3. 次のコマンドを実行して、CronJob YAMLファイルを作成します。
```shell
kubectl create -f CronJob YAMLファイル名称
```
例えば、ファイル名がcronjob.yamlであるCronJob YAMLファイルを作成するには、次のコマンドを実行します。
```shell
kubectl create -f cronjob.yaml
```

#### 方法2

1. `kubectl run`コマンドを速やかに実行することによって、CronJobを速やかに作成します。
例えば、完全な構成情報を書き込む必要がないCronJobを速やかに作成するには、次のコマンドを実行します：
```shell
kubectl run hello --schedule="*/1 * * * *" --restart=OnFailure --image=busybox -- /bin/sh -c "date; echo Hello"
```
2. 次のコマンドを実行して、作成が成功したかどうかを確認します。
```shell+-
kubectl get cronjob [NAME]
```
下記のような情報が返された場合は、作成が成功したことを示しています。
```
NAME      SCHEDULE    SUSPEND   ACTIVE    LAST SCHEDULE   AGE
cronjob   * * * * *   False     0         <none>          15s
```

### CronJobの削除
>!
> - この削除コマンドを実行する前に、作成中のJobが存在するかいやかを確認してください。そうしないと、このコマンドを実行したら、作成中のJobを終了します。
> - この削除コマンドを実行するとき、作成したJobおよび完了したJobの両方とも、終了または削除されません。
> - CronJobによって作成されたJobを削除するには、手動で削除してください。

次のコマンドを実行して、CronJobを削除します。
```
kubectl delete cronjob [NAME]
```


