### Cluster Autoscaler と監視指標に基づくノードのAuto Scalingはどのようなちがいがありますか。

Cluster Autoscaler はロードに関わらず、クラスター内のすべてのPodをスケジューリングできます。監視指標に基づくノードのAuto Scaling は、自動でスケールイン・アウトする際にPodを考慮しませんが、Podのないノードを追加したり、システムの中核Podがあるノードを削除したりする場合があります。Kubernetes は、このような自動スケーリングを推奨しません。 Cluster Autoscaler と監視指標に基づくAuto Scalingのノードは競合するため、両方ともに有効にしないでください。

### CA とスケーリンググループはどのような対応関係にありますか。

CAを有効にしたクラスターは、選択されたノード設定に従って、起動設定を作成し、その起動設定のスケーリンググループをバインディングします。バインディング後、そのスケーリンググループ内でスケールイン・アウトをして、スケールアウト後のCVMは自動的にクラスターに入れられます。自動スケールイン・アウトのノードは従量制課金です。スケーリンググループに関しては [Auto Scaling 資料](https://intl.cloud.tencent.com/document/product/377)をご参照ください。

### Tencent Kubernetes Engine (TKE) コンソールで手動で追加したノードはCAスケールインすることはありますか。

ありません。CAスケールインのノードはスケーリンググループ内のノードに限られます。 [TKE コンソール](https://console.cloud.tencent.com/tke2) で追加されたノードはスケーリンググループに追加されません。

### Auto Scaling コンソールで、Cloud Virtual Machine (CVM) の追加や削除ができますか。

できません。[Auto Scaling コンソール](https://console.cloud.tencent.com/autoscaling)にて、設定を変更する一切の操作は推奨されていません。

### スケールイン・アウトは選択したノードのどのような設定を継承しますか。

スケーリンググループ作成時、 [起動設定](https://intl.cloud.tencent.com/document/product/377/8543)を作成するために、クラスター内のあるノードを参考として選択する必要があります。参考としたノードの設定は以下の通りです。
 - vCPU
 - メモリ
 - システムディスクのサイズ
 - データディスクのサイズ
 - ディスクタイプ
 - 帯域幅
 - 帯域幅課金モデル
 - パブリックネットワークIPの割当
 - セキュリティグループ
 - Virtual Private Cloud
 - サブネット

### 複数のスケーリンググループを使用するには？

サービスの重要度やタイプといった特徴によって、複数のスケーリンググループを作成し、スケーリンググループに異なるラベルを設定することで、スケーリンググループからスケールアウトしたノードのラベルを指定することができます。これにより、サービスを分類します。

### スケールイン・アウトの最大値はいくつに設定できますか。

現在、Tencent Cloudユーザーには各アベイラビリティゾーンにつき30の従量課金CVMクォーターが利用可能です。スケーリンググループで30台を超えた従量課金のCVMをご希望の場合、[チケットの提出](https://console.cloud.tencent.com/workorder/category) を通して申請してください。
詳細のクォーターについては現在のアベイラビリティーゾーンのCVMの [インスタンス及びクォーター](https://console.cloud.tencent.com/cvm/overview)をご参照ください。また、Auto Scalingにも最大値の制限があり、最大値は200となっています。それ以上の値を希望する場合、[チケットの提出](https://console.cloud.tencent.com/workorder/category)から申請してください。

### クラスターに対してスケールインを有効にするのは安全ですか。

ノードをスケールインする際にPodをスケジューリングしなおすため、スケジューリングと一時中断後の再度スケールインを許容する必要があります。サービスに [PDB](https://kubernetes.io/docs/tasks/run-application/configure-pdb/) を設定することを推奨します。PDBは、実行中のPodセットのコピーの最小数または最小パーセンテージを任意の時点で指定できます。PodDisruptionBudget を使用すると、アプリケーションデプロイヤーは同一時点で行ったPodを削除するクラスターオペレーションが過剰にPodを廃棄しないことを保証し、、データ紛失やサービス中断、許容できないダウングレードを回避することができます。

### ノード上にどんなPodがあるとスケールインされなくなりますか。

 - 厳密に設定された PodDisruptionBudget の Pod が PDB を満たさない時、スケールインされません。
 - Kube-system の Pod。
 - ノード上に deployment、replica set、job、stateful set以外のコンソールで作成された Podが存在します。
 - Podにローカルストレージがあります。
 - Pod は他のノード上にスケジューリングできません。

### ノードがスケールインの条件を満たしてからスケールインされるまでどのくらいの時間がかかりますか。

所要時間は10分です。

### ノードがNot Ready 状態になってからスケールインされるまでどのくらいの時間がかかりますか。

所要時間は20分です。

### どのくらいの間隔で、スケールイン・アウトが必要かどうかをスキャンしますか。

スキャン間隔は10秒です。

#### CVMにスケールアウトするまでどのくらいの時間がかかりますか。

基本的には10分以内ですが、Auto Scalingに関しては [Auto Scaling](https://intl.cloud.tencent.com/document/product/377)をご参照ください。

### Unschedulable の Pod があるのに、スケールアウトされないのはなぜですか。

以下の事項を確認してください：
- Podのリクエストリソースが大きすぎる。
- node selector を設定しているか。
- スケーリンググループは最大値に達しているか。
- アカウントの残高（残高不足の場合、Auto Scaling はスケールアウトできません）、または、クォーターなどが不足しているか。詳細については、 [Auto Scaling トラブルシューティング](https://intl.cloud.tencent.com/document/product/377/8626)をご参照ください。


### Cluster Autoscaler が特定のノードをスケールインするのは、どのように防ぐことができますか。

``` sh
# ノードのannotationsに次のメッセージを設定してください。
kubectl annotate node <nodename> cluster-autoscaler.kubernetes.io/scale-down-disabled=true
```


### スケールイン・アウトのイベントは、どのようにフィードバックされますか。

Auto Scaling コンソールにて、スケーリンググループのスケーリング状況を調べたり、k8sイベントを閲覧できます。以下の３つのリソースは対応するイベントがあります：
- kube-system/cluster-autoscaler-status config map
    - **ScaledUpGroup** - CA がスケールアウト。
    - **ScaleDownEmpty** - CA が実行されていないPodのあるノードを１つ削除。
    - **ScaleDown** - CA がスケールイン。
- node
    - **ScaleDown** - CAがスケールイン。
    - **ScaleDownFailed** - CA がスケールインすることに失敗。
- pod
    - **TriggeredScaleUp** - CA がこのPodによってスケールアウト。
    - **NotTriggerScaleUp** - CA はスケールアウトできるスケーリンググループが見つからなかったため、このPodをスケジューリングできません。
    - **ScaleDown** - CA はこのPodを追い出すことで、ノードのスケールインを試みました。


